---
layout: post
category: "read"
title:  Linux  Golong
tags: [Linux,Debian]
---


fdisk /dev/vda
n
p
q



格式化新分区的时候，报错，提示下面的错误，没有这个文件或目录。

 解决方法：执行partprobe 命令
partprobe包含在parted的rpm软件包中。
partprobe可以修改kernel中分区表，使kernel重新读取分区表。 
因此，使用该命令就可以创建分区并且在不重新启动机器的情况下系统能够识别这些分区。

reboot


接下来，格式化分区为XFS，使用mkfs.xfs命令。如果已有其他文件系统创建在此分区，必须加上"-f"参数来覆盖它。

mkfs.xfs -f /dev/vda3 

mount -t xfs /dev/vda3 /git

chown -R git:git computerback.git/
git init --bare computerbackup.git

git clone

git init
git add .
git commit -m "start"
git remote add file git@192.168.1.113:/home/weimenglang/git/file.git
