---
title: mysql_根据id集合排序
date: 2016-09-08 17:12:08
tags: "mysql"
---

select * from table where id IN (3,6,9,1,2,5,8,7) order by field(id,3,6,9,1,2,5,8,7); 
