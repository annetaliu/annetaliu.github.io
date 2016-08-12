---
layout: post
title:  Python Advanced1:less than class
date:   2016-06-27 01:11:26 -0900
categories: python
permalink: /python/advanced1
---
This page is About:

* __List comprehensions__
* __Iterator & Generators__
* __Discriptors & Properties__
* __Decrators__
* __Contextlib__

---

* **list comprehensions**   
	* vectorization [矢量化编程的概念](http://ufldl.stanford.edu/wiki/index.php/%E7%9F%A2%E9%87%8F%E5%8C%96%E7%BC%96%E7%A8%8B)
    * enumerate() 遍历list同时得到index,value. 可用于提高效率，尤其在矢量化编程中。
    * [VS map() and / or filter()](http://www.secnetix.de/olli/Python/list_comprehensions.hawk):
        map() and / or filter(), list comprehensions 可以解决类似的一些问题,但是通常列表推导的效率、可读性更高。 
    * Q: 为什么for循环的执行速度会比较慢？
    
```Python
>>> [i for i in range(1,10) if i%2 == 0 ]
[2, 4, 6, 8]

>>> [i*2 for i in range(1,5)]
[2, 4, 6, 8]

>>> [x for x in range(2, 50) if x not in [j for i in range(2, 8) for j in range(i*2, 50, i)]]
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]    
```

* **iterators & generators 迭代器和生成器**
    * 迭代器本身是一个底层的的特性和概念，为生成器提供了基础
    * 生成器： 当需要一个返回一个的函数，或返回在循环中执行的函数时，就应该考虑生成器。
		* 基于yield：暂停一个函数，并返回中间结果
		* send()
		* next() VS throw(exceptions)
		* close(): GeneratorExit exception. 不管什么exception 接到，iterator就结束了，这意味着GeneratorExit。
	* ?make code simple, not data: 有许多简单的处理序列值的可迭代函数，要比一个复杂的、每次计算一个值的函数更好些。
	
``` python
>>> def fibonacci():
...     a,b = 0,1
...     while True:
...         yield b
...         a, b = b, a+b
>>> f = fibonacci() 
>>> f.next()
1
>>> f.next()
1   
>>> f.next()
2 
>>> f.next()
3 
>>> [f.next() for i in range(0,10)]
[5, 8, 13, 21, 34, 55, 89, 144, 233, 377]
``` 
``` python
>>> def testge():
...     print "welcome"
...     try:
...             print "first try"
...             yield "try 1"
...     except ValueError:
...             print "got exception"
...             yield "except 2"
...     finally:
...             print "finally"
...             yield "last 3"
...     print "end"
...     yield "bye"
...
>>> a=testge()
>>> a.throw(ValueError("error1"))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 1, in testge
ValueError: error1
>>> a.next()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>>
>>> b=testge()
>>> b.next()
welcome
first try
'try 1'
>>> b.next()
finally
'last 3'
>>> b.next()
end
'bye'
>>> b.next()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration

``` 

* ？用generator编写coroutine协同程序:可以挂起、恢复，并且有多个进入点的函数，例如多任务，管道机制，每个协同程序将消费或生成数据，然后暂停，直到其他数据被传递。
	* 其他语言的经典实现： [lua](https://zh.wikipedia.org/wiki/Lua)脚本语言，[more](http://www.runoob.com/lua/lua-tutorial.html)
	* VS 线程：线程需要资源锁以避免线程之间的冲突
	* trampoline
	* greenlet
	* contextlib
	

* 生成器表达式： 类似列表推导的语法（代替yield）来构造生成器.
	* 用圆括号代替方括号：整个序列和list comprehensions一样都不会事先进行计算.
	* 以此来代替yield表达式可以减少序列代码的总量
		
``` python
>>> iter = (x**2 for x in range(1,10) if x%2 == 0 )
>>> for ite in iter:
...     print ite
...
4
16
36
64
```

* itertools模块	
	* 提供了许多高效迭代器模式,可以用各种方式对数据进行循环操作，此模块中的所有函数返回的迭代器都可以与for循环语句以及其他包含迭代器（如生成器和生成器表达式）的函数联合使用。
	* islice, tee, groupby
		* islice: 抽取位于流中特定位置的数据，可以看作在每行数据之上的一个滑动窗口。
		* tee: 往返式的迭代器
		* groupby：uniq迭代器， 当需要在数据上完成一个摘要时，结合sorted函数，可以把相似的元素放到一起。
			* ex:使用行程长度编码(RLE)来压缩数据：字符中每组相邻的重复字符将替换成字符本身和重复次数。 [LZ77压缩](https://zh.wikipedia.org/wiki/LZ77%E4%B8%8ELZ78)
	* itertools的工具都可以自行实现。itertools只是提供了更加成形的解决方案。 [一些函数](http://www.cnblogs.com/vamei/p/3174796.html)
		* 无穷循环器： count, cycle, repeat
		* 函数式工具： imap, starmap, ifilter, ifilterfalse, takewhile, dropwhile
		* 组合工具： chain, product, permutations, combinations, combinations_with_replacement
		
* **Decrators**
	* 封装函数和方法，增强一个函数（通常是改变作用域，类型？）。 ？方法和函数的差别？ 
		* ex: @classmethod  ,@staticmethod  替代了用对应的方法增强函数的操作。 
		* 关注所封装的函数或方法的接受和返回的参数，减少[introspection](https://www.hikyle.me/archives/581/)
		* 常用于： 参数检查;缓存代理;上下文提供者
			* ex: 提供xmlrpc的签名认证
			* ex: 多线程共享的数据，多重访问的保护锁。 

* **with and contextlib**
	* __enter__() 和 __exit__()之间的步骤
	* 和try... finally ...相比，with简化了实现过程：对于即使发生一些错误也能进行代码清理
		* 关闭一个文件
		* socket
		* 释放一个锁
		* 创建一个临时代码补丁
		* 在特殊环境中运行受保护的代码	
	* contextlib是为了加强with语句，提供上下文机制的模块，它是通过Generator实现的。
		* nested, closing
		* ？下面的例子我的理解是： @contextmanager 增加了__enter__() 和 __exit__() 这个上下文。
		
``` bash
[anne@BTSOM-1 test]$ cat test.py
from contextlib import contextmanager

@contextmanager
def make_context() :
    print 'enter'
    try :
        yield {}
    except RuntimeError, err :
        print 'error' , err
    finally :
        print 'exit'

with make_context() as value :
    print value

print "============="
def new_context():
    print 'enter'
    try:
        yield {}
    except RuntimeError, err:
        print 'error',err
    finally:
        print 'exit'

with new_context() as value:
    print value

```		
```	bash	
[anne@BTSOM-1 test]$ python test.py
enter
{}
exit
=============
Traceback (most recent call last):
  File "test.py", line 26, in <module>
    with new_context() as value:
AttributeError: __exit__
		
```		