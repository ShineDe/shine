---
layout: post
title:  搬瓦工 FinalSpeed + SS 实现科学上网加速
categories: 科学上网加速
description: FinalSpeed SS 实现科学上网加速
keywords: 科学上网加速
---

FinalSpeed是高速双边加速软件,可加速所有基于tcp协议的网络服务,在高丢包和高延迟环境下,仍可达到90%的物理带宽利用率,即使高峰时段也能轻松跑满带宽。

<!--more-->

我这边是能流畅的看1080P，当然实际的速度要看你的宽带，下面这张是视频截图可以看到视频加载很流畅。话不多说开始教程了


![enter image description here](http://7xsod9.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20170329110055.png)

## 安装服务端

安装前说明：

1. 服务器建议至少256M内存。

2. openvz架构只支持udp协议，搬瓦工属于openvz。

3. 服务端可以和锐速共存,互不影响。

4. FinalSpeed必须服务端和客户端同时配合使用,否则没有任何加速效果。

5. 官方地址： [http://www.ip4a.com/](http://www.ip4a.com/)

## 一.windows版服务端

说明：Windows版服务端运行需要java环境和winpcap。

下载地址：[点击下载finalspeed-service-windows1.0](https://pan.baidu.com/s/1nvwiUmt)

## 二.linux版服务器端（本人Centos6）

服务端会启动iptables，如果服务器修改过ssh的默认端口，请先开放你的ssh端口，否则可能导致ssh连接失败。

不熟悉不要乱改配置，如果无法连接，请卸载后一键安装，不要做任何修改,严格按照教程操作。

开放端口命令（下面的命令是为了防止安装之后连不上ssh）

首先Xshell登陆你的VPS 

输入：

> **service iptables start**

继续：（端口号要改成你VPS的SSH端口号）

> **iptables -I INPUT -p tcp --dport 端口号 -j ACCEPT**

>**iptables -I OUTPUT -p tcp --sport ssh端口号 -j ACCEPT**

>**service iptables save**

一键安装命令：（依次输入就行）


>**rm -f install_fs.sh**

>**wget  http://soft.paozailushang.com/vps/install_fs.sh**

>**chmod +x install_fs.sh**

>**./install_fs.sh 2>&1 |\|| tee install.log**

![](http://7xsod9.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20170329111932.png)

输入完得到这个就是成功。 因为没有启动所以找不到日志。

使用 **sh /fs/start.sh** 命令启动服务

## 三.配置windows

Windows版：[finalspeed_install1.12.exe](https://pan.baidu.com/s/1kVFjT2n)

##  <span style="color:red">注意问题：</span>

服务器必须同时部署 FinalSpeed 服务端才能进行加速。

客户端必须准确设置物理带宽，最终加速的速度不会超过所设置的带宽值，如果设置值高于实际带宽会造成丢包，导致速度变慢。

客户端首选tcp协议,如果udp不稳定，请切换到tcp。

若服务器为openvz架构，客户端只能选择udp协议,其他架构同时支持tcp和udp协议。

windows 客户端使用 tcp 协议时不兼容锐速，停止锐速后可以正常运行。

FinalSpeed 不提供加密功能,如有安全需求，不要直接加速明文协议。

## 四.加速Shadowsocks

假设SS服务器的IP为[235:561:109:56] （也可以是ipv4的地址），FinalSpeed端口为默认150，Shadowsocks 端口为433。

设置服务器地址，选择UDP协议，物理宽带是你实际的宽带值，不能超过你当前的宽带值，否则可能影响使用。

![](http://7xsod9.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20170329113049.png)

点击添加

名称和本地端口可以随便填 ，加速端口填写服务器ss端口 ，默认是443

![](http://7xsod9.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20170329113630.png)


设置SS客户端 密码即为SS密码


![](http://7xsod9.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20170329114047.png)

设置完后  如果出现

![](http://7xsod9.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20170329114235.png)

就说明成功了  连连youtube试试速度吧

## 五.其他使用说明

更新：执行一键安装会自动完成更新。

卸载：

>**sh /fs/stop.sh ; rm -rf /fs**

启动：

>**sh /fs/start.sh**

停止：

>**sh /fs/stop.sh**

重新启动：

>**sh /fs/restart.sh**

运行日记

>**tail -f /fs/server.log**

设置开机启动：

依次输入：

>**chmod +x /etc/rc.local**

>**vi /etc/rc.local**

按 i 进入编辑模式 加入

>**sh /fs/start.sh**

每天晚上3点自动重启

>**crontab -e**

>**0 3 * * * sh /fs/restart.sh**

大概效果如下图

![](http://7xsod9.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20170329114714.png)


教程到此差不多结束了 有不懂的在下面留言问我吧