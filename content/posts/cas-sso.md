+++
title = "Springboot + cas 搭建认证中心"
description = ""
tags = [
    "go",
    "golang",
    "templates",
    "themes",
    "development",
]
date = "2019-02-19"
categories = [
    "Development",
    "golang",
]
menu = "main"
+++
参考资料：

-   [Springboot和Cas搭建和学习的案例，以前直接打war包的方式，放弃，直接使用springboot吧](https://gitee.com/yellowcong/springboot_cas)
-   [https://gitee.com/shuzheng/zheng](https://gitee.com/shuzheng/zheng) 基于Spring+SpringMVC+Mybatis分布式敏捷开发系统架构，提供整套公共微服务服务模块：集中权限管理（单点登录）、内容管理、支付中心、用户管理（支持第三方登录）、微信平台、存储系统、配置中心、日志分析、任务和通知等，支持服务治理、监控和追踪，努力为中小型企业打造全方位J2EE企业级开发解决方案。
-   [spring + shiro + cas 实现sso单点登录](https://www.cnblogs.com/coderhuang/p/5897444.html)
-   [Apereo CAS - Enterprise Single Sign On for all earthlings and beyond.](https://github.com/apereo/cas)
-   [Enterprise Single Sign-On for All](https://apereo.github.io/cas/5.3.x/index.html)
-   [CAS_SSO_Record](https://github.com/X-rapido/CAS_SSO_Record)

### 认证中心架构

![架构图](/images/cas_architecture.png)


### 安装caswar

-   [pandaAnthony:spring boot cas 服务端和spring security客户端搭建（一）](https://www.jianshu.com/p/0b3375b10860)

####    下载安装cas-overlay-template v5.3

下载地址： [https://github.com/apereo/cas-overlay-template](https://github.com/apereo/cas-overlay-template)

此版本将安装cas server 5.3.6。在本地编译生成，会下载相应的程序包并打包生成cas.war。

>避免使用最新版本的cas server和cas-overlay-template，因为新版要求jdk11。

####    生成SSL证书

1. 使用java自带keytool创建本地密钥库

密码：```changeit```

别名：```cas.server.com```

语法： ```keytool -genkey -alias cas.server.com -keyalg RSA -keystore casServer.keystore```

``` 
keytool -genkey -alias cas.server.com -keyalg RSA -keystore casServer.keystore
Enter keystore password:
Re-enter new password:
What is your first and last name?
  [Unknown]:  oscar peng
What is the name of your organizational unit?
  [Unknown]:  weibo-dev
What is the name of your organization?
  [Unknown]:  weibo
What is the name of your City or Locality?
  [Unknown]:  changsha
What is the name of your State or Province?
  [Unknown]:  hunan
What is the two-letter country code for this unit?
  [Unknown]:  zh
Is CN=oscar peng, OU=weibo-dev, O=weibo, L=changsha, ST=hunan, C=zh correct?
  [no]:  yes

Enter key password for <cas.server.com>
	(RETURN if same as keystore password):
```
在当前目录下生成了密钥库```casServer.keystore```。

2. 把密钥库导出成证书文件

语法： ```keytool -export -alias cas.server.com -keystore casServer.keystore -file casServer.crt -storepass changeit ```

``` 
keytool -export -alias cas.server.com -keystore casServer.keystore -file casServer.crt -storepass changit
Certificate stored in file <casServer.crt>
```
当前目录下将产生一个证书文件```casServer.crt ```。

3. 查看证书

语法： ``` 语法： keytool -printcert -file casServer.crt ```

``` 
keytool -printcert -file casServer.crt
Owner: CN=oscar peng, OU=weibo-dev, O=weibo, L=changsha, ST=hunan, C=zh
Issuer: CN=oscar peng, OU=weibo-dev, O=weibo, L=changsha, ST=hunan, C=zh
Serial number: 50285f9a
Valid from: Wed Dec 26 08:49:55 CST 2018 until: Tue Mar 26 08:49:55 CST 2019
Certificate fingerprints:
	 MD5:  9E:D7:4B:89:86:33:C4:35:EA:D6:92:16:23:65:59:E2
	 SHA1: B7:73:49:E3:0C:9A:F4:8C:D7:F6:C8:58:BA:29:BA:A7:DB:12:41:A5
	 SHA256: C8:26:1F:86:94:39:DE:98:59:B4:8B:3F:DC:34:E0:8B:1E:49:48:D2:A1:10:14:83:34:56:1D:09:E3:BE:17:E9
	 Signature algorithm name: SHA256withRSA
	 Version: 3

Extensions:

#1: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: 82 77 08 4D 55 BC 55 2E   53 BD 3E 81 39 A3 01 61  .w.MU.U.S.>.9..a
0010: A6 F0 23 D5                                        ..#.
]
]
```

4. 将创建过的证书导入到java证书库

语法： ```sudo keytool -import -keystore $JAVA_HOME/jre/lib/security/cacerts -file ~/casServer.crt -alias cas.server.com```

```
sudo keytool -import -keystore $JAVA_HOME/jre/lib/security/cacerts -file ~/casServer.crt -alias cas.server.com
Enter keystore password:
Owner: CN=oscar peng, OU=weibo-dev, O=weibo, L=changsha, ST=hunan, C=zh
Issuer: CN=oscar peng, OU=weibo-dev, O=weibo, L=changsha, ST=hunan, C=zh
Serial number: 50285f9a
Valid from: Wed Dec 26 08:49:55 CST 2018 until: Tue Mar 26 08:49:55 CST 2019
Certificate fingerprints:
	 MD5:  9E:D7:4B:89:86:33:C4:35:EA:D6:92:16:23:65:59:E2
	 SHA1: B7:73:49:E3:0C:9A:F4:8C:D7:F6:C8:58:BA:29:BA:A7:DB:12:41:A5
	 SHA256: C8:26:1F:86:94:39:DE:98:59:B4:8B:3F:DC:34:E0:8B:1E:49:48:D2:A1:10:14:83:34:56:1D:09:E3:BE:17:E9
	 Signature algorithm name: SHA256withRSA
	 Version: 3

Extensions:

#1: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: 82 77 08 4D 55 BC 55 2E   53 BD 3E 81 39 A3 01 61  .w.MU.U.S.>.9..a
0010: A6 F0 23 D5                                        ..#.
]
]

Trust this certificate? [no]:  yes
Certificate was added to keystore
```

> 注：java证书库的名字是```cacerts```，而不是```caserts```. java证书库的密码竟然是```changeit```.

5. 查看jdk证书内容

语法： ```keytool -list -v -keystore cacerts -alias cas.server.com```

``` 
keytool -list -v -keystore $JAVA_HOME/jre/lib/security/cacerts -alias cas.server.com
Enter keystore password:
Alias name: cas.server.com
Creation date: Dec 26, 2018
Entry type: trustedCertEntry

Owner: CN=oscar peng, OU=weibo-dev, O=weibo, L=changsha, ST=hunan, C=zh
Issuer: CN=oscar peng, OU=weibo-dev, O=weibo, L=changsha, ST=hunan, C=zh
Serial number: 50285f9a
Valid from: Wed Dec 26 08:49:55 CST 2018 until: Tue Mar 26 08:49:55 CST 2019
Certificate fingerprints:
	 MD5:  9E:D7:4B:89:86:33:C4:35:EA:D6:92:16:23:65:59:E2
	 SHA1: B7:73:49:E3:0C:9A:F4:8C:D7:F6:C8:58:BA:29:BA:A7:DB:12:41:A5
	 SHA256: C8:26:1F:86:94:39:DE:98:59:B4:8B:3F:DC:34:E0:8B:1E:49:48:D2:A1:10:14:83:34:56:1D:09:E3:BE:17:E9
	 Signature algorithm name: SHA256withRSA
	 Version: 3

Extensions:

#1: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: 82 77 08 4D 55 BC 55 2E   53 BD 3E 81 39 A3 01 61  .w.MU.U.S.>.9..a
0010: A6 F0 23 D5                                        ..#.
]
]
```

6. 根据 alias 别名删除JDK证书

>语法： ```sudo keytool -delete -alias cas.server.com -keystore cacerts```

7. 浏览器访问时查看证书

#### 在"下载安装cas-overlay-template v5.3"步骤中，修改配置

建```src/main/resources/```文件夹，将上次生成的目标文件夹中的```application.properties```文件复制到这里并进行修改，同时把生成的证书库```casServer.keystore```也复制到这里。

``` 
server.ssl.key-store=classpath:casServer.keystore
server.ssl.key-store-password=changeit
server.ssl.key-password=changeit
```

默认静态用户名和密码在底部：
``` 
cas.authn.accept.users=casuser::Mellon
```

生新编译生成cas.war,并启动：

``` 
java -jar target/cas.war
```

![images/cas-server.png](/images/cas-server.png)

> 修改hosts,增加一行：127.0.0.1    cas.server.com

打开浏览器，访问地址：```https://cas.server.com:8443/cas```

![](/images/cas-server-login.png)

用配置文件中的静态用户和密码登录：

![](/images/cas-server-login-success.png)

