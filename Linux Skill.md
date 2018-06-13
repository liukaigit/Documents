### Linux Skills
**1、core dump file**
- 生成可调式coredump file，需程序编译阶段添加编译选项`-g`，才可借用gdb工具调试，该功能的开关如下所示：
    - 开启
        - `ulimit -c unlimited`
            - 不限制coredump的大小，将所有信息全部生成到coredump file
    - 关闭
        - `ulimit -c 0`
    - 查看
        - `ulimit -c`

**2、多行操作**
- 多行添加
    - 光标置于目标位置，按组合键`ctrl + v`，进入列模式，选择所有待处理行
    - 按组合键`shift + i`，进入插入模式，输入插入字符
    - 按`Esc`键退出，所有行同步插入字符
- 多行删除
    - 光标置于目标位置，按组合键`ctrl + v`，进入列模式，按上下键选择所有待处理行，按左右键选择待处理字符
    - 按`x`键删除选中字符

**3、系统时间**
- 查看
    - `date`
    - `date +%s`
        - 系统时间转换成秒
- 修改时间
    - `date -s 时:分:秒`
- 修改日期
    - `date -s 月/日/年`

**4、grep命令**
- 文本搜索工具，区别find命令，简介如下：
    - `-i` ignore case   忽略大小写
    - `-v` invert match  不匹配
    - `-n` number        输出匹配的文件名及行数
- 示例
    - `grep -n "txt" ./* -r` 
        - `./adir/b.txt:1:fdasftxt` 

**5、编译未定义**
- 声明是否OK
- 依赖动态库或静态库是否OK
- 头文件顺序是否OK

**6、环境变量**
- LIBRARY_PATH
    - 用于程序编译期间查找依赖动态库，这个变量可以忽略，在编写Makefile时用LDFLAGS来设置共享库链接路径
- LD_LIBRARY_PATH
    - 用于程序加载运行期间查找指定共享库
    - 临时添加通过命令：
        `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$PWD`
    - 还可以通过修改`/etc/ld.so.conf`或者添加`/etc/ld.so.conf.d/xxx.conf`来添加自定义共享库加载路径，`ldconfig`重载这些配置

**7、路由规则**
- 添加默认路由
    - `route add default gw xxx.xxx.xxx.xxx dev vEthx`
- 删除默认路由
    - `route del default` 
- 添加指定网段路由
    - `route add -net xxx.xxx.xxx.0/24  gw xxx.xxx.xxx.xxx dev vEthx`

**8、iotop**
- 监控磁盘I/O使用状况，涉及主要参数和命令如下：
    - `-o`      只显示有I/O操作的进程
    - `-p PID`  监控指定进程
    - `a`  记录启用`iotop`之后，显示进程累计的I/O使用量

**9、tee命令**
- tee命令读取标准输入数据，并将内容写入文件，对于错误的命令将不写入到文件，相关参数如下：
    - `-a` 内容追加到文件
- 示例如下
    - `ls | tee -a a.txt`
        - `ls`内容输出到终端的同时通过tee保存一份到`a.txt`，因有`-a`参数内容追加到`a.txt`尾部 

**10、bash快捷键**
- `ctrl + a`  
    - 跳转至行首
- `ctrl + e`
    - 跳转至行尾
- `ctrl + \->` 或 `<\-`
    - 按单词快速移动光标
- `ctrl + k`
    - 删除光标开始至结尾所有字符
- `ctrl + u`
    - 删除光标开始至行首所有字符
- `ctrl + l`
    - 通clear命令清屏
- `ctrl + r`
    - 历史命令查找 

**11、tree命令**
- 以树形结构显示文件目录结构，主要参数如下：
    - `-C`  大写，通过颜色区分目录和文件
    - `-D`  大写，显示目录更改时间
    - `-f`  小写，显示完整相对路径
- 示例
    - `tree . -C -D -f`
    ```
    .
    ├── [May 25 14:54]  ./adir
    │.. └── [May 25 14:59]  ./adir/b.txt
    ├── [May 25 11:21]  ./a.out
    └── [May 25 11:20]  ./t.c 
    ```
**12、find命令**
- 用来查找文件，不同于grep搜索的是文件内容，几个常用的参数如下：
    - `-name`   查找文件名
    - `-type b/d/c/p/l/f`   文件类型块设备、目录、字符设备、管道、符号链接、普通文件
- 示例
    - `find ./* -type f "*txt*"`
        ```    
        ./adir/b.txt
        ```
    - `find . -type f \( -name "*x*" -or -name "*t" \)`
        ```
        ./adir/b.txt
        ./.test
        ./a.out
        ```

**13、who命令**
- 显示目前登录系统的用户信息，相关命令参数如下所示：
    - `who`
        ```
        root     pts/0        2018-05-25 11:19 (172.16.130.81)
        root     pts/1        2018-05-25 14:40 (172.16.130.75)
        root     pts/2        2018-05-25 14:58 (172.16.130.54)
        ```
    - `w`
        ```
        USER     TTY        LOGIN@   IDLE   JCPU   PCPU WHAT
        root     pts/0     11:19    4:20m  0.04s  0.04s -bash
        root     pts/1     14:40    4.00s  0.11s  0.00s w
        root     pts/2     14:58   41:56   0.04s  0.04s -bash
        ```
**14、shell脚本格式**
- windows系统编辑的shell脚本，直接拷贝到linux系统后，直接运行会出现问题：
    - `-bash: ./shellcode: /bin/bash^M: bad interpreter: No such file or directory`
- 解决方法，打开shell文件运行命令，修改文件格式：
    - `set fileformat=unix`

**15、修改网卡MAC地址**
- 临时修改，设备重启或者network服务重启后失效
    - `ifconfig vEthx hw ether 00:AA:BB:CC:DD:EE`
- 永久修改，需要修改网卡的系统配置，添加如下字段
    - `MACADDR=00:AA:BB:CC:DD:EE`

**16、watch命令**
- 定时监听查看某服务信息，示例
    - watch -n2 "cat /var/log/sss.log"

**17、network.service失败**
- 失败现象如下：
    ```
    May 14 21:24:16 localhost.localdomain network[1465]: Bringing up interface enp8s0:  Error: Connection activation failed: Connection 'enp8s0' is not available on the device enp8s0 at this time.
    May 14 21:24:16 localhost.localdomain network[1465]: [FAILED]
    ```
- 解决方法
    - 检测ifcfg-enxxx网卡配置信息，包括HWADDR,NAME,UUID等
        - 命令`nmcli connection` 用来查看网卡UUID信息，需要开启`NetworkManager.service`服务
    - 对于centos7版本，关闭冲突`NetworkManager.service`服务
    - 重启服务`systemctl restart network.service`
    
**18、malloc重载coredump**
- 实际工作遇到的触发情况，在注册信号函数里面编写过多代码，尤其是调用malloc分配内存，malloc不支持重入

**19、ASCII表**
- 0 对应    48
- A 对应    65
- a 对应    97

**20、ipset命令**
- 对数据包进行过滤，可以有集合的概念，支持超时自动清理功能，常用命令简介如下：
    - 创建ipset，带超时timeout，默认超时时间
        `ipset create mylist hash:ip timeout 10` 
    - 添加iptables规则
        `ipset add mylist xxx.xxx.xxx.xxx`
        
**21、mysql版本查看**
- 快速查看mysql版本，先确保`mysqld`服务已经正常运行，然后借助`help`命令查看版本，命令如下：
    ```
    # mysql --help| grep Distrib
    结果如下：
    mysql  Ver 14.14 Distrib 5.6.32, for Linux (x86_64) using  EditLine wrapper
    ```
