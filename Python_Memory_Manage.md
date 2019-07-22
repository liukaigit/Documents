## Python 内存管理机制

Python内存管理机制包括：垃圾回收、引用技术和内存池机制，重点关注内存池机制；

**1.内存池机制**
- 分层的Python内存分配机制，如下所示：
 ```
 Pyhon对象操作
  |
 Python内存池，PyMem_Malloc，小内存1~256KB直接分配，大内存大于256KB调用malloc申请（不释放free内存）
  |
 C malloc/free操作
 -------
 系统内存操作
 ```
- 各类型消耗内存，如下所示：
 ```
 >>> import sys
 >>> sys.getsizeof(1)
 24
 >>> sys.getsizeof([])
 72
 >>> sys.getsizeof(())
 56
 >>> sys.getsizeof({})
 280
 >>> sys.getsizeof(True)
 24
 ```
- 字典类型默认初始化包含8个元素，若分配的字典元素个数小于8个，则存在内存浪费（这个）；

