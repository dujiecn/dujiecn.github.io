---
title: maven项目强制不热重启配置
date: 2016-09-10 11:02:42
tags: "maven"
---

1. 命令方式

		clean jetty:run -Djetty.port=8081 -Djetty.reload=manual
		
2. pom.xml中配置		
	
		<plugin>
				<groupId>org.mortbay.jetty</groupId>
				<artifactId>maven-jetty-plugin</artifactId>
				<version>6.1.26</version>
				<configuration>
					<reload>manual</reload>
					<connectors>
						<connector implementation="org.mortbay.jetty.nio.SelectChannelConnector">
							<port>8080</port>
							<maxIdleTime>30000</maxIdleTime>
						</connector>
					</connectors>
					<scanIntervalSeconds>3</scanIntervalSeconds>
					<webAppSourceDirectory>src/main/webapp</webAppSourceDirectory>
					<contextPath>/</contextPath>
				</configuration>
			</plugin>