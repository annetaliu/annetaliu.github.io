---
layout: post
title:  "Start Jekyll Blog on GitHub"
date:   2016-06-20 04:11:26 -0900
categories: blog in jekyll
---
## 如何快速地创建自己的博客？ 
Jekyll on github 是一个灰常棒的选择:

* 从域名到服务器都是`免费`的： 
	* geithub上创建项目，上传jekyll的代码即可。	
* 更新管理内容方便： 
	* `markdown`等标记文档把格式和内容都掌控在自己手里。
	* Jekyll的文档中英文版本都很好用。
* 丰富多样的`主题模版`提供选择：
	* 自己创建或者去rubygem网站找模版。


## 基本步骤：
* 安装好基本软件，库，启动demo的网站

``` bash
jekyll server -H 10.0.2.15
```

![log](/images/jekyll-blog-1-server-start-log.png)

* 本地调试之后上传到github, github的项目名称有格式规定，比如我的是：annetaliu.github.io
* 尝试添加demo之外的第一篇文章
	* 在_post 目录之下添加类似格式的文章。默认markdown 格式（配置文件可以修改）。
	* 我碰到一个问题，因为电脑的时间设置问题，第一篇没有显示，时间戳的模式有个好处是可以预约发送。
* 去网上找好看的主题。默认的主题太单一了。很多人写了各种主题开源，选择太多也是个问题呀。

	
	
