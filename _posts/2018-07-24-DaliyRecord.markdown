---
layout: post
category: "read"
title:  Linux  GIF
tags: [Linux,GIF]
---

 
[![page.gif](https://i.loli.net/2018/07/24/5b568a75e8b27.gif)](https://i.loli.net/2018/07/24/5b568a75e8b27.gif)
[![page7.gif](https://i.loli.net/2018/07/24/5b568a764b872.gif)](https://i.loli.net/2018/07/24/5b568a764b872.gif)
[![page8.gif](https://i.loli.net/2018/07/24/5b568a76befd5.gif)](https://i.loli.net/2018/07/24/5b568a76befd5.gif)
[![page9.gif](https://i.loli.net/2018/07/24/5b568a76d4b5e.gif)](https://i.loli.net/2018/07/24/5b568a76d4b5e.gif)
[![paper1.gif](https://i.loli.net/2018/07/24/5b568a7803839.gif)](https://i.loli.net/2018/07/24/5b568a7803839.gif)
[![paper2.gif](https://i.loli.net/2018/07/24/5b568a780e39e.gif)](https://i.loli.net/2018/07/24/5b568a780e39e.gif)
[![page3.gif](https://i.loli.net/2018/07/24/5b568a7a4ad6a.gif)](https://i.loli.net/2018/07/24/5b568a7a4ad6a.gif)
[![page4.gif](https://i.loli.net/2018/07/24/5b568a7a78a9d.gif)](https://i.loli.net/2018/07/24/5b568a7a78a9d.gif)
[![page5.gif](https://i.loli.net/2018/07/24/5b568a7b0c80d.gif)](https://i.loli.net/2018/07/24/5b568a7b0c80d.gif)
[![page6.gif](https://i.loli.net/2018/07/24/5b568a7b4551f.gif)](https://i.loli.net/2018/07/24/5b568a7b4551f.gif)

bash <(curl -L -s https://install.direct/go.sh)


一、 查看所有进程占用的端口 
在开始-运行-cmd,输入：netstat –ano可以查看所有进程



二、查看占用指定端口的程序 

当你在用tomcat发布程序时，经常会遇到端口被占用的情况，我们想知道是哪个程序或进程占用了端口，可以用该命令 netstat –ano|findstr “指定端口号” 二、查看占用指定端口的程序 当你在用tomcat发布程序时，经常会遇到端口被占用的情况，我们想知道是哪个程序或进程占用了端口，可以用该命令 netstat –ano|findstr “指定端口号” 二、查看占用指定端口的程序 

当你在用tomcat发布程序时，经常会遇到端口被占用的情况，我们想知道是哪个程序或进程占用了端口，可以用该命令 netstat –ano|findstr “指定端口号” 
如:查询占用了8080端口的进程：netstat -ano|findstr "8080"



三、通过任务管理器杀死相关的进程
方法一：使用任务管理器杀死进程
打开任务管理器->查看->选择列->然后勾选PID选项，回到任务管理器上可以查看到对应的pid，然后结束进程
当然上面的方法有时候不好用，就是任务管理器中的进程比较多的时候，然后去找到对应的进程是很麻烦的，所以还有一种方法可以杀死进程的



方法二：使用命令杀死进程
1>首先找到进程号对应的进程名称
tasklist|findstr 进程号
如:tasklist|findstr 3112



2>然后根据进程名称杀死进程
taskkill /f /t /im 进程名称
如:taskkill /f /t /im /javaw.exe

