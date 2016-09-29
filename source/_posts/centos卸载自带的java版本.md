---
title: centos卸载自带的java版本
date: 2016-09-29 11:05:36
tags:
---
hadoop里面使用到jps命令，centos7 自带java环境，但是没有jps命令，需要自行安装：
	
	yum search java-1.8.0
	yum install -y java-1.8.0-openjdk-devel.x86_64

安装完成就会有jps命令			
		