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
  
