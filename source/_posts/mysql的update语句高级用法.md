---
title: mysql的update语句高级用法
date: 2016-09-08 17:07:25
tags: "mysql"
---
update tableName set column=2 where limit 条数;
 
replace into tableName(id,name)  values(1,'abc);

insert into tableName(id,name) on duplicate key update name = ?;