---
layout: post
category: "read"
title:  Linux  5月4号日常操作
tags: [Linux,Centos]
---
 
	 http://71bbs.people.com.cn/postImages/D3/19/08/A5/1523960055973.gif
	 
	 LightCloud 推荐
	 https://my.lightvm.com/aff.php?aff=202
	 http://t.cn/RuBlhRV
	 
	 Centos7安装Python3的方法
由于centos7原本就安装了Python2，而且这个Python2不能被删除，因为有很多系统命令，比如yum都要用到。

    [root@VM_105_217_centos Python-3.6.2]# python
    Python 2.7.5 (default, Aug  4 2017, 00:39:18)
    [GCC 4.8.5 20150623 (Red Hat 4.8.5-16)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
输入Python命令，查看可以得知是Python2.7.5版本

输入

    which python
可以查看位置，一般是位于/usr/bin/python目录下。

下面介绍安装Python3的方法

首先安装依赖包

    yum -y groupinstall "Development tools"
    yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
然后根据自己需求下载不同版本的Python3，我下载的是Python3.6.2

    wget https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tar.xz
如果速度不够快，可以直接去官网下载，利用WinSCP等软件传到服务器上指定位置，我的存放目录是/usr/local/python3，使用命令：

    mkdir /usr/local/python3 
建立一个空文件夹

然后解压压缩包，进入该目录，安装Python3

    tar -xvJf  Python-3.6.2.tar.xz
    cd Python-3.6.2
    ./configure --prefix=/usr/local/python3
    make && make install
最后创建软链接

    ln -s /usr/local/python3/bin/python3 /usr/bin/python3
    ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
	ln -s/usr/local/python3/bin/pip /usr/bin/pip
在命令行中输入python3测试

	这是两层压缩，外面是xz压缩方式，里层是tar压缩

所以可以分两步实现解压	
 
    $ xz -d node-v6.10.1-linux-x64.tar.xz
    $ tar -xvf node-v6.10.1-linux-x64.tar
	
	Centos 7 mysql
	yum install mariadb-server mariadb 
	yum install mariadb-devel
	
	mariadb数据库的相关命令是：

    systemctl start mariadb  #启动MariaDB
    
    systemctl stop mariadb  #停止MariaDB
    
    systemctl restart mariadb  #重启MariaDB
    
    systemctl enable mariadb  #设置开机启动
    
    所以先启动数据库
    
    [root@yl-web yl]# systemctl start mariadb
	
	还有一台一直没用上的23O，最近很流行NAT小鸡啊，搭了自带的 Proxmox ，自己开几个装着玩，

芬兰线路，富强和建站都太委屈了，

偶然在TG上看到说NAT还可以利用IPV6配合 CF 建站的，

马上各种查了怎么搞，研究了好半天，终于搞定了，

弄好后，简单搭了个宝塔，很多地方没有 IPV6 的要访问的话，必须搭配上 CF 了，

这样 CF 用 IPV6 回源 NAT小鸡，同时还提供 ipv4 和 ipv6 的访问

这样建站就没问题了，

NAT 鸡鸡目前还是有很多可玩性的，等 IPV6 普及之后，NAT 鸡鸡估计也就不会有太大存在的必要了

配上 CF 的 Railgun 的话连续访问的 TTFB 还可以再减短一些，有时间再搞一下，芬兰离回源的 CF 美国节点还是太远了，

如果是美国西海岸的 NAT 鸡配上 CF 还要再快一些

来各位大佬，求测个速，

http://de6.oldking.pl
http://de6.oldking.pl





参考资料
http://www.iytc.net/wordpress/?p=3199
http://www.hostloc.com/thread-436385-2-1.html
https://www.zmrbk.com/post-3245.html
https://www.lowendtalk.com/discussion/119741/help-with-ipv6-bridge-settings-debian-hetzner
分享到:  

Centos 7 开放查看端口 防火墙关闭打开
查看已经开放的端口：

firewall-cmd --list-ports
1
开启端口

firewall-cmd --zone=public --add-port=80/tcp --permanent
	
	开启 X11
	本地下载安装Putty
本地下载安装Xming

Putty是一个和Xshell，SecureCRT类似的SSH Client，但是与Xshell不同的是，
Putty和secureCRT支持X11 Forwarding功能，这里我们选择使用Putty。

Xming类似一个远程桌面展示工具，可以实时展示远程linux服务器GUI图形界面，方便我们在本地操作的一种X server。

Putty下载地址：http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
Xming下载地址：http://sourceforge.net/projects/xming/
在远程linux服务器上安装xauth

yum install xauth
linux服务器配置ssh支持X11 Forwarding

vim /etc/ssh/sshd_config
加上如下配置：X11Forwarding yes
ps：一般默认就是开启的则不用执行4,5步骤
重启sshd服务

service sshd restart


https://linux.cn/article-5645-1.html


1. links
Links是用C语言写的一个开源web浏览器，支持包括Linux、Windows、OS X和OS/2在内的所有主流平台。它提供了基于文本和图形界面两种版本。大多数标准的Linux发行版都默认包含了基于文本的版本。如果您的发行版中默认没有安装links，可以通过包管理工具进行安装。Elinks是links的一个衍生版本。

# apt-get install links
# yum install links

3. lynx
lynx是一个基于文本的web浏览器，使用GNU GPLv2协议发布，用ISO C编写。lynx是一个可高度配置的web浏览器，是许多系统管理员的救世主，有最悠久的web浏览器之称，并且至今仍然处在积极开发中。

通过下面的命令安装lynx。

# apt-get install lynx
# yum install lynx

last -x|grep reboot

Centos下安装和使用EPEL源

https://vpsyou.com/epel-repo/

我们在Centos下使用yum安装时往往找不到rpm的情况，官方的rpm repository提供的rpm包也不够丰富，很多时候需要自己编译很痛苦，而EPEL恰恰可以解决这两方面的问题。EPEL的全称叫 Extra Packages for Enterprise Linux 。EPEL是由 Fedora 社区打造，为 RHEL 及衍生发行版如 CentOS、Scientific Linux 等提供高质量软件包的项目。装上了 EPEL之后，就相当于添加了一个第三方源。
一、如果是Centos 7.x or RHEL 7.x：

cd  /tmp
wget -c http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo yum install epel-release-latest-7.noarch.rpm


在你忘记用 root 方式打开文件时的文件保存
这可能是一个在论坛中一直受欢迎的命令。每当你打开一个你没有写入权限的文件（比如系统配置文件）并做了一些修改，Vim 无法通过普通的 “:w” 命令来保存。

你不需要重新以 root 方式打开文件再进行修改，只需要运行：

:w !sudo tee %

比较两个文件的不同
你们中的大多数很可能都知道 vimdiff 命令，它可以使用分离模式打开 Vim 并比较两个文件的不同。语法如下：

$ vimdiff [文件1] [文件2]
但同样的结果也可以通过下面的 Vim 命令来获得：

:diffthis
首先在 Vim 中打开原始文件。然后使用分离模式带来第二个文件：

:vsp [文件2]
最后在第一个缓冲区里输入：

:diffthis
通过 Ctrl+w 来切换缓冲区并再次输入：

:diffthis
这样两个文件中不同的部分就会被高亮。

（译者注：可以直接在一个缓冲区里使用命令 :windo diffthis，而不用输入 :diffthis 两次）

要停止比较，使用：

:diffoff



