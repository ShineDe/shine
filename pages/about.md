---
layout: page
title: About
description: 打码改变世界（马赛克）
keywords: ShineDe, DeHai
comments: true
menu: 关于
permalink: /about/
---

我是ShineDe.   Welcome to my blog

博客模板来自[@mzlogin](https://github.com/mzlogin)的分享
代码源于思想，思想源于探索 
探索源于热爱， 我们不是码农 
我们是改变世界的科学家 


## 坚信

* 熟能生巧
* 努力改变人生
* 积极、乐观、热爱生活
* 没有不可能，只有不努力

## 联系

* GitHub：[@ShineDe](https://github.com/shinede)
* 博客：[{{ site.title }}]({{ site.url }})
* 微博: [@空心菜没有心ing](http://weibo.com/3626494712)
* 知乎: [@ShineDe](http://www.zhihu.com/people/shinede)
* 豆瓣: [@ShineDe](http://www.douban.com/people/153431026)

## Skill Keywords

#### Software Engineer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_software_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>

#### Mobile Developer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_mobile_app_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>

#### Windows Developer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_windows_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>
