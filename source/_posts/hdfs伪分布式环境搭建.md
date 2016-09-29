---
title: hdfs伪分布式环境搭建
date: 2016-09-29 13:50:14
tags: hadoop
---
本地环境是mac
### 安装虚拟机，设置基本环境
1. 安装vm虚拟机，并安装centos7系统，拷贝多个节点。变成node1,node2,node3
2. 设置所有节点的自定义IP，保证在同一个网段
	DNS:172.16.153.2

3. 关闭所有节点的防火墙
		
		systemctl stop firewalld
		
4. 设置免登录
		
		ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa && cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
	把本地的.ssh/id_rsa.pub 拷贝到需要控制的节点的~/.ssh/authorized_keys文件中
5. 修改本地环境的/etc/hosts
	
		sudo vim /etc/hosts
		172.16.153.10    node1
		172.16.153.20    node2
		172.16.153.30    node3

### 安装HDSF
假设node1是namenode，node2和node3是datanode，secondarynode在node2上面；

#### 设置node1
解压hadoop-1.2.1到/home/hadoop-1.2，cd到/home/hadoop-1.2目录下；	
	
1. 设置core-site.xml内容(配置查考`docs/core-default.html`)
	
		vim conf/core-site.xml
		
		<configuration>
	     <property>
	         <name>fs.default.name</name>
	         <value>hdfs://node1:9000</value>
	     </property>
	     <property>
	         <name>hadoop.tmp.dir</name>
	         <value>/opt/hadoop-1.2</value>
	     </property>
		</configuration>

	`fs.default.name`属性设置namenode；
	`hadoop.tmp.dir`设置临时文件存放位置，默认是在`/tmp`下面，	这个目录重启之后数据就没有咯。所以需要修改。

2. 设置hdfs-site.xml(配置查考`docs/hdfs-default.html`)
	
		vim conf/hdfs-site.xml
		
		<configuration>
			<property>
		         <name>dfs.replication</name>
		         <value>2</value>
		     </property>
		</configuration>
	
	`dfs.replication`设置datanode节点个数，默认是3，这里我们是datanode是node2和node3，所以设置为2。
	
3. 设置datanode
	
		vim conf/slaves
		
		node2
		node3
4. 设置secondarynode,这里是设置在node2上
	
		vim conf/master
		
		node2			
		
5. 设置	JAVA_HOME变量
	
		vim conf/hadoop-env.sh
		export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.102-1.b14.el7_2.x86_64/jre
	
6. 设置datanode免密码登录	
	这里我需要在namenode(node1)统一启动，所以我需要从node1到node2，node3免密码登录
		
		ssh root@node2
		ssh root@node3
	
	这两个操作都是免密码登录的。

至此，namenode设置完成了。

最后需要拷贝一样的hadoop环境到node2和node3
	
	scp /home/hadoop-1.2 root@node2:/home/
	scp /home/hadoop-1.2 root@node3:/home/
	
	
注意点：

***保证hadoop的包环境完全一致***

***设置免密码登录***

***设置JAVA_HOME***

***关闭防火墙***

在本地通过浏览器访问:http://node1:50070就能看到成果了。

	
		
		
			


	
	
