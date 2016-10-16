---
title: docker中centos镜像启动systemctl异常
date: 2016-10-16 23:27:47
tags: docker
---

在docker的centos:latest镜像中运行systemctl命令`Failed to get D-Bus connection: Operation not permitted`错误，添加启动参数就能够解决

	docker run -itd \
	  --security-opt seccomp=unconfined \
  	  --cap-add=SYS_ADMIN \
	  -e "container=docker" \
	  -v /Users/dujie/Documents/Kitematic/centos/sys/fs/cgroup:/sys/fs/cgroup \
	  --name=centos \
	  centos:latest /usr/sbin/init