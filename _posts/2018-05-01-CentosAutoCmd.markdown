---
layout: post
category: "read"
title:  Linux  Centos 7 服务自动启动
tags: [Linux,Centos]
---

CentOS 7添加开机启动服务/脚本
[日期：2016-12-09]	来源：Linux社区  作者：startcentos	[字体：大 中 小]

 
一、添加开机自启服务

在CentOS 7中添加开机自启服务非常方便，只需要两条命令(以Jenkins为例)：
systemctl enable jenkins.service #设置jenkins服务为自启动服务
sysstemctl start  jenkins.service #启动jenkins服务

二、添加开机自启脚本

在centos7中增加脚本有两种常用的方法，以脚本autostart.sh为例：
#!/bin/bash
#description:开机自启脚本
/usr/local/tomcat/bin/startup.sh  #启动tomcat

方法一

1、赋予脚本可执行权限（/opt/script/autostart.sh是你的脚本路径）
chmod +x /opt/script/autostart.sh

2、打开/etc/rc.d/rc/local文件，在末尾增加如下内容
/opt/script/autostart.sh

3、在centos7中，/etc/rc.d/rc.local的权限被降低了，所以需要执行如下命令赋予其可执行权限
chmod +x /etc/rc.d/rc.local

方法二

1、将脚本移动到/etc/rc.d/init.d目录下
mv  /opt/script/autostart.sh /etc/rc.d/init.d

2、增加脚本的可执行权限
chmod +x  /etc/rc.d/init.d/autostart.sh

3、添加脚本到开机自动启动项目中
cd /etc/rc.d/init.d
chkconfig --add autostart.sh
chkconfig autostart.sh on

以上两种方法均已在centos7系统上验证过，如有疑问，欢迎大家评论留言。

更多CentOS相关信息见CentOS 专题页面 http://www.linuxidc.com/topicnews.aspx?tid=14

本文永久更新链接地址：http://www.linuxidc.com/Linux/2016-12/138079.htm

/etc/rc.local
/etc/rc.sysinit
/etc/inittab
/etc/profile