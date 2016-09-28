---
title: linux_远程免登录
date: 2016-09-08 16:48:06
tags: "linux"

---

A为本地主机(即用于控制其他主机的机器) ;B为远程主机(即被控制的机器Server), 假如ip为172.24.253.2 ;A和B的系统都是Linux;
 
### 在A上的命令:
	# ssh-keygen -t rsa (连续三次回车,即在本地生成了公钥和私钥,不设置密码)
	或者ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa 
	# ssh root@172.24.253.2 "mkdir .ssh;chmod 0700 .ssh" (需要输入密码， 注:必须将.ssh的权限设为700)
	# scp ~/.ssh/id_rsa.pub root@172.24.253.2:.ssh/id_rsa.pub (需要输入密码)
 
### 在B上的命令:
	# touch /root/.ssh/authorized_keys (如果已经存在这个文件, 跳过这条)
	# chmod 600 ~/.ssh/authorized_keys  (# 注意： 必须将~/.ssh/authorized_keys的权限改为600, 该文件用于保存ssh客户端生成的公钥，可以修改服务器的ssh服务端配置文件/etc/ssh/sshd_config来指定其他文件名）
	# cat /root/.ssh/id_rsa.pub  >> /root/.ssh/authorized_keys (将id_rsa.pub的内容追加到 authorized_keys 中, 注意不要用 > ，否则会清空原有的内容，使其他人无法使用原有的密钥登录)
 
### 回到A机器:
	# ssh root@172.24.253.2 (不需要密码, 登录成功)
 
假如在生成密钥对的时候指定了其他文件名（或者需要控制N台机器，此时你会生成多对密钥），则需要使用参数-i指定私钥文件

	# ssh root@172.24.253.2 -i /path/to/your_id_rsa	
scp也是一样，如:
	
	scp －i /root/.ssh/id_rsa  ./xxx 192.168.102.158:/home/wwy/bak
因为默认情况下ssh命令会使用~/.ssh/id_rsa作为私钥文件进行登录，如果需要连接多台服务器而又不希望每次使用ssh命令时指定私钥文件，可以在ssh的客户端全局配置文件/etc/ssh/ssh_config（或本地配置文件~/.ssh/config, 如果该文件不存在则建立一份）中增加如下配置

	IdentityFile /path/to/your_id_rsa
 
也可以为每个服务器指定一个Host配置:  
 
	Host 172.24.253.2
        IdentityFile /path/to/your_id_rsa
  
如果连接时出现如下的错误：
  Agent admitted failure to sign using the key
则使用 ssh-add 指令将私钥加进来（根据个人的密匙命名不同更改 id_rsa）

	ssh-add   ~/.ssh/id_rsa
 
如果能保护好自己的私钥, 这种方法相对在shell上输入密码, 要安全一些
 
### 深入一点:
 
从表面上简单的理解一下登录的过程,
首先 ssh-keygen -t rsa 命令生成了一个密钥和一个公钥, 而且密钥可以设置自己的密码
可以把密钥理解成一把钥匙, 公钥理解成这把钥匙对应的锁头,
把锁头(公钥)放到想要控制的server上, 锁住server, 只有拥有钥匙(密钥)的人, 才能打开锁头, 进入server并控制
而对于拥有这把钥匙的人, 必需得知道钥匙本身的密码,才能使用这把钥匙 (除非这把钥匙没设置密码), 这样就可以防止钥匙被了配了(私钥被人复制)
 
当然, 这种例子只是方便理解罢了,
拥有root密码的人当然是不会被锁住的, 而且不一定只有一把锁(公钥), 但如果任何一把锁, 被人用其对应的钥匙(私钥)打开了, server就可以被那个人控制了
所以说, 只要你曾经知道server的root密码, 并将有root身份的公钥放到上面, 就可以用这个公钥对应的私钥"打开" server, 再以root的身分登录, 即使现在root密码已经更改!
 
---------------------------------------------------------------------------------------
### 方法二、安装sshpass
	# sudo apt-get install sshpass
安装完成后使用sshpass允许你用 -p 参数指定明文密码，然后直接登录远程服务器。例如：
 
	# sshpass -p '你的密码' ssh 用户名@服务器ip地址
用 '-p' 指定了密码后，还需要在后面跟上标准的 ssh 连接命令。
 
Sshd的配置文件/etc/ssh/ssd_config
 
-------------------------------
ssh无密码验证的情况下向远程主机发送命令

	发送一条:
	ssh username@remote_server_ip your_command
	ssh username@remote_server_ip “your_command1;your_command2; your_command3”