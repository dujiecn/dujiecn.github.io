---
title: springboot打包不进去第三方jar的问题
date: 2016-12-20 10:05:00
tags:
---
在springboot maven构建的项目中，可能需要用到第三方的jar，这时候项目eclipse运行可能是没有问题，但是打包成可执行jar包的时候第三方jar包打不进去。解决方法如下：
1.创建目录`src/main/webapp/WEB-INF/lib`,把第三方的jar包放到该目录下
2.pom.xml引用：
	
	<dependency>
		<groupId>com.yunpian.sdk</groupId>
		<artifactId>yunpian-java-sdk</artifactId>
		<version>12</version>
		<scope>system</scope>
		<systemPath>${project.basedir}/src/main/webapp/WEB-INF/lib/yunpian-java-sdk.jar</systemPath>
	</dependency>
3.配置打包资源：
	
	<resources>
		<resource>
			<directory>${project.basedir}/src/main/resources</directory>
			<filtering>true</filtering>
		</resource>
		<resource>
			<directory>${project.basedir}/src/main/webapp/WEB-INF/lib</directory>
			<targetPath>BOOT-INF/lib/</targetPath>
			<includes>
				<include>**/*.jar</include>
			</includes>
		</resource>
	</resources>
	
这样就可以了。

局部完整的pom.xml配置如下：
	
	<dependencies>
		<dependency>
				<groupId>com.yunpian.sdk</groupId>
				<artifactId>yunpian-java-sdk</artifactId>
				<version>12</version>
				<scope>system</scope>
				<systemPath>${project.basedir}/src/main/webapp/WEB-INF/lib/yunpian-java-sdk.jar</systemPath>
		</dependency>
	</dependencies>
	
	
	<build>
		<resources>
			<resource>
				<directory>${project.basedir}/src/main/resources</directory>
				<filtering>true</filtering>
			</resource>
			<resource>
				<directory>${project.basedir}/src/main/webapp/WEB-INF/lib</directory>
				<targetPath>BOOT-INF/lib/</targetPath>
				<includes>
					<include>**/*.jar</include>
				</includes>
			</resource>
		</resources>

		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
					<encoding>UTF-8</encoding>
				</configuration>
			</plugin>

			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<configuration>
					<mainClass>com.helper.server.Application</mainClass>
				</configuration>
				<executions>
					<execution>
						<goals>
							<goal>repackage</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
	
	
	
	