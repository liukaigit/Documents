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
  - os.waitpid()的选项，当没有子进程状态是返回（0，0）
  
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
