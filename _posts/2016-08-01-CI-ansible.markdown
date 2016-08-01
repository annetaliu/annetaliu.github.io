---
layout: post
title:  CI Automation -ansible
date:   2016-08-01 01:11:27 -0800
categories: CI
permalink: /CI/ansible
---

the difference between git clone

Ansible:

* 首先配置我自己的电脑来个demo： 通过playbook设置所有的配置,可以用来管理自己的电脑的配置。
	* apt-get install ansible (add addtional repo if needed)
	* 配置
	* playbook: 
		* 语法:[yaml](https://zh.wikipedia.org/wiki/YAML) 基本概念，元素： 
			* variables; 
			* inventories: list for the resouces (ips...);custom things;支持range等语法
			* 语法： 开头---， 注释#，缩进要求很严格，list by -;
		* playbook contains plays : yaml文件可以多个同时执行,执行之后可以找到配置文件： rols/raw/
		* play contain tasks: name, do steps.
		* tasks contain moudules: 标准的格式调用module； 基本的shell命令都有。		
	* how to run ansible:
		* Ad-Hoc: 执行临时的不需要保存的命令
		* ansible localhost -m modulesname
		* ansible-playbook **.yaml 执行了配置的命令
			* log的展示： changed， ok， 一些软件的版本升级也可以在log中体现。
	* ansible tower: 提供了GUI的界面。
	* Q: 和alias相比，优势有什么？
* 更多应用： 
	* 大量的服务器集群管理；经常重复的命令管理：比如git的一些配置命令。
	* 管理自己的多台机器的配置；
	* 管理could上的大量的服务器列表(jenkins slave);
	* distcc的后台服务器列表申请和维护；
	* 
	
		
		
		
