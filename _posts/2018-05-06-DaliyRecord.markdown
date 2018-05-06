---
layout: post
category: "read"
title:  Linux  5月6号日常操作
tags: [Linux,Centos]
---
	
	https://sebastianblade.com/how-to-modify-ssh-port-in-centos7/
	
	更改 SSH 端口号
	修改sshd配置文件  # vi /etc/ssh/sshd_config 
	取消“#Port 22”前面的#号，另起一行新增Port 1522（可自定义端口），
	
	可知，SELinux没有给SSH开放10086端口，那么我们来添加该端口：
    semanage port -a -t ssh_port_t -p tcp 10086  

	添加端口 # firewall-cmd --zone=public --add-port=1522/tcp --permanent

	重新加载 # firewall-cmd --reload
	
	重启服务 # systemctl restart firewalld.service

	查看端口 # firewall-cmd --zone=public --list-all
	
	修改SELinux端口：

    检查SELinux是否启用 # sestatus -v |grep SELinu 
	
	yum installl firewall-cmd
	先查看防火墙是否开启了10086端口
	firewall-cmd --permanent --query-port=10086/tcp  
	
	完成后，再次查看
	semanage port -l|grep ssh  
	
	重新加载防火墙策略：
	firewall-cmd --reload  
	
	重启SSH服务和防火墙，最好也重启下服务器
	systemctl restart sshd  
    systemctl restart firewalld.service  
    shutdown -r now  
	
	关闭22端口
	semanage port -d -t ssh_port_t -p tcp 22
	ValueError: Port tcp/443 is defined in policy, cannot be deleted
	
	使用
	semanage port -m -t ssh_port_t -p tcp 22122
	
	
	firewall-cmd --zone=public --remove-port=22/tcp --permanent
	
	ssh 取消监听 22 端口，就已经配置好了，防火墙只不过是在 ssh 外多一层访问限制。如果要做的更好还可以将 22 端口的访问流量转向访问者本地：
	firewall-cmd --permanen --zone=public --add-forward-port=port=22:proto=tcp:toport=22:toaddr=127.0.0.1
	
	/opt/yilu/mservice -user_id 37736 -reg_device -dev_name py
	sudo pidof mservice | xargs kill -9 && service YiluzhuanqianSer start
	
	一、修改配置文件：
    /opt/yilu/work/workers.json
    
    --slow 10 线程数默认是2+3级缓存/2MB再减去10%，实测如果跑的比较多的其他业务，还需要再减少几个线程。
    cpu_priority > 0时， 赚钱优先； <0 时其他程序优先
    也就是slow后面的数字越大，占用的cpu核心数字越少。当cpu_priority的值小于0时，其他进程会优先使用cpu资源。
    
    二、重启服务
    对于ubuntu以及centos 7的用户
    
    service YiluzhuanqianSer restart
    对于centos 6的用户
    
    sudo pidof mservice | xargs kill -9 && nohup /opt/yilu/mservice > /dev/null 2>&1 &
	
	
	防范DDOS攻击脚本

    #防止DOS太多连接进来,可以允许外网网卡每个IP最多15个初始连接,超过的丢弃 
    iptables -A INPUT -i eth0 -p tcp --syn -m connlimit --connlimit-above 15 -j DROP 
    iptables -A INPUT -p tcp -m state --state ESTABLISHED,RELATED -j ACCEPT
    防范CC攻击
    
    (1)控制单个IP的最大并发连接数
    iptables -I INPUT -p tcp --dport 80 -m connlimit  --connlimit-above 50 -j REJECT #允许单个IP的最大连接数为 30
    
    (2)控制单个IP的某段时间的连接数
    iptables -A INPUT -p icmp -m limit --limit 1/m --limit-burst 10 -j REJECT
    iptables -A INPUT -p icmp -j DROP
	
	
	安装
	https://www.moerats.com/archives/545/
    1、安装thefuck
    运行以下命令：
    
    #CentOS系统
    yum -y update && yum -y install gcc 
    wget https://bootstrap.pypa.io/get-pip.py
    python get-pip.py && yum -y install python-devel
    sudo -H pip install thefuck
    
    #Ubuntu/Debian系统
    sudo apt update
    sudo apt install python3-dev python3-pip
    sudo pip3 install thefuck
    更多安装及使用方法查看Github项目地址：https://github.com/nvbn/thefuck。
	
	digitalocean 防火墙配置错误还可以上网站上通过网页版的console连接。。。
	
	