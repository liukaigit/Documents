## Python 内存管理机制

Python内存管理机制包括：垃圾回收、引用技术和内存池机制，重点关注内存池机制；

**1.内存池机制**
- 分层的Python内存分配机制（参考链接：http://svn.python.org/projects/python/trunk/Objects/obmalloc.c ），如下所示：
```
   Object-specific allocators
      _____   ______   ______       ________
      [ int ] [ dict ] [ list ] ... [ string ]       Python core         |
   +3 | <----- Object-specific memory -----> | <-- Non-object memory --> |
       _______________________________       |                           |
      [   Python's object allocator   ]      |                           |
   +2 | ####### Object memory ####### | <------ Internal buffers ------> |
       ______________________________________________________________    |
      [          Python's raw memory allocator (PyMem_ API)          ]   |
   +1 | <----- Python memory (under PyMem manager's control) ------> |   |
       __________________________________________________________________
      [    Underlying general-purpose allocator (ex: C library malloc)   ]
    0 | <------ Virtual memory allocated for the python process -------> |

      =========================================================================
       _______________________________________________________________________
      [                OS-specific Virtual Memory Manager (VMM)               ]
   -1 | <--- Kernel dynamic storage allocation & management (page-based) ---> |
       __________________________________   __________________________________
      [                                  ] [                                  ]
   -2 | <-- Physical memory: ROM/RAM --> | | <-- Secondary storage (swap) --> |
```
- 网络资源总结如下：
```
 Pyhon对象操作
  |
 Python内存池，PyObject_Malloc和PyMem_Malloc，小内存1~256KB直接分配，大内存大于256KB调用malloc申请（不释放free内存）
  |
 C malloc/free操作
 -------
 系统内存操作
 ```

**2.内存占用**
- 采集python不同类型数据占用内存情况，如下所示：
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

