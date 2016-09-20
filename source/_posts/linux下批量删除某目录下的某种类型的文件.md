---
title: linux下批量删除某目录下的某种类型的文件
date: 2016-09-09 08:51:22
tags: "linux"
---

批量删除当前目录下的名字是_md后缀的任何格式的文件	

	find . -name "*_md.*" -exec rm -rf {} \;

