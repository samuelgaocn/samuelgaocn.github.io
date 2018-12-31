---
layout: post
category: "read"
title:  Linux  12月23号日常操作
tags: [Linux,Centos]
---

linux环境yum异常：BDB1507 Thread died in Berkeley DB library
2018年08月03日 14:14:43 tjsahwj 阅读数：84
安装svn时报出如下问题：



解决办法如下：

解释：

删除/var/lib/rpm目录下的__db开头的rpmdb文件

rm -f /var/lib/rpm/__db*

rpm数据库重建

rpm --rebuilddb

清理所有yum缓存

yum clean all

重新生成yum缓存

yum makecache



.tar.gz     格式解压为          tar   -zxvf   xx.tar.gz

.tar.bz2   格式解压为          tar   -jxvf    xx.tar.bz2