**1、cProfile优化辅助工具**
- 测试示例文件：
  - func.py
- 运行示例脚本：
  - python -m cProfile -o test.out func.py
- 获取运行结果，并按时间排序
  - python -c "import pstats; p=stats.Stats('test.out');p.sort_stats('time').print_stats()"

`上述运行和结果获取可以写入shell脚本，并通过重定向将脚本运行信息和接口检测信息写入文本方便查看`
   
