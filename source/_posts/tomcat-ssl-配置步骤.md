---
title: tomcat_ssl_配置步骤
date: 2016-09-08 17:22:44
tags: "tomcat"
---

系统需求：

1、  Windows系统或Linux系统

2、  安装并配置JDK 1.6.0_13

3、  安装并配置Tomcat 6.0

 

### 第一步：为服务器生成证书

1. Windows系统

“运行”控制台，进入%JAVA_HOME%/bin目录
使用keytool为Tomcat生成证书，假定目标机器的域名是“localhost”，keystore文件存放在“D:\home\tomcat.keystore”，口令为“password”，使用如下命令生成：
 

keytool -genkey -v -alias tomcat -keyalg RSA -keystore D:\home\tomcat.keystore -validity 36500

 

(参数简要说明：“D:\home\tomcat.keystore”含义是将证书文件的保存路径，证书文件名称是tomcat.keystore ；“-validity 36500”含义是证书有效期，36500表示100年，默认值是90天)

在命令行填写必要参数：
A、输入keystore密码：此处需要输入大于6个字符的字符串

B、“您的名字与姓氏是什么？”这是必填项，并且必须是TOMCAT部署主机的域名或者IP[如：gbcom.com 或者 10.1.25.251]（就是你将来要在浏览器中输入的访问地址），否则浏览器会弹出警告窗口，提示用户证书与所在域不匹配。在本地做开发测试时，应填入“localhost”

C、“你的组织单位名称是什么？”、“您的组织名称是什么？”、“您所在城市或区域名称是什么？”、“您所在的州或者省份名称是什么？”、“该单位的两字母国家代码是什么？”可以按照需要填写也可以不填写直接回车，在系统询问“正确吗？”时，对照输入信息，如果符合要求则使用键盘输入字母“y”，否则输入“n”重新填写上面的信息

D、输入<tomcat>的主密码，这项较为重要，会在tomcat配置文件中使用，建议输入与keystore的密码一致，设置其它密码也可以

完成上述输入后，直接回车则在你在第二步中定义的位置找到生成的文件
2. Linux系统

“运行”控制台，进入%JAVA_HOME%/bin目录
使用如下命令生成：
 

keytool -genkey -alias tomcat -keyalg RSA -keystore ./tomcat.keystore -validity 36500

(参数简要说明：“/etc/tomcat.keystore”含义是将证书文件保存在路径/usr/local/ac/web/下，证书文件名称是tomcat.keystore ；“-validity 36500”含义是证书有效期，36500表示100年，默认值是90天)

在命令行填写必要参数：
A、Enter keystore password：此处需要输入大于6个字符的字符串

B、“What is your first and last name?”这是必填项，并且必须是TOMCAT部署主机的域名或者IP[如：gbcom.com 或者 10.1.25.251]，就是你将来要在浏览器中输入的访问地址

C、“What is the name of your organizational unit?”、“What is the name of your organization?”、“What is the name of your City or Locality?”、“What is the name of your State or Province?”、“What is the two-letter country code for this unit?”可以按照需要填写也可以不填写直接回车，在系统询问“correct?”时，对照输入信息，如果符合要求则使用键盘输入字母“y”，否则输入“n”重新填写上面的信息

D、Enter key password for <tomcat>，这项较为重要，会在tomcat配置文件中使用，建议输入与keystore的密码一致，设置其它密码也可以

完成上述输入后，直接回车则在你在第二步中定义的位置找到生成的文件
 

### 第二步：为客户端生成证书

 

为浏览器生成证书，以便让服务器来验证它。为了能将证书顺利导入至IE和Firefox，证书格式应该是PKCS12，因此，使用如下命令生成：
 

keytool -genkey -v -alias client -keyalg RSA -storetype PKCS12 -keystore ./client.p12

 

对应的证书库存放在“D:\home\mykey.p12”，客户端的CN可以是任意值。双击mykey.p12文件，即可将证书导入至浏览器（客户端）。

 

### 第三步：让服务器信任客户端证书

 

由于是双向SSL认证，服务器必须要信任客户端证书，因此，必须把客户端证书添加为服务器的信任认证。由于不能直接将PKCS12格式的证书库导入，必须先把客户端证书导出为一个单独的CER文件，使用如下命令：
 

