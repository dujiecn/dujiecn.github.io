---
title: mysql语句中常见的技巧
date: 2016-09-13 12:43:10
tags: mysql
---

	update topic_config set value = cast(value as DECIMAL) + 1
使用 cast(value as DECIMAL) 把varchar类型的value值转成int类型然后进行计算

	insert into dictionary (value) values ((select * from (select ifnull(max(value),0) from dictionary where type = 2) tmp) + 1)		
	
insert语句中包含select语句，获取复合条件的最大值然后加1，常见于排序字段	


	insert into topic_module_subject_category
		(type,text,ptype)
		values
		( 
		<choose>
			<when test="ptype == 0">
				(select * from (select ifnull(max(type),100000) from topic_module_subject_category where ptype = #{ptype}) tmp) + 10000
			</when>
			<otherwise>
				(select * from (select ifnull(max(type),${ptype}) from topic_module_subject_category where ptype = #{ptype}) tmp) + 1
			</otherwise>
		</choose>
		,#{text},#{ptype})