---
layout: post
category: "read"
title:  Linux  Golong
tags: [Linux,Centos]
---

	今天开了一个Google Cloud VM，设置了SSH，发现用户名不能设置成root。
	
	更新python 到3.6
	sudo apt-get install gcc automake autoconf libtool make
	
	wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tar.xz
	tar -Jxvf Python-3.6.4.tar.xz
	cd Python-3.6.4
	./configure
	make & make install
	
	安装pyenv
$ git clone git://github.com/yyuu/pyenv.git ~/.pyenv
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
$ echo 'eval "$(pyenv init -)"' >> ~/.bashrc
$ exec $SHELL -l

apt-get install libssl-dev
apt-get install make build-essential libssl-dev zlib1g-dev libbz2-dev libsqlite3-dev

apt-get install libdb5.3-dev libgdbm-dev libsqlite3-dev libssl-dev -y

sudo apt-get install python3-pipp'y
