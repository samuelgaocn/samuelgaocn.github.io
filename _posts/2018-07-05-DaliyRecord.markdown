---
layout: post
category: "read"
title:  Linux  Golong
tags: [Linux,Debian]
---

	升级内核，第一步首先是升级内核到支持BBR的版本：
1.yum更新系统版本：

yum update

2.查看系统版本：

[root@server ~]# cat /etc/redhat-release 
CentOS Linux release 7.4.1708 (Core) 
[root@server ~]# 
3.安装elrepo并升级内核：

[root@server ~]# rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
[root@server ~]# rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
[root@server ~]# yum --enablerepo=elrepo-kernel install kernel-ml -y
4.更新grub文件并重启系统：

[root@server ~]# egrep ^menuentry /etc/grub2.cfg | cut -f 2 -d \'
CentOS Linux 7 Rescue 8619ff5e1306499eac41c02d3b23868e (4.14.14-1.el7.elrepo.x86_64)
CentOS Linux (4.14.14-1.el7.elrepo.x86_64) 7 (Core)
CentOS Linux (3.10.0-693.11.6.el7.x86_64) 7 (Core)
CentOS Linux (3.10.0-693.el7.x86_64) 7 (Core)
CentOS Linux (0-rescue-c73a5ccf3b8145c3a675b64c4c3ab1d4) 7 (Core)
[root@server ~]# grub2-set-default 0
[root@server ~]# reboot
5.重启完成后查看内核是否已更换为4.14版本：

[root@server ~]# uname -r
4.14.14-1.el7.elrepo.x86_64
[root@server ~]#
6.开启bbr：

[root@server ~]# vim /etc/sysctl.conf    # 在文件末尾添加如下内容
net.core.default_qdisc = fq
net.ipv4.tcp_congestion_control = bbr
7.加载系统参数：

[root@vultr ~]# sysctl -p
net.ipv6.conf.all.accept_ra = 2
net.ipv6.conf.eth0.accept_ra = 2
net.core.default_qdisc = fq
net.ipv4.tcp_congestion_control = bbr
[root@vultr ~]#
如上，输出了我们添加的那两行配置代表正常。

8.确定bbr已经成功开启：

[root@vultr ~]# sysctl net.ipv4.tcp_available_congestion_control
net.ipv4.tcp_available_congestion_control = bbr cubic reno
[root@vultr ~]# lsmod | grep bbr
tcp_bbr                20480  2 
[root@vultr ~]# 
输出内容如上，则表示bbr已经成功开启。