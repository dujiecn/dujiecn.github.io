---
title: mybatis中if里面字符串比较
date: 2016-09-23 10:22:01
tags: mybatis
---

mybatis中如果使用如下字符串比较会报错：
	
	<choose>
		<when test="module == 'd'">
			topic_module_dynamic b
		</when>
	</choose>

改写成这样就ok了：
	
	<choose>
		<when test="module == 'd'.toString()">
			topic_module_dynamic b
		</when>
	</choose>

或者
	
	<choose>
		<when test='module == "d"'>
			topic_module_dynamic b
		</when>
	</choose>	