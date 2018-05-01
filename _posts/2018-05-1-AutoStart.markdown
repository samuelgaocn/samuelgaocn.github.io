---
layout: post
category: "read"
title:  Linux  开机启动
tags: [Linux,Autostart]
---
a. 在/etc/rc.d/rc.local文件中加入下面行
   /etc/init.d/vncserver start
b. 编辑/etc/sysconfig/vncservers
   VNCSERVERS="1:root"
   VNCSERVERARGS[1]="-geometry 1024x768" --配置启动的桌面
多个用户可以这样写：
VNCSERVERS= "1:user 2:user2 3:user3"


redhat系统上vnc启动命令：
/etc/init.d/vncserver start
查看vnc启动情况
netstat -tulnp
关闭服务器上自己的vnc链接
vncserver -kill :桌面号
例如：关闭上面的vnc链接
vncserver -kill :1 

chkconfig vncserver on

