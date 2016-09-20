layout: extjs
title: ExtJS中组件使用注意点
date: 2016-09-13 09:10:01
tags: extjs
---
使用ext组件的时候如果自定义一个公共的组件，最好使用如下方式：
		
		Ext.define('MyComponent',	{
			extend:'Ext.panel.Panel',
			initComponent:function() {
				var me = this;
				Ext.applyIf(me,{
					items:[
						...
					]
				});
				me.callParent(arguments);
			}
			
		});
		
如果使用子面量的形式，比如：
	
		Ext.define('MyComponent',{
			extend:'Ext.panel.Panel',
			items:[
				...
			]
		});
		
这种写法会导致组件里面有些store是单例，只会创建一次。则会出现组件的状态共用问题。