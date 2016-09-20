---
title: mysql快速拷贝数据库
date: 2016-09-09 14:12:33
tags: "mysql"
---
假设已经存在数据库db1，拷贝到新建的db2

1. 新建数据库db2
	
		create database db2 default charset utf8mb4;
		
2. 在shell控制台使用mysqldump命令

		mysqldump db1 -uroot -p123 --add-drop-table | mysql db2 -uroot -p123	
