---
title: mysql_经纬度两点间的距离
date: 2016-09-08 17:13:35
tags: "mysql"
---
定义两个点的坐标，下面的方法返回两点理论距离，单位为KM

	set @lat1 = 31.9587090000;
	set @lng1 = 118.8255550000;
	set @lat2 = 31.9520910000;
	set @lng2 = 118.8127630000;            
	select 2 * asin(sqrt(pow(sin((@lat1 - @lat2) * PI() / 180.0 / 2), 2) + cos(@lat1 * PI() / 180.0) * cos(@lat2 * PI() /180.0) * pow(sin((@lng1 - @lng2) * PI() / 180.0 / 2), 2))) * 6378.137;
	