keytool -export -alias client -keystore ./client.p12 -storetype PKCS12 -storepass password -rfc -file ./client.cer

 

通过以上命令，客户端证书就被我们导出到“D:\home\mykey.cer”文件了。下一步，是将该文件导入到服务器的证书库，添加为一个信任证书：
 

keytool -import -v -file ./client.cer -keystore D:\home\tomcat.keystore

 

通过list命令查看服务器的证书库，可以看到两个证书，一个是服务器证书，一个是受信任的客户端证书：
 

keytool -list -v -storepass password -keystore D:\home\tomcat.keystore

 

### 第四步：让客户端信任服务器证书

 

由于是双向SSL认证，客户端也要验证服务器证书，因此，必须把服务器证书添加到浏览的“受信任的根证书颁发机构”。由于不能直接将keystore格式的证书库导入，必须先把服务器证书导出为一个单独的CER文件，使用如下命令：
 

keytool -keystore ./tomcat.keystore -export -alias tomcat -file ./tomcat.cer

 

 

通过以上命令，服务器证书就被我们导出到“D:\home\tomcat.cer”文件了。双击tomcat.cer文件，按照提示安装证书，将证书填入到“受信任的根证书颁发机构”。
第四步：配置Tomcat服务器

 

打开Tomcat根目录下的/conf/server.xml，找到如下配置段，修改如下：

 

<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
SSLEnabled="true" maxThreads="150" scheme="https"
secure="true" clientAuth="true" sslProtocol="TLS"
keystoreFile="D:\\home\\test.keystore" keystorePass="123456"
truststoreFile="D:\\home\\test.keystore" truststorePass="123456" />

属性说明：

clientAuth:设置是否双向验证，默认为false，设置为true代表双向验证
keystoreFile:服务器证书文件路径
keystorePass:服务器证书密码
truststoreFile:用来验证客户端证书的根证书，此例中就是服务器证书
truststorePass:根证书密码
### 第五步：测试

 

在浏览器中输入:https://localhost:8443/，会弹出选择客户端证书界面，点击“确定”，会进入tomcat主页，地址栏后会有“锁”图标，表示本次会话已经通过HTTPS双向验证，接下来的会话过程中所传输的信息都已经过SSL信息加密。


注意事项：貌似导入证书的时候，最好导入到“个人”那一栏里面，貌似客户端的用户名不填写也是可以的，或者随便填写。

http://licg1234.blog.163.com/blog/static/13908233320121165356868/ 


=====================================================================================================
keytool -genkey -v -alias tomcat -keyalg RSA -keystore ./tomcat.keystore -validity 36500
keytool -genkey -v -alias client -keyalg RSA -storetype PKCS12 -keystore ./client.p12 -validity 36500
keytool -export -alias client -keystore ./client.p12 -storetype PKCS12 -storepass 123456 -rfc -file ./client.cer
keytool -import -v -alias client -file ./client.cer -keystore ./tomcat.keystore -storepass 123456
keytool -list -v -storepass 123456 -keystore ./tomcat.keystore
keytool -keystore ./tomcat.keystore -export -alias tomcat -file ./tomcat.cer -storepass 123456

<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
SSLEnabled="true" maxThreads="150" scheme="https"
secure="true" clientAuth="true" sslProtocol="TLS"
keystoreFile="D:\\home\\test.keystore" keystorePass="123456"
truststoreFile="D:\\home\\test.keystore" truststorePass="123456" />






keytool -genkeypair -alias "tomcat" -keyalg "RSA" -keystore "./tomcat.keystore"
<Connector port="8443" 
					protocol="org.apache.coyote.http11.Http11Protocol"
               maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
               clientAuth="false" sslProtocol="TLS"
	       keystoreFile="/usr/local/tomcat/tomcat.keystore" 
	       keystorePass="123456" 
		ciphers="TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA, TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA, TLS_ECDHE_RSA_WITH_RC4_128_SHA,TLS_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_128_CBC_SHA, TLS_RSA_WITH_AES_256_CBC_SHA256,TLS_RSA_WITH_AES_256_CBC_SHA,SSL_RSA_WITH_RC4_128_SHA" />
