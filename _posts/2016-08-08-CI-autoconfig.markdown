---
layout: post
title: Automake & Autoconf
date:   2016-08-08 01:11:26 -0800
categories: CI
permalink: /CI/automake
---

**automake**：程序开发人员只需要写一些简单的含有预定义宏的文件:

* 由autoconf根据一个宏文件生成configure,
	autoconf需要[GNU M4](http://my.oschina.net/ReJaVu/blog/184503)宏处理器来处理aclocal.m4,生成configure脚本.
* 由automake根据另一个宏文件生成Makefile.in,
* 再使用configure依据Makefile.in来生成一个符合惯例的 Makefile.

**autoconf**

* 各种参数设置，判断，生成的Makefile的大部分参数都通过这个文件设置

  
  
**相关命令介绍**

* autoscan
	* configure.scan --> configure.in 
* aclocal : createaclocal.m4 by scanning configure.ac".
* autoconf :
	* .configure
* Makefile.am: 用来生成Makefile.in
* automake： 生成makefile.in

**生成的makefile支持：**

* make：
　　根据Makefile编译源代码,连接,生成目标文件,可执行文件.
* make clean
　　清除上次的 make命令所产生的 object文件（后缀为".o"的 文件）及可执行文件.
* make install
　　将编译成功的 可执行文件安装到系统目录中,一般为/usr/local/bin目录.
* make dist
　　产生发布软件包文件（即distribution package）.这个命令将会将可执行文件及相关
文件打包成一个tar.gz压缩的 文件用来作为发布软件的 软件包.
　　它会在 当前目录下生成一个名字类似"PACKAGE-VERSION.tar.gz"的 文件.PA
CKAGE和VERSION,是 我们在 configure.in中定义的 AM_INIT_AUTOM
AKE(PACKAGE, VERSION).
* make distcheck
　　生成发布软件包并对其进行测试检查,以确定发布包的正确性.  


    
**配置文件**

* automake的配置文件 *.am
* autoconfig的配置文件 *.ac
	* autoreconf
	

**执行**

* 生成configure文件
