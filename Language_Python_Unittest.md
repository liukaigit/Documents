### Python单元测试简介

**1、环境搭建**
- 覆盖率检测工具`coverage`
  - 资源：`coverage-4.5.1-cp27-cp27mu-manylinux1_x86_64.whl`
  - 下载地址：`https://pypi.org/project/coverage/#files`
  - 安装前提win7系统已经安装python2.7（跟上述的工具包版本信息cp27对应），安装命令如下：
  `安装路径\python27\Scripts>pip.exe install 安装包路径\coverage-4.5.1-cp27-cp27m-win_amd64.whl`
 
**2、创建包**
- 目录结构如下
  ```
  |-- __init__.py
  |-- myapi.py
  `-- test.py
  ```

- 编写`myapi.py`，添加方法，如下所示：
  ```
  #!/usr/bin/env python
  # _*_ coding: utf-8 _*_
  
  
  def myapi_add(x, y):
    print "%d + %d = %d" % (x, y, x + y)
    
  if __name__ == '__main__':
    myapi_add(3, 4)
  
  独立运行结果：
    3 + 4 = 7
  ```
  
- 编写`test.py`，添加单元测试方法，如下所示：
  ```
  #!/usr/bin/env python
  # _*_ coding: utf-8 _*_
  from myapi import myapi_add
  import unittest


  class myunittest(unittest.TestCase):

    def test_add(self):
        myapi_add(3, 4)

  if __name__ == '__main__':
    unittest.main()
  独立运行结果：
    3 + 4 = 7
  ```
  
**3、覆盖率检测**
- win7系统打开`powershell`超级终端，`cd`进入到上述代码目录，利用`coverage`工具执行`test.py`脚本检测`myapi.py`代码覆盖率
- 执行检测命令如下：
  - `安装路径\coverage.exe run .\test.py`
  - 输出结果如下：
  ```
  3 + 4 = 7
  .
  -----------
  Ran 1 test

  OK
  ```
  
- 执行覆盖率检测结果文本信息命令如下：
  - `安装路径\coverage.exe report`
  - 结果如下：
  ```
  Name       Stmts   Miss  Cover
  ------------------------------
  myapi.py       5      1    80%
  test.py        8      0   100%
  ------------------------------
  TOTAL         13      1    92%
  ```
- 执行覆盖率检测结果html信息命令如下：
  - `安装路径\coverage.exe html`
  - 上述命令执行成功后，在当前路径下生存子目录`htmlcov`，可以用浏览器打开`index.html`查看结果
