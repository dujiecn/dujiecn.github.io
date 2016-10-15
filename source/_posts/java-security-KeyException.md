---
title: java.security.KeyException
date: 2016-10-15 16:26:34
tags: java
---

在centos系统上用openjdk1.7， 用https请求微信api，报错如下
	
	Caused by: java.security.ProviderException: java.security.KeyException
    at sun.security.ec.ECKeyPairGenerator.generateKeyPair(ECKeyPairGenerator.java:146)
    at java.security.KeyPairGenerator$Delegate.generateKeyPair(KeyPairGenerator.java:704)
    at sun.security.ssl.ECDHCrypt.<init>(ECDHCrypt.java:78)
    at sun.security.ssl.ClientHandshaker.serverKeyExchange(ClientHandshaker.java:717)
    at sun.security.ssl.ClientHandshaker.processMessage(ClientHandshaker.java:278)
    at sun.security.ssl.Handshaker.processLoop(Handshaker.java:913)
    at sun.security.ssl.Handshaker.process_record(Handshaker.java:849)
    at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:1035)
    at sun.security.ssl.SSLSocketImpl.performInitialHandshake(SSLSocketImpl.java:1344)
    at sun.security.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1371)
    ... 52 more
    Caused by: java.security.KeyException
    at sun.security.ec.ECKeyPairGenerator.generateECKeyPair(Native Method)
    at sun.security.ec.ECKeyPairGenerator.generateKeyPair(ECKeyPairGenerator.java:126)
    ... 61 more
    

解决方案

升级nss
	
	sudo yum upgrade nss
