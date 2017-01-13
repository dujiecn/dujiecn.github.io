---
title: python二分法计算平方根
date: 2017-01-13 17:02:44
tags: python
---

	#!/user/bin/python
	# coding=utf-8
	
	'''
	    
	'''
	
	
	def sqrt(v,t = 0.0001):
	    '''
	        二分法计算平方根     
	    '''
	    v = v + 0.0
	    s = 0
	    e = v / 2
	    r = 0
	    while((e - s) > (t * 2)):
	        r = (s + e) / 2
	        if(r * r > v): 
	            e = r
	        elif (r * r < v):
	            s = r
	        else:
	            return r 
	
	    return r
	
	print sqrt(9)
	print sqrt(10,0.1)
