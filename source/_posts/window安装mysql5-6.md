---
title: window安装mysql5.6
date: 2016-09-09 10:15:14
tags: "mysql"
---
1. 到mysql官网下载mysql-installer-community-5.6.25.0.msi

2. 点击安装--自定义安装--安装server
	
	不需要加入到service服务（后面通过命令安装）

3. 管理员身份打开命令提示符（cmd）
	进入到mysql的server安装目录的bin下
		
		cd C:\Program Files\MySQL\MySQL Server 5.6\bin
	关闭正在运行的mysql服务
	
		mysqladmin -uroot -p shutdown　
4. 把服务注册到服务列表里
	
		mysqld --install 

5. 启动服务
	
		net start mysql 

6. 设置密码
	
	做完上面的步骤可能导致原先安装时候设置的密码无效，这时候应该默认	没有密码，需要重新设置密码
		
		mysqladmin -u root password 123456
		
	修改密码：
	
		mysqladmin -u root -p123456 password 123456

7. 进入mysql
		
		mysql -uroot -p123456
