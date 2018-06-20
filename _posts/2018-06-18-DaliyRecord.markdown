---
layout: post
category: "read"
title:  Linux  Golong
tags: [Linux,Debian]
---

	1、修改系统变量

echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
2、保存生效

sysctl -p
3、查看内核是否已开启BBR

sysctl net.ipv4.tcp_available_congestion_control
显示以下即已开启：

# sysctl net.ipv4.tcp_available_congestion_control
net.ipv4.tcp_available_congestion_control = bbr cubic reno
4、查看BBR是否启动

lsmod | grep bbr
显示以下即启动成功：

# lsmod | grep bbr
tcp_bbr                20480  14



2
3
wget --no-check-certificate https://github.com/kuoruan/shell-scripts/raw/master/kcptun/kcptun.sh

sudo wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh

firewall-cmd --list-ports

2018-06-05 14:43:41
Centos7端口管理
1.查看已开放的端口(默认不开放任何端口)
firewall-cmd --list-ports
2.开启80端口
firewall-cmd --zone=public(作用域) --add-port=80/tcp(端口和访问类型) --permanent(永久生效)

3.重启防火墙
firewall-cmd --reload
4.停止防火墙
systemctl stop firewalld.service
5.禁止防火墙开机启动
systemctl disable firewalld.service
6.删除
firewall-cmd --zone= public --remove-port=2667/tcp --permanent

/usr/sbin/iptables -I INPUT -p tcp --dport 28998 -j ACCEPT


1）安装IUS软件源

复制
#安装EPEL依赖
sudo yum install epel-release

#安装IUS软件源
sudo yum install https://centos7.iuscommunity.org/ius-release.rpm
2）安装Python3.6

复制
sudo yum install python36u
安装Python3完成后的shell命令为python3.6，为了使用方便，创建一个到python3的符号链接

复制
sudo ln -s /bin/python3.6 /bin/python3
3）安装pip3

安装完成python36u并没有安装pip，安装pip

复制
sudo yum install python36u-pip
安装pip完成后的shell命令为pip3.6，为了使用方便，创建一个到pip3的符号链接

复制
sudo ln -s /bin/pip3.6 /bin/pip3


pip3 install jupyter

jupyter notebook --generate-config

jupyter notebook password

vi /root/.jupyter/jupyter_notebook_config.json   

vi /root/.jupyter/jupyter_notebook_config.py   

c.NotebookApp.ip='*' #设置访问notebook的ip，*表示所有IP，这里设置ip为都可访问  
c.NotebookApp.password = u'sha1:5df252f58b7f:bf65d53125bb36c085162b3780377f66d73972d1' #填写刚刚生成的密文  
c.NotebookApp.open_browser = False # 禁止notebook启动时自动打开浏览器(在linux服务器一般都是ssh命令行访问，没有图形界面的。所以，启动也没啥用)  
c.NotebookApp.port =8889 #指定访问的端口，默认是8888。  

firewall-cmd --permanent --zone=public --add-port=2667/tcp
firewall-cmd --reload

https://pytorch.org/

pip3 install http://download.pytorch.org/whl/cpu/torch-0.4.0-cp36-cp36m-linux_x86_64.whl 

conda install pytorch -c pytorch 

pip install torchvision
pip3 install torchvision




