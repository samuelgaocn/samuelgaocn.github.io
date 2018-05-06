---
layout: post
category: "read"
title:  Linux  Do Server
tags: [Linux,Centos]
---

	更改SSH端口，采用密锁登陆
	
	138.68.26.67
	
	安装 Oneinstack
	注意 安装面板前，如果更改了SSH的端口，需要在选择ssh端口是打勾并正确设置端口，否则会因为安装脚本默认修改回22端口，导致SSH与火墙规则冲突导致无法SSH连接。
	
		
	wget -c http://mirrors.linuxeye.com/oneinstack-full.tar.gz && tar xzf oneinstack-full.tar.gz && ~/oneinstack/install.sh --nginx_option 1 --php_option 5 --phpcache_option 1 --php_extensions imagick --db_option 7 --dbinstallmethod 1 --dbrootpwd kg6xm8m4 --memcached  --iptables  --reboot 
	
	dojpg.samuelgao.review
	dobig.samuelgao.review
	dofrp.samuelgao.review
	dostat.samuelgao.review
	
	
	Nginx install dir:              /usr/local/nginx

    Database install dir:           /usr/local/mariadb
    Database data dir:              /data/mariadb
    Database user:                  root
    Database password:              kg6xm8m4
    
    PHP install dir:                /usr/local/php
    Opcache Control Panel URL:      http://138.68.26.67/ocp.php
    
    memcached install dir:          /usr/local/memcached
    
    Index URL:                      http://138.68.26.67/

	php5/7 大版本并存
	https://blog.linuxeye.cn/441.html
	
	确保这两个东西各自命名正确:
	配置文件
	/etc/init.d/php-fpm
	/etc/init.d/php7-fpm
	安装文件
	/usr/local/php
	/usr/local/php7
	设置php5.4、php7开机自启动：
    # CentOS:
    chkconfig --add php7-fpm
    chkconfig --add php-fpm
    chkconfig php7-fpm on
    chkconfig php-fpm on
	
    service php-fpm stop #后面需要再安装php，需要停止php
    mv /etc/init.d/php-fpm{,_bk} #后面需要再安装php会覆盖，备份启动脚本
	
	
	默认php5.4安装路径是/usr/local/php，如果再次安装会提示php已经安装，因此必须修改options.conf的php安装目录，将php7安装路径设置为/usr/local/php7，修改/root/oneinstack/options.conf：

    php_install_dir=/usr/local/php7
	
	再次执行./install.sh，选择Install php-7，其余均选择n，等待ing

    3. 修改php配置文件
    service php-fpm stop #停止php7启动脚本
    mv /etc/init.d/php-fpm /etc/init.d/php7-fpm  #重命名php7启动脚本
    mv /etc/init.d/php-fpm_bk /etc/init.d/php-fpm  #恢复php5.4启动脚本
	
	如果一开始就安装的PHP7， 请自行逻辑分析
	
	
	https://www.moerats.com/archives/611/
	
	LNMP操作命令：
    
    #操作前请在oneinstack目录下操作
    cd oneinstack
    #添加网站
    ./vhost.sh
    #删除网站
    ./vhost.sh del
    #添加其它组件
    ./addons.sh
    #网站备份
    ./backup_setup.sh
    #更新版本
    ./upgrade.sh
	
	systemctl start firewalld.service
    发现面板锁定了 防火墙	Failed to start firewalld.service: Unit is masked.
	systemctl unmask firewalld
	
	开80和443端口
	firewall-cmd --permanent --zone=public --add-port=80/tcp
	firewall-cmd --permanent --zone=public --add-port=443/tcp
	
	重启防火墙
	systemctl restart firewalld.service
	查看端口情况
	firewall-cmd --zone=public --list-all 
	
	1. 获取当前 SELinux 运行状态
    getenforce
    可能返回结果有三种：Enforcing、Permissive 和 Disabled。Disabled 代表 SELinux 被禁用，Permissive 代表仅记录安全警告但不阻止可疑行为，Enforcing 代表记录警告且阻止可疑行为。
    目前常见发行版中，RHEL 和 Fedora 默认设置为 Enforcing，其余的如 openSUSE 等为 Permissive。
    2. 改变 SELinux 运行状态
    setenforce [ Enforcing | Permissive | 1 | 0 ]
    该命令可以立刻改变 SELinux 运行状态，在 Enforcing 和 Permissive 之间切换，结果保持至关机。一个典型的用途是看看到底是不是 SELinux 导致某个服务或者程序无法运行。若是在 setenforce 0 之后服务或者程序依然无法运行，那么就可以肯定不是 SELinux 导致的。
    若是想要永久变更系统 SELinux 运行环境，可以通过更改配置文件 /etc/sysconfig/selinux 实现。注意当从 Disabled 切换到 Permissive 或者 Enforcing 模式后需要重启计算机并为整个文件系统重新创建安全标签(touch /.autorelabel && reboot)。
    3. SELinux 运行策略
    配置文件 /etc/sysconfig/selinux 还包含了 SELinux 运行策略的信息，通过改变变量 SELINUXTYPE 的值实现，该值有两种可能：targeted 代表仅针对预制的几种网络服务和访问请求使用 SELinux 保护，strict 代表所有网络服务和访问请求都要经过 SELinux。
	
	semanage port -a -t http_port_t -p tcp 888
	
	Total OneinStack Install Time: 11 minutes

    PHP install dir:                /usr/local/php
    Opcache Control Panel URL:      http://138.68.26.67/ocp.php

	
	https://www.91linux.org/458.html
	404问题原因
    伪静态没有配置正确，Chevereto 默认提供基于 Apache 环境的伪静态规则，如果服务器是 Nginx 则需要设置伪静态规则

    解决办法 在 server 下加入以下配置：


    location / {
        try_files $uri $uri/ /index.php?$query_string;
 
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
    官方推荐配置
    

    # Disable access to .ht* files
    location ~ /\.ht {
        deny all;
    }
   
    # Disable access to sensitive files in app path
    location ~ /(app|content|lib)/.*\.(po|php|lock|sql)$ {
      deny all;
    }
   
    # Disable log on not found images + image replacement
    location ~* (jpe?g|png|gif) {
        log_not_found off;
        error_page 404 /content/images/system/default/404.gif;
    }

    # Enable CORS header (needed for CDN)
    location ~ \.(ttf|ttc|otf|eot|woff|woff2|css|js)$ {
        add_header Access-Control-Allow-Origin "*";
    }

    # Force serve upload path as static content
    location ~ /images {}
   
    # Route dynamic request to index.php
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }  
	
    # Disable access to .ht* files
    location ~ /\.ht {
        deny all;
    }
   
    # Disable access to sensitive files in app path
    location ~ /(app|content|lib)/.*\.(po|php|lock|sql)$ {
      deny all;
    }
   
    # Disable log on not found images + image replacement
    location ~* (jpe?g|png|gif) {
        log_not_found off;
        error_page 404 /content/images/system/default/404.gif;
    }
 
    # Enable CORS header (needed for CDN)
    location ~ \.(ttf|ttc|otf|eot|woff|woff2|css|js)$ {
        add_header Access-Control-Allow-Origin "*";
    }
 
    # Force serve upload path as static content
    location ~ /images {}
   
    # Route dynamic request to index.php
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
	
	重启Nginx
	/etc/init.d/nginx restart
	
	安装Xfce
    安装额外yum源
    yum install epel-release

