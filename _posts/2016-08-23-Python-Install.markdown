---
layout: post
title:  Python:Install
date:   2016-07-23 01:11:26 -0000
categories: python
permalink: /python/install
---

python 安装和几年前比较已经变得越来越简单了，但是因为不同版本间的差异带来的一些安装问题很棘手，下面记录下我遇到过的一些情况：


* 可以用的安装库的方法：
	* 自己编译
	* easy_install
	* pip
	* 


* 安装两个以上的python版本，如何共存，区分调用？

* 两个版本该如何安装库呢？默认版本好说，不是默认的版本怎么处理？


* linux的操作系统，比如centos， yum命令和python的版本是有关系的，如果手动修改python的默认版本yum可能不能用。
	
* 默认python2.7.8 ， python 3.5.1 需要安装lxml: [用pip](https://pip.pypa.io/en/stable/installing/)
	* 升级默认python下的pip：  pip install -U pip
	* 下载  [get-pip.py](https://bootstrap.pypa.io/get-pip.py)
	* python get-pip.py :pip2/3貌似都有了

	
