#### Redis操作
**参考链接**
- redis常用接口参考链接：
	- https://blog.csdn.net/y472360651/article/details/77951595?locationNum=7&fps=1
- redis阻塞事件：
	- https://blog.csdn.net/immershy/article/details/77150842


**1.集合操作**
- 简介：
	- 集合包括：有序和无序集合；
		- 无序集合就是不允许元素重复的列表，添加的元素存在则不重复添加；
		- 有序集合元素包含值和分数，根据分数排序；

- 应用场景：
	- 目前项目实际应用为有序集合，用于存储变更的节点信息，可并发读取集合所有数据，清理时根据获取数据的分数范围清理，数据不会被丢失或覆盖，写入集合前先获取集合最大分数递增后添加；
	- redis对集合操作支持原子性；
	- 适应变更数据频率较低，保证缓存失效性的同时，保证获取数据速度；
	- 对于定时变更数据大的场景，需配合定时全量更新缓存即可；
	- 仅限于单个键值小于1M的场景，对于python二样键值过大（字符串），将引发python进程内存泄漏（内存不释放）；
	- 场景1：
		- A/B/C进程读取redis缓存数据；D/E进程写redis变更集合数据；
		- A/B/C进程尝试获取更新缓存数据锁，先读取redis全量变更集合数据（0，-1），再获取redis缓存，处理变更数据，若获取更新缓存锁，先更新redis缓存，再删除获取的redis变更集合数据（按照分数范围清理，元素不存在忽略）；
		- D/E进程写数据前先获取集合增锁（阻塞获取文件锁），确保获取分数和写数据的原子性（获取集合最大分数递增再添加到集合）；

- 有序集合主要操作
	- zadd(name,*args,**kwargs)：在name对应的有序集合中添加元素，分数越小，越靠前
		- name：键
		- args：键值对,例如:‘n1’,1,‘n2’,2
		- kwargs：键值对，例如:‘n1’=1,‘n2’=2
	- zrange(name,start,end,desc=False,withscores=False,score_with_func=float)：获取name对应的有序集合中,start<=下标<=end的所有数据。
		- name：键
		- start：起始位置
		- end：结束位置
		- desc：是否是倒序，默认False
		- withscores：是否获取分数,默认False
		- score_with_func：分数类型
	- zremrangebyscore(name,min,max)：删除在name对应的有序集合中,min<=分数<=max的数据
		- name：键
		- min：小(分数)
		- max：大(分数)
	
**2.键操作**
- 简介：
	- 字符串操作，key-value
	- 字典操作，hashname,key,vlaue
- 应用场景：
	- 目前项目实际应用主要是字典操作，用来存储节点和拓扑信息的json格式数据；就目前的操作粒度而言为字典键，其实是存在获取多余的信息加载到缓存，空耗进程内存资源（不精细化）；
	- 键的操作原子性，适用于键值较小的场景，对于键值超过1M的场景，将同时影响redis（写操作）和调度进程（读操作）的内存消耗，控制键值大小是保证系统稳定性关键；
	- 场景2：
		- 产品管理资源不断扩展，单个键值大小不可避免超过1M，通过精简化单个键值大小也只能够环境，当不可控数据量出现时将大概率是调度进程和redis进程内存爆增，系统崩溃凉凉；为兼容扩展，分如下两个方法处理：一是一定的算法将
	字典的元素进行拆分，多个字典键存储，读取时获取所有键值后进行拼接组装数据；二是因拆分字典键后，整个字典键值的操作无法继续通过redis单个键原子操作保证，需要在业务代码进行封装，获取字典键值时阻塞拿读锁；更新字典键值时阻塞
	拿写锁；
		- 对于拆分后的子字典键注意更新后清理残留；
		- 上述方案需要通过实际验证，包括拆分字典键的算法，需要结合字典键值大小（单个元素之和不能直接转换合成之后的字段键值计算长度）和元素个数进行拆分；
- 字符串操作：
	- set(name,value,ex=None,px=None,nx=False,xx=False)：设置键值
		- name：键
		- value：值
		- ex：过期时间(秒)
		- px：过期时间(毫秒)
		- nx：True时，name存在才会执行set操作
	- get(name)：获取键值
		- name：键
	- strlen(name)：获取name对应值的长度
		- name：键
	- incr(name,amount)：name不存在,则name=amount，name存在，则name对应的值+amount
		- name：键
		- amount：自增值
	- decr(name,amount)：name不存在，则name=amount，name存在，则name对应的值-amount
		- name：键
		- amount：自减值
	- append(key,value)：在key对应的值后面追加value
		- name：键
		- value：追加的值
	
- 字典操作
	- hset(name,key,value)：存储字典
		- name：键
		- key：字典的key
		- value：字典的值
	- hget(name,key)：获取name对应的字典中对应key的值
		- name：键
		- key：字典的key
	- hmset(name,mapping)：存储字典
		- name：键
		- mapping：字典，如：{“info”:“shenzhen”,“age”:18}
	- hmget(name,keys,*args)：获取字典的值
		- name：键
		- keys：字典键,如：hmget(“name”,[“info”,“age”])
		- args：字典键，如：hmget(“name”,“info”,“age”)
	- hgetall(name)：获取字典(dict格式)
		- name：键
	- hlen(name)：获取字典的长度
		- name：键
	- hkeys(name)：获取字典的所有key
		- name：键
	- hvals(name)：获取字典的所有value
		- name：键
	- hexists(name,key)：name对应的字典中是否存在键key
		- name：键
		- key：字典的key
	- hdel(name,*args)：删除name对应的字典中的键值对
		- name：键
		- args：字典的key元组

**3.其他操作**

- delete(*names)：删除Redis中的任意数据类型
	- names：键
- exists(name)：判断键是否存在
	- name：键
- keys(pattern="*")：获取符合规则的所有键
	- pattern：通配符,默认*获取所有。常见:"*h"：h结尾的键；“h*”：h开头的键；“h*x”：h开头,x结尾的键；“h[ae]x”：获取名为hax或hex的键
- expaire(name,time)：设置超时时间
	- name：键
- info：查看redis实时信息
	- info clients：查看当前连接请情况；
- ttl：获取键的过期时间
	- num表示过期秒
	- -1 表示无过期时间
	- -2 表示键不存在；
