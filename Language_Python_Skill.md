**1、\_\_name\_\_ == '\_\_main\_\_'**
- Make the script importable and executable.
  -  脚本模块既可以导入到其他模块使用，也可以模块本身运行
 
**2、\_\_init\_\_**
-  创建类实例时调用进行初始化：
  ```
  class XyyTzz:
    def __init__(self):
      self.b = 12
      self.a = 2
    
    ...
  ```
  
**3、自定义module**
- python2.7安装目录，添加自定义模块目录，简单示例：
  - 创建目录如下：
  ```
  |-- __init__.py       
  |-- __init__.pyc
  |-- const.py
  `-- const.pyc
  ```
  - `__init__.py`一般为空，作用是将文件夹变成一个python模块
  - `const.py`里面封装模块方法，本示例放置变量供测试
  ```
  # cat const.py
  # coding=utf-8
  TEST_NAME = 'This is a test.'
  ```
  - 终端测试调用`const`里面的变量`TEST_NAME`，示例如下所示：
  ```
  >>> from  mytest import const
  >>> print "%s" % const.TEST_NAME
  This is a test.
  ```
  
**4、os模块**
- 对目录和文件操作常用的方法列表
- `os.listdir('dir')`
  - 列出指定`dir`目录内文件和子目录
- `os.path.exists('file or dir')`
  - 检查文件或路径是否存在
- `os.path.isfile('file')`
  - 检查是否为文件
- `os.path.isdir('dir')`
  - 检查是否为目录
- `os.path.basename('path/filename')`
  - 提取`filename`返回
- `os.path.split('path/filename')`
  - 路径文件分割，结果`('path','filename')`
- `os.path.splitext('filename')`
  - 文件名名称和扩展名分割，结果`('名称','扩展名')`
- `os.path.join('path','filename')`
  - 路径文件名拼接，结果`path/filename`
- `os.getsize('file')`
  - 获取文件大小
- `os.WNOHANG`
  - `os.waitpid()`的选项，当没有子进程状态是返回`（0，0）`
- `os.chmod('keyfile',0oxxx)`
  - `os.chmod('./test.sh',0o777)`将当前目录`test.sh`文件权限修改成`777`注意`0o`
  
**5、ConfigParser模块**
- 该模块为python解析配置文件标准库，配置文件格式如下：
  ```
  [section1]
  option1 = 12
  option2 = 'test'
  
  [section2]
  option1 = 'test2'
  option2 = 23
  
  ...
  ```
- 常用的方法如下
  - 加载配置文件，创建对象`config`，然后通过调用对象方法`read`加载配置文件
  ```
  config = ConfigParser.ConfigParser()
  config.read(configpath)
  ```
  - 获取配置文件所有`section（section1,section2）`
  ```
  config.sections()
  ```
  - 获取指定`section1`的选项所有参数`option`
  ```
  config.options(section1)
  ```
  - 获取指定`section1`的`option1`的值
  ```
  config.get(section1,option1)
  ```

**6、字符串前后缀检查**
- 前缀检查`str`字符串是否包含前缀`prefix`，格式：`str.startswith(prefix)`
  ```
  >>> str = "This is a test."
  >>> prefix = 'This'
  >>> str.startswith(prefix)
  True
  >>>
  ```
- 后缀检查`str`字符串是否包含后缀`suffix`，格式：`str.endswith(suffix)`
  ```
  >>> str = "This is a test."
  >>> suffix = 'est.'
  >>> str.endswith(suffix)
  True
  >>>
  ```

**7、多字符串拼接join方法**
- 语法：`'sep'.join(seq)`
- 参数说明
  - `sep`：分隔符，可以为空
  - `seq`：要连接的元素序列、字符串、元组、字典
- 返回值：返回一个以分隔符sep连接各个元素后生成的字符串
- 示例
  ```
  >>> list = ['123','456','789']
  >>> sep = '-'
  >>> string = sep.join(list)
  >>> print string 
  123-456-789
  >>>
  ```
  
**8、列表排序sort/sorted**
- `sort`方法改变列表原有顺序，`sorted`方法排序后生成新列表
- `sort`方法示例：
  ```
  >>> list = ['923','456','789']
  >>> list.sort()
  >>> print list
  ['456', '789', '923']
  >>>
  ```
- `sorted`方法示例：
  ```
  >>> list = ['923','456','789']
  >>> other = sorted(list)
  >>> print other
  ['456', '789', '923']
  >>> print list
  ['923', '456', '789']
  >>>
  ```
- `key function`扩展，多元素比较，示例：
  ```
  >>> list = [('d',3),('b',5),('d',6),('a',1)]
  >>> print sorted(list, key = lambda y:(y[0],y[1]))
  [('a', 1), ('b', 5), ('d', 3), ('d', 6)]
  >>> print sorted(list, key = lambda y:(y[1],y[0]))
  [('a', 1), ('d', 3), ('b', 5), ('d', 6)]
  >>> list = [('d',3),('b',5),('d',6),('a',1),('c',3)]
  >>> print sorted(list, key = lambda y:(y[1],y[0]))
  [('a', 1), ('c', 3), ('d', 3), ('b', 5), ('d', 6)]
  >>>
  ```

**9、对象类型比较方法isinstance**
- 语法：`isinstance(object,classinfo)`
- 示例1：
  ```
  >>> a = 1
  >>> isinstance(a,int)
  True
  >>> isinstance(a,float)
  False
  >>>
  ```
- 示例2，类对象比较
  ```
  >>> class Test:
  ...     def __init__(self):
  ...         self.a = 1
  ... 
  >>> test = Test()
  >>> isinstance(test,Test)
  True
  >>>
  ```

**10、作用域**
- 全局变量能够被文件任何地方调用，但修改只能全局操作；
- 局部变量只在函数内部使用，若是没有找到所需变量，则往外进行查找。

**11、装饰器wrapper**
- 直接看示例，不考虑参数，若是考虑参数的情况可用：`(*args, **kwarg)`：
  ```
  def dec1(func):
    print "one+++"
    def one():
        print "one---start-----"
        func()
        print "one----end-------"
    return one


  def dec2(func):
    print "two+++"
    def two():
        print "two-----start----"
        func()
        print "two------end-----"
    return two

  @dec1
  @dec2
  def test():
    print "My name is %s" % __name__

  test()
  结果：
  two+++
  one+++
  one---start-----
  two-----start----
  My name is __main__
  two------end-----
  one----end-------
  ```

**12、函数**
- 函数包括：def关键字、函数名、可选参数列表，return关键字，示例：
  ```
  def func():
    return 0
  func()
  ```
- func的命名空间随函数开始而开始，结束而销毁
- 函数也有属性，可以把函数当作参数一样传递给其他函数，示例：
  ```
  def add(x,y):
    return x + y

  def apply(test, x, y):
    return test(x, y)

  print apply(add, 3, 4)
  运行结果：
    7
  ```

**13、获取函数名**
- 方法一：引用函数名直接调用参数`__name__`，如下示例：
  ```
  def func():
    print func.__name__
  运行结果：
    func
  ```
  
- 方法二：通过添加装饰器的方法获取函数名，如下示例：
  ```
  def get_funcname(func):
    def run():
        print func.__name__
        func()
    return run

  @get_funcname
  def myprint():
    print "This is a test."
  运行结果：
    myprint
    This is a test.
  ```

**14、模块引入**
- 相对引入
  - 比如对celery模块的引用，当前目录mycelery存在模块celery.py时，import celery将优先引入本地模块，若本地无该模块，将引入系统celery模块；
- 绝对引入
  - 通过添加如下引用，import celery将直接引用系统模块若需要调用本地celery模块，可采用import mycelery.celery方式导入
  `from __future__ import absolute_import`

**15、打印堆栈**
- 命令
  ```
  import traceback
  traceback.print_stack()
  ```
