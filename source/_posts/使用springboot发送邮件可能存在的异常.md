---
title: 使用springboot发送邮件可能存在的异常
date: 2016-10-14 13:11:44
tags: springboot
---
使用springboot 发送邮件的时候存在异常

1. `handshake_failure `异常
	
		Mail server connection failed; nested exception is javax.mail.MessagingException: Could not connect to SMTP host: smtp.qq.com, port: 465;
		nested exception is: javax.NET.ssl.SSLHandshakeException: Received fatal alert: handshake_failure. Failed messages: javax.mail. MessagingException: Could not connect to SMTP host: smtp.qq.com, port: 465;
		nested exception is: 	javax.net.ssl.SSLHandshakeException: Received fatal alert: handshake_failure
		
	这个问题在jdk1.8中出现，通过替换jdk1.8安装目录`/Library/Java/JavaVirtualMachines/jdk1.8.0_101.jdk/Contents/Home/jre/lib/security`包路径下的`US_export_policy.jar`和`US_export_policy.jar`两个文件来解决。使用jdk1.7版本同样目录下的这两个文件替换。或者到这里下载<http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html>

2. the trustAnchors parameter must be non-empty
	
	可能原因是使用的jdk1.7中`/Library/Java/JavaVirtualMachines/jdk1.8.0_101.jdk/Contents/Home/jre/lib/security`路径下缺少证书，由于我的电脑安装两个jdk版本，我的做法是拷贝1.8版本的`/Library/Java/JavaVirtualMachines/jdk1.8.0_101.jdk/Contents/Home/jre/lib/security`文件夹到1.7版本，或者到同事的电脑的拷贝。
