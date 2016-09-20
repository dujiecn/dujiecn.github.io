---
title: linux利用scp上传下载
date: 2016-09-08 17:18:39
tags: "linux"
---
### 上传
拷贝本地test到远程电脑/home/gydl目录下：

	scp -r test root@192.168.0.179:/home/gydl 
如果test是目录则需要加 “-r”	
### 下载
下载远程服务器/home／gydl/test文件到当前目录：
	
	scp -r root@192.168.0.179:/home/gydl .
