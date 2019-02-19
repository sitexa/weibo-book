+++
title = "用SpringBoot + shiro 做SSO"
description = ""
tags = [
    "go",
    "golang",
    "hugo",
    "development",
]
date = "2019-02-19"
categories = [
    "Development",
    "golang",
]
menu = "main"
+++

### 一些参考文章

-   [spring boot 2.0 集成 shiro 和 pac4j cas单点登录](https://www.cnblogs.com/suiyueqiannian/p/9359597.html) 2018/8/29
-   [spring boot整合Shiro实现单点登录](https://blog.csdn.net/liuchuanhong1/article/details/76850181) 2017/8/17
-   [Springboot+shiro单点登录实现](https://blog.csdn.net/chenjiazhu/article/details/77851860) 2017/9/5
-   [spring boot配置单点登录](https://www.jianshu.com/p/600593b1f366) [github](https://github.com/willwu1984/springboot-cas-shiro)
2017/3/23
-   [Spring Boot 集成Shiro和CAS](https://blog.csdn.net/catoop/article/details/50534006) 2016/1/17
-   [在 Web 项目中应用 Apache Shiro](https://www.ibm.com/developerworks/cn/java/j-lo-shiro/index.html) 2013/1/31

### 进度说明

由于要实现单点登录，必须先做一个sso服务供其他应用使用。浏览了一些文章，比较接近的方案是上面的第一篇文章。其他文章对学习技术逻辑有帮助，
但不适用于我们的场景，或者版本比较旧，变化比较大，难于直接拿来用。


2018-12-22


