---
title: linux系统安装mysql步骤
date: 2016-09-08 17:04:52
tags: "mysql"
---
1. 下载mysql.tar.gz
2. tar -zxvf mysql.tar.gz
3. cp mysql /usr/local/mysql
4. cd /usr/local
5. groupadd mysql ,useradd mysql mysql
6. cd /usr/local/mysql
7. chown -R mysql:mysql ./
8. cp /support-files/my-default.cnf /etc/my.cnf
9. vim /etc/my.cnf 
	datadir = /usr/local/mysql/data
10. /usr/local/mysql/bin/mysqld --initialize --user=mysql
11. /usr/local/mysql/bin/mysqladmin -uroot -p旧密码 password 新密码
12. cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql 添加开机启动
13. service mysql start/stop