yum grouplist
yum groupinstall xfce
yum install vnc-server
vi /etc/sysconfig/vncservers
然后在内容中添加

VNCSERVERS="1:root"
VNCSERVERARGS[1]="-geometry 1024x768"

vncpasswd

vncserver

vi /root/.vnc/xstartup

#!/bin/sh
# Uncomment the following two lines for normal desktop:
unset SESSION_MANAGER
#exec /etc/X11/xinit/xinitrc
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &
#xterm -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop"&
#twm &
startxfce4 &


cp /lib/systemd/system/vncserver@.service /lib/systemd/system/vncserver.service  

firewall-cmd --permanent --add-service vnc-server
systemctl restart firewalld.service


vncviewer基本上不用配置；

vncserver的配置，创建一个新的配置文件，以开启1号窗口为例（也可以同时开启多个窗口，修改数字即可），方法如下：

cp /lib/systemd/system/vncserver@.service /lib/systemd/system/vncserver@:1.service

或者再增加一个窗口：

cp /lib/systemd/system/vncserver@.service /lib/systemd/system/vncserver@:2.service

编辑/lib/systemd/system/vncserver@:1.service,设置用户root相关参数,最终内容如下：

Description=Remote desktop service (VNC)
After=syslog.target network.target
[Service]
Type=forking
# Clean any existing files in /tmp/.X11-unix environment
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
ExecStart=/sbin/runuser -l root -c "/usr/bin/vncserver %i"
PIDFile=/root/.vnc/%H%i.pid
ExecStop=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
上述内容中最好设置为root用户，否则可能会看到以下报错：

三.应用

更新systemctl以使其生效；

systemctl daemon-reload 

设置vncserver的密码；

 vncpasswd root

按提示输入密码以及确认密码

启动该服务用来启用vnc的1号窗口；

systemctl start vncserver@:1.service  或者 vncserver :1

关闭1号窗口：

systemctl stop vncserver@:1.service   或者 vncserver -kill :1

设置为开机自动启动；

systemctl enable vncserver@:1.service

End.          

