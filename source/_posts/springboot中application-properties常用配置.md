---
title: springboot中application.properties常用配置
date: 2016-09-10 10:54:38
tags: "springboot"
---

### 数据库
	spring.datasource.url=jdbc:mysql://localhost:3306/going_user?useUnicode=true&characterEncoding=UTF-8&rewriteBatchedStatements=true&autoReconnect=true&useSSL=false
	spring.datasource.username=root
	spring.datasource.password=123
	spring.datasource.driverClassName=com.mysql.jdbc.Driver

### 缓存
	spring.redis.host=localhost
	spring.redis.database=1
	spring.redis.password=123
	spring.redis.port=6379
	#spring.redis.pool.max-idle=8  
	#spring.redis.pool.min-idle=0  
	#spring.redis.pool.max-active=8  
	#spring.redis.pool.max-wait=-1

### 日志
	logging.file=var/log/user.log
	#logging.path=var/log
	logging.level.org.springframework.web=INFO
	logging.level.org.hibernate=WARN
	logging.level.org.springframework.data=DEBUG

### server
	server.port=8083
	server.tomcat.compression=on
	#server.tomcat.compression=4096
	server.tomcat.compressableMimeTypes=application/json,application/xml
	
### secruity
		security.user.name=admin
		security.user.password=admin	



