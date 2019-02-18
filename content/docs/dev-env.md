---
bookShowToc: false
---

# 开发环境

##  1，开发服务器：Linux/CentOS 7

IP地址：10.10.4.25

```
root/*
xnpeng/*
chenlm/*
zhangn/*
zengsd/*
public/123456
```

##  2，Java版本：jdk1.8

``` 
[xnpeng@localhost ~]$ java -version
openjdk version "1.8.0_191"
OpenJDK Runtime Environment (build 1.8.0_191-b12)
OpenJDK 64-Bit Server VM (build 25.191-b12, mixed mode)
```

##  3，数据库：MySQL, Oracle

```
Oracle: 10.10.4.18
MySQL: 10.10.4.25:3306 root/WEIbo123!@#
```

客户端工具：MySQLWorkbench。 请自官网下载：[https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/)

##  4，构建工具：Maven

请上官网下载Maven工具：[http://maven.apache.org/download.cgi](http://maven.apache.org/download.cgi)

```
Apache Maven 3.3.9 (bb52d8502b132ec0a5a3f4c09453c07478323dc5; 2015-11-11T00:41:47+08:00)
Maven home: /Users/open/Library/apache-maven-3.3.9
Java version: 1.8.0_192, vendor: Oracle Corporation
Java home: /Library/Java/JavaVirtualMachines/jdk1.8.0_192.jdk/Contents/Home/jre
Default locale: en_CN, platform encoding: UTF-8
OS name: "mac os x", version: "10.14.2", arch: "x86_64", family: "mac"
```

基本命令：

1.  mvn clean
2.  mvn package
3.  mvn install
4.  mvn jetty:run
5.  mvn tomcat:run

##  5，Maven仓库

```
http://10.10.4.25:8081
admin/admin123
```

##  6，版本控制：GitLab

```
http://10.10.4.25:9876
```

请上官网下载git客户端工具：[https://git-scm.com/](https://git-scm.com/)

请自己注册用户，并学习使用。上面建了一个练习项目go-test。

基本命令：

1.  git clone http://10.10.4.25:9876/root/go-test.git //克隆中央git仓库中的go-test项目
2.  git status //查看版本状态
3.  git add . //将修改后的文件加入git本地仓库
4.  git commit -m '修改README' //提交修改后的版本到本地仓库
5.  git push  //推送本地仓库中的版本到中央仓库

> .gitignore的重要性：为了保持仓库干净，一切无用的代码都不允许提交到版本库，包括本地环境文件，编译生成文件，过程文件。因此，必须在项目根目录上建立.gitignore文件，将需要排除的文件、目录写进去。

```.gitignore 
.idea/
.target/
**/target/
.out/
**/out/
.build/
**/build/
logs/
**/logs/
.svn/
**/.svn/
.project/
**/.project/
.settings/
**/.settings/
go-config/basedir/

*.iml
**/*.iml
**/*.gz
**/*.log
```

##  7，开发工具：Intellij IDEA

请上官网下载：[https://www.jetbrains.com/idea/](https://www.jetbrains.com/idea/)

注册码：
``` 
K71U8DBPNE-eyJsaWNlbnNlSWQiOiJLNzFVOERCUE5FIiwibGljZW5zZWVOYW1lIjoibGFuIHl1IiwiYXNzaWduZWVOYW1lIjoiIiwiYXNzaWduZWVFbWFpbCI6IiIsImxpY2Vuc2VSZXN0cmljdGlvbiI6IkZvciBlZHVjYXRpb25hbCB1c2Ugb25seSIsImNoZWNrQ29uY3VycmVudFVzZSI6ZmFsc2UsInByb2R1Y3RzIjpbeyJjb2RlIjoiSUkiLCJwYWlkVXBUbyI6IjIwMTktMDUtMDQifSx7ImNvZGUiOiJSUzAiLCJwYWlkVXBUbyI6IjIwMTktMDUtMDQifSx7ImNvZGUiOiJXUyIsInBhaWRVcFRvIjoiMjAxOS0wNS0wNCJ9LHsiY29kZSI6IlJEIiwicGFpZFVwVG8iOiIyMDE5LTA1LTA0In0seyJjb2RlIjoiUkMiLCJwYWlkVXBUbyI6IjIwMTktMDUtMDQifSx7ImNvZGUiOiJEQyIsInBhaWRVcFRvIjoiMjAxOS0wNS0wNCJ9LHsiY29kZSI6IkRCIiwicGFpZFVwVG8iOiIyMDE5LTA1LTA0In0seyJjb2RlIjoiUk0iLCJwYWlkVXBUbyI6IjIwMTktMDUtMDQifSx7ImNvZGUiOiJETSIsInBhaWRVcFRvIjoiMjAxOS0wNS0wNCJ9LHsiY29kZSI6IkFDIiwicGFpZFVwVG8iOiIyMDE5LTA1LTA0In0seyJjb2RlIjoiRFBOIiwicGFpZFVwVG8iOiIyMDE5LTA1LTA0In0seyJjb2RlIjoiR08iLCJwYWlkVXBUbyI6IjIwMTktMDUtMDQifSx7ImNvZGUiOiJQUyIsInBhaWRVcFRvIjoiMjAxOS0wNS0wNCJ9LHsiY29kZSI6IkNMIiwicGFpZFVwVG8iOiIyMDE5LTA1LTA0In0seyJjb2RlIjoiUEMiLCJwYWlkVXBUbyI6IjIwMTktMDUtMDQifSx7ImNvZGUiOiJSU1UiLCJwYWlkVXBUbyI6IjIwMTktMDUtMDQifV0sImhhc2giOiI4OTA4Mjg5LzAiLCJncmFjZVBlcmlvZERheXMiOjAsImF1dG9Qcm9sb25nYXRlZCI6ZmFsc2UsImlzQXV0b1Byb2xvbmdhdGVkIjpmYWxzZX0=-Owt3/+LdCpedvF0eQ8635yYt0+ZLtCfIHOKzSrx5hBtbKGYRPFDrdgQAK6lJjexl2emLBcUq729K1+ukY9Js0nx1NH09l9Rw4c7k9wUksLl6RWx7Hcdcma1AHolfSp79NynSMZzQQLFohNyjD+dXfXM5GYd2OTHya0zYjTNMmAJuuRsapJMP9F1z7UTpMpLMxS/JaCWdyX6qIs+funJdPF7bjzYAQBvtbz+6SANBgN36gG1B2xHhccTn6WE8vagwwSNuM70egpahcTktoHxI7uS1JGN9gKAr6nbp+8DbFz3a2wd+XoF3nSJb/d2f/6zJR8yJF8AOyb30kwg3zf5cWw==-MIIEPjCCAiagAwIBAgIBBTANBgkqhkiG9w0BAQsFADAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBMB4XDTE1MTEwMjA4MjE0OFoXDTE4MTEwMTA4MjE0OFowETEPMA0GA1UEAwwGcHJvZDN5MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxcQkq+zdxlR2mmRYBPzGbUNdMN6OaXiXzxIWtMEkrJMO/5oUfQJbLLuMSMK0QHFmaI37WShyxZcfRCidwXjot4zmNBKnlyHodDij/78TmVqFl8nOeD5+07B8VEaIu7c3E1N+e1doC6wht4I4+IEmtsPAdoaj5WCQVQbrI8KeT8M9VcBIWX7fD0fhexfg3ZRt0xqwMcXGNp3DdJHiO0rCdU+Itv7EmtnSVq9jBG1usMSFvMowR25mju2JcPFp1+I4ZI+FqgR8gyG8oiNDyNEoAbsR3lOpI7grUYSvkB/xVy/VoklPCK2h0f0GJxFjnye8NT1PAywoyl7RmiAVRE/EKwIDAQABo4GZMIGWMAkGA1UdEwQCMAAwHQYDVR0OBBYEFGEpG9oZGcfLMGNBkY7SgHiMGgTcMEgGA1UdIwRBMD+AFKOetkhnQhI2Qb1t4Lm0oFKLl/GzoRykGjAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBggkA0myxg7KDeeEwEwYDVR0lBAwwCgYIKwYBBQUHAwEwCwYDVR0PBAQDAgWgMA0GCSqGSIb3DQEBCwUAA4ICAQC9WZuYgQedSuOc5TOUSrRigMw4/+wuC5EtZBfvdl4HT/8vzMW/oUlIP4YCvA0XKyBaCJ2iX+ZCDKoPfiYXiaSiH+HxAPV6J79vvouxKrWg2XV6ShFtPLP+0gPdGq3x9R3+kJbmAm8w+FOdlWqAfJrLvpzMGNeDU14YGXiZ9bVzmIQbwrBA+c/F4tlK/DV07dsNExihqFoibnqDiVNTGombaU2dDup2gwKdL81ua8EIcGNExHe82kjF4zwfadHk3bQVvbfdAwxcDy4xBjs3L4raPLU3yenSzr/OEur1+jfOxnQSmEcMXKXgrAQ9U55gwjcOFKrgOxEdek/Sk1VfOjvS+nuM4eyEruFMfaZHzoQiuw4IqgGc45ohFH0UUyjYcuFxxDSU9lMCv8qdHKm+wnPRb0l9l5vXsCBDuhAGYD6ss+Ga+aDY6f/qXZuUCEUOH3QUNbbCUlviSz6+GiRnt1kA9N2Qachl+2yBfaqUqr8h7Z2gsx5LcIf5kYNsqJ0GavXTVyWh7PYiKX4bs354ZQLUwwa/cG++2+wNWP+HtBhVxMRNTdVhSm38AknZlD+PTAsWGu9GyLmhti2EnVwGybSD2Dxmhxk3IPCkhKAK+pl0eWYGZWG3tJ9mZ7SowcXLWDFAk0lRJnKGFMTggrWjV8GYpw5bq23VmIqqDLgkNzuoog==
```

或者自行上网获取：[http://idea.lanyus.com/](http://idea.lanyus.com/)

##  8，微服务体系：Spring Cloud v2

请上官网查看版本依赖：[http://spring.io/projects/spring-cloud](http://spring.io/projects/spring-cloud)

我们的项目使用最新发行版：```SpringCloud 2.1.1.RELEASE，SpringBoot Finchley.RELEASE```. 许多组件的版本需要精确匹配，不能随意更改。

##  9，前端技术栈： NodeJS v8.12.0 + Vue v2.5

请上官网下载安装：

NodeJS: [https://nodejs.org/en/](https://nodejs.org/en/)

VueJS: [https://cn.vuejs.org/](https://cn.vuejs.org/)

##  10, 前端UI框架：ElementUI

官网：[http://element-cn.eleme.io/#/zh-CN](http://element-cn.eleme.io/#/zh-CN)

##  11, 跨平台移动APP框架：Cordova, Flutter

官网： [https://cordova.apache.org/](https://cordova.apache.org/)

官网： [https://flutter.io/](https://flutter.io/)


