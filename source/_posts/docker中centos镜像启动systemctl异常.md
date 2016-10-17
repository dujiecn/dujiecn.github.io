---
title: docker中centos容器执行systemctl命令异常
date: 2016-10-16 23:27:47
tags: ["docker","centos"]
---

在docker的centos:latest镜像中运行systemctl命令`Failed to get D-Bus connection: Operation not permitted`错误，添加启动参数就能够解决

	docker run -d -i -t \
		--privileged \
  		--cap-add SYS_ADMIN \
	  	-e container=docker \
	  	-v /sys/fs/cgroup:/sys/fs/cgroup \
	  	centos:latest /usr/sbin/init



