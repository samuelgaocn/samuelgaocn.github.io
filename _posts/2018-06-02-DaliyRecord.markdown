---
layout: post
category: "read"
title:  Linux  Golong
tags: [Linux,Centos]
---

	
Create the file /etc/apt/sources.list.d/pgdg.list, and add a line for the repository:
     deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main
Import the repository signing key, and update the package lists:
     wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
     sudo apt-get update
	 
	 pg_dump -h ec2-46-137-82-17.eu-west-1.compute.amazonaws.com -U fazfdkvfqnsvai -d dcpntpvaglb152 -p 5432 >tx.bak

	 
	 远程连接问题，默认情况下只允许本地连接，要想允许其它客户端连接，我们可以修改它的配置文件，这个文件的目录位于/etc/postgresql/9.5/main,这个目录下有两个文件：
  1：postgresql.conf,这个是服务器相关，里面有一个listen_address的地址，默认只监听本地，我们可以修改它。
  
  