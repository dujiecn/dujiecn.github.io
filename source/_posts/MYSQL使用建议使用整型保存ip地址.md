---
title: MYSQL使用建议使用整型保存ip地址
date: 2016-11-25 16:21:46
tags: mysql
---

mysql中建议使用整型保存ip地址，通过函数转换

	set @ip = '192.168.1.110';
	select inet_aton(@ip);
	select inet_ntoa(inet_aton(@ip));