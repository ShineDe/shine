---
layout: post
title:  第一次利用Git命令创建仓库,并提交代码
categories: 提交git
description: 初次提交git，第一次提交git
keywords: 第一次提交git
---

记录git使用的方法和命令，熟练使用基础命令，第一次利用Git命令创建仓库,并提交代码。

<!--more-->


**1. 首先在git.oschina.net上新建一个项目**

**2. 在本地目录下，执行如下命**

```java

git init

git add .

git config user.name 'xxx'

git config user.email 'xxxx@xx.com'

git pull https://git.oschina.net/xxx/xxx.git master

git remote add origin https://git.oschina.net/xxx/xxx.git

git commit -am 'init'

git push -u origin master

```
