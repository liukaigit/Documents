## Python 性能优化

**1.the python profilers**
- 常用的python性能分析器包括：cProfile、profile和hotshot，相关参考链接：https://docs.python.org/2/library/profile.html
重点介绍cProfile工具的使用；
- cProfile
  - 脚本性能检测方法：
  ```
    python -m cProfile [-o output_file] [-s sort_order] myscript.py
      -o writes the profile results to a file instead of to stdout
      -s specifies one of the sort_stats() sort values to sort the output by. This only applies when -o is not supplied.
  ```
- pstats
  - 处理cProfile检测生成的二进制文件，处理方法如下所示：
    - python -c "import pstats; p=pstats.Stats('output_file'); p.print_stats()"
