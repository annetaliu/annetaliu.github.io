---
layout: post
title:  CodeStyle Check 
date:   2016-09-14
categories: CI
permalink: /codestyle/index
---

代码规范的检查指标，通常有静态和动态检查区分。

**静态检查：**

* 复杂度：圈复杂度，时间复杂度，空间复杂度，算法复杂度，
* 重复度


**动态检查：**

* 覆盖率（比如UT覆盖率）
* 复杂度：时间复杂度，空间复杂度，算法复杂度，

---

**针对C/C++**


**针对java**

* Apache Maven Checkstyle Plugin 
* maven PMD: also support CPD	
* maven findbugs

	* 官网的说明都很好用
	* 检查的内容
	* 默认是sun的java标准，也可以找到google标准的代码配置xml；也可以自己修改，定制标准
	* 过滤一些文件、目录的方式： 通过comment过滤很方便

