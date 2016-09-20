---
title: docker常用命令
date: 2016-09-08 14:01:53
tags: "docker"
---
### 运行容器
	docker run  -d -t --name centos -v ~/Documents/Kitematic/centos:/mnt centos:latest
镜像为：centos:latest
容器名：centos
映射本地目录到容器/mnt目录中：/usr/local/centos
### 导出镜像
	docker save centos:latest > centos.tar
### 导出镜像	
	docker load centos.tar
### 修改容器并提交新的镜像	
	docker commit -m 'update' -a 'walljay' centos walljay/centos:latest
-m 更新日志
-a 作者
centos 容器名
walljay/centos:lastest 镜像
### 设置容器时间
	cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
