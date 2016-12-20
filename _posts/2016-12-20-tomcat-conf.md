---
layout: post
title: Tomcat项目跨域问题(Tomcat7)
categories: Tomcat7
description: 这是一个简单的跨域处理方法， 通过修改 tomcat 配置文件就能实现。
keywords: Tomcat7
---

在tomcat.6.0.27以上版本，跨域问题有简单解决方法：

在tomcat 的conf 目录下面　编辑：context.xml

将里面的Context修改为以下即可：
``` java 
 <Contextsession CookiePath="" sessionCookieDomain=".×××.com"/>
```
问题得到解决
>注: .xxx.com   xxx 是你的域名。

之前的tomcat6跨域解决方法是自己创建jar包。