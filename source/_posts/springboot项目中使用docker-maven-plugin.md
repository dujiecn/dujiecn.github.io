---
title: springboot项目中使用docker-maven-plugin
date: 2016-09-10 10:48:53
tags: [springboot,docker]
---

		<plugin>
				<groupId>com.spotify</groupId>
				<artifactId>docker-maven-plugin</artifactId>
				<version>0.4.12</version>
				<configuration>
					<imageName>${project.name}</imageName>
					<baseImage>java</baseImage>
					<entryPoint>["java", "-jar", "/${project.build.finalName}.jar"]</entryPoint>
					<resources>
						<resource>
							<targetPath>/</targetPath>
							<directory>${project.build.directory}</directory>
							<include>${project.build.finalName}.jar</include>
						</resource>
					</resources>
					<forceTags>true</forceTags>
				</configuration>
			</plugin>


