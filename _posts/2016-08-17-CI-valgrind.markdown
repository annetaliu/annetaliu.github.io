---
layout: post
title: Valgrind practise
date:   2016-08-17 01:11:26 -0000
categories: valgrind
permalink: /CI/valgrind
---

VALGRIND check(这里我只基于监控C、C++的UT,当然也支持其他的行为): [官方使用手册](http://valgrind.org/docs/manual/manual.html)

* 配置： 因为不是安装在默认路径下的，在调用的时候需要设置VALGRIND_LIB
	* 旧的做法是设置LD_LIBRARY_PATH，现在已经不能用了，而且这个设置比较危险。
	* 需要通过ld --library-path 添加库来执行ut case的时候，在新版valgrind下不支持，可以在编译的时候用-rpath,libpath 来达到这个目的，把的路径
	* [basic options](http://valgrind.org/docs/manual/manual-core.html#manual-core.toolopts)

* supported toolname:
	--tool=<toolname> [default: memcheck]
           Run the Valgrind tool called toolname, e.g. memcheck, cachegrind, callgrind,
           helgrind, drd, massif, lackey, none, exp-sgcheck, exp-bbv, exp-dhat, etc.
	
* toolname supported:	
	* memcheck : 
		* valgrind memcheck 运行时间消耗比较大，官方说*40，说是用sanitizer=adress 可以替代memcheck，效果可能更好，运行时间只有*2
		* valgrind memcheck 和sanitizer=adress 是不能同时使用的： “ Shadow memory range interleaves with an existing memory mapping. ASan cannot proceed correctly. ABORTING. ”
	* 

	

---

Ext refs：

* [关于C编译选项的说明](http://duanple.blog.163.com/blog/static/7097176720111141085197/) 这个总结很好
* [多种检查memory的工具比较](https://techtalk.intersec.com/2013/12/memory-part-5-debugging-tools/)
* [valgrind is not a leak-checker](http://maintainablecode.logdown.com/posts/245425-valgrind-is-not-a-leak-checker ) 
* [valgrind和sanitizer=adress 是冲突的](https://sourceforge.net/p/valgrind/mailman/message/35040138/)
* [AdressSanitizer](https://github.com/google/sanitizers/wiki/AddressSanitizer)

以下内容请忽略，只是私人的问题记录草稿：

* 因为valgrind不是安装在系统上的，怎么调用？
	* 用**/ld.so ----library-path xx:xx **/bin/valgrind ./ut 时报错valgrind: failed to start tool 'memcheck' for platform 'amd64-linux': No such file or directory
		设置变量VALGRIND_LIB=**/lib64/valgrind  以上错误没有了，如果检查ls这条命令是没有报错，但是执行./ut会报以下错误。
	
	* 设置时候报错： error while loading shared libraries: libasan.so.1: cannot open shared object file
	感觉是因为valgrind调用到的库找不到链接
	* 设置LD_LIBRARY_PATH为asan所在的地址  --有其他的time的方法找不到
	  设置LD_LIBRARY_PATH为asan所在的地址，加上所有其他的lib,还继承原来的LD_LIBRARY_PATH:Shadow memory range interleaves with an existing memory mapping. ASan cannot proceed correctly
		* LD_PRELOAD indicate asan.so
	  设置LD_LIBRARY_PATH为空的话，还是libasan找不到： 不能通过设置LD_LIBRARY_PATH,很危险。
	* LDFLAGS: -fPIC -lasan 把库直接链接进去 :not working 
	* -Wl,-Bstatic -lasan 所有的静态链接都说找不到了 ? 在编译的时候
	* -Bstatic -lasan ： error while loading shared libraries: liblz4.so.1 这个东西为什么找不到呢？ 在执行case的时候
		* 设置LD_LIBRARY_PATH 之后 make: error while loading shared libraries: __vdso_time: invalid mode for dlopen(): Invalid argument
		* LIBRARY_PATH会在编译的时候找的路径，LD_LIBRARY_PATH则是在执行的时候找的路径
	* 想试试LD_PRELOAD=valgrind.so 但是，cannot find this so in my laptop		
	
	* -fsanitize=undefined,address 这个flag对编译为什么会有影响？，去掉之后居然报错，
	有地方说这个不支持子线程： http://stackoverflow.com/questions/31099373/suppressing-gtk-errors-in-valgrind 

	* 在valgrind的线程下，动态库的链接找不到，用静态的话好多
	
	* 把执行ut需要的库的地址用-rpath 加到链接选项中， 就可以不用后期执行时加ld --library-path了
	* valgrind在执行的时候加载库asan出错，加在这个库时有问题，：==31106==Shadow memory range interleaves with an existing memory mapping. ASan cannot proceed correctly. ABORTING. ： [valgrind和sanitizer=adress 是冲突的](https://sourceforge.net/p/valgrind/mailman/message/35040138/)
		* LD_PRELOAD indicate asan.so: 没有用。
		* root cause: Address Sanitizer is another recent tools used for memory check, which can replace somepart of valgrind memcheck.
	* valgrind for memory-check : https://techtalk.intersec.com/2013/12/memory-part-5-debugging-tools/
		
		
		