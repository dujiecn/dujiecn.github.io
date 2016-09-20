---
title: mongodb安装
date: 2016-09-08 16:45:13
tags: "mongodb"
---
### 安装mongodb
1. 到mongodb官网下载对应的包
2. 解压 tar zxvf mongodb.taz
3. 把解压出来的文件夹移动自己指定的目录
	mv mongodb ./develop-tools
4. 把mongod的命令加入环境变量
	vi ~/.bash_profile
	MONGODB_HOME=/Users/dujie/develop-tools/mongodb
	PATH=$PATH:$MONGO_HOME
5. 创建存放数据和日志的目录
	sudo mkdir /data/db
	sudo mkdir/data/log
	赋权限
	sudo chown -R dujie /data
6. 指定数据和日志目录
	cd /data
	mongod --dbpath db --logpath log/mongod.log --logappend --fork
7. 启动mongodb数据库
	mongod



=================================================================
### mongodb命令


1. 运行mongodb服务器
	mongod
2. 运行mongodb客户端
	mongo
3. 连上到数据库服务器进行一些操作
	查看当前所有的数据库：show dbs
	创建数据库：use mydb
	查看当前选择的数据库：db
	删除数据库：1. use mydb 2. db.dropDatabase()
	创建集合：db.createCollection(name,options)
		or  db.myCollection.insert({name:'dj'}) 

	删除集合：db.myCollection.drop()
	查询集合：db.myCollection.find()//.pretty()
		具体查询的where条件参照：http://www.yiibai.com/mongodb/mongodb_query_document.html
