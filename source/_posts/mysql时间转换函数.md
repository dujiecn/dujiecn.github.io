---
title: mysql时间转换函数
date: 2016-09-23 08:48:36
tags: mysql
---


date_add(current_timestamp,interval - 1 month)

date_format(date,'%Y%m%d');

last_day('2007-03-01');

1 某一天的所在月的第一天：
	
	select date_add(date_add(last_day('2008-02-01'),interval 1 day),interval -1 month);
某一天的所在月的最后一天：
	
	select last_day('2008-02-01');