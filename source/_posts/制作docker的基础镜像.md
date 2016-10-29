---
title: 基于centos制作docker的基础镜像
date: 2016-10-16 22:56:37
tags: docker
---

利用Dockerfile
	
	FROM centos:latest
	MAINTAINER walljay <760813193@qq.com>
	RUN yum -y update
	RUN yum -y install sudo \
			&& yum -y install net-tools \
			&& yum -y install openssh-server \
			&& yum -y install openssh-clients \
			&& yum -y install vim \
			&& yum -y install git \
			&& yum -y install java-1.8.0-openjdk-devel
	# RUN curl -sSL https://get.docker.com/ | sh

	ENV container docker
	VOLUME ["/sys/fs/cgroup"]
	CMD ["/usr/sbin/init"]
	
包含基本的java vim ssh net,git等工具，后续添加必要的工具

生成镜像的步骤：
	
	mkdir -p test
	cd test
	vim Dockerfile

把上面的内容复制到Dockerfile文件中并保存,然后在Dockerfile所在的目录下运行命令：
	
	docker build -t walljay/centos:devel .

-t 是标记tag参数，换成自己的，格式为[仓库名:版本],注意后面的“.”不能少，这个是表示Dockerfile所在的目录

启动centos容器：
	
	docker run -itd walljay/centos:devel