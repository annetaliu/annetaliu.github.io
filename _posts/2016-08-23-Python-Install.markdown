---
layout: post
title:  Python:Install
date:   2016-08-23 
categories: python
permalink: /python/install
---

python 安装和几年前比较已经变得越来越简单了，但是因为不同版本间的差异带来的一些安装问题很棘手，下面记录下我遇到过的一些情况（针对linux操作系统）：
经常我们一台机器上装了多个版本的python:

* 可以用的安装库的方法：
	* 下源码编译安装： 通常是setup.py install/build
		* 安装的目标路径怎么选择？
			* 可以默认安装到系统默认python的pythonpath里
			* 可以通过参数安装到指定目录？ 这个方法可以实现库的迁移么？
	* easy_install ：只是一个脚本
		* 
	* pip 
		* 依赖于easy_install
		* yum类的操作系统喜欢用这个，pip支持比较好；
		* apt-get 对这个的支持不太好， apt-get 可以通过 install python-libname 的方式很简单地安装各种库；
	* 

* 为不是默认的python安装库：
	* 下源码编译安装： 源码编译安装也会涉及到python版本差异
	

* 安装两个以上的python版本，如何共存，区分调用？
	* 默认的python是在PATH里定义的那些路径下最先找到的python的可执行文件所对应的版本。
	* 可以同时装多个python，并且设置到PATH里，通过pythonX ，就是加版本号的方式打开不同的python解析器
	* 那么，问题来了，多个版本怎么管理他们的安装的库呢？
		* 默认会在对应的site-package下找库，还可以通过环境变量的设置修改库的路径。 
		* 那么不同版本之间的安装好的库可以通用么？
			* 不同版本之间不一定能用
		* 不同平台下（OS）安装的库可以通用么？
			* 我记得以前是可以有个egg包来实现的，貌似最近python不太流行这种用法了。为什么？
		

* 两个版本该如何安装库呢？默认版本好说，不是默认的版本怎么处理？


* linux的操作系统，比如centos， yum命令和python的版本是有关系的，如果手动修改python的默认版本yum可能不能用。
	
* 默认python2.7.8 ， 系统里的另外一个python3.5.1需要安装lxml: [用pip](https://pip.pypa.io/en/stable/installing/)
	* ubuntu 类的系统很简单：
		* apt-get install python3-lxml  - so easy
	* yum就糟糕了： 网上一堆的操作wiki,结果都不行…………
		* 直接安装是不行的
		* 升级默认python下的pip：  pip install -U pip
		* 下载  [get-pip.py](https://bootstrap.pypa.io/get-pip.py)
		* python get-pip.py :pip2/3貌似都有了

	
