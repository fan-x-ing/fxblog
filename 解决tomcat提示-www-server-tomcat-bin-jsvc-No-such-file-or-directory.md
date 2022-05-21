title: 解决tomcat提示/www/server/tomcat/bin/jsvc:No such file or directory
categories: 教程
tags: [宝塔,tomcat,java]
date: 2021-09-13 12:21:00
---
最近我在折腾tomcat的时候，tomcat竟然无法正常使用。如果强制启动会提醒（daemon.sh: line 196: /www/server/tomcat/bin/jsvc: No such file or directory）



`jsvc`是`tomcat`的进程守护文件，我还专门去看了看，发现没有这个文件。今天我就教大家如何解决。



# 问题

安装好`tomcat`无法正常启动，如图：

![fanxing/2d7020913111420.png](https://q2.a1pic.cn/BTTs.webp)

## 解决

提示目录确实缺少`jsvc`这个文件，这里我给大家打包好了，下载了解压到`/www/server/tomcat/bin`这个目录就好

[hide]https://cloud.189.cn/web/share?code=IjIV73qqMf2m（访问码：mod2）[/hide]