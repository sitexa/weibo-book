---
author: "Michael Henderson"
date: 2019-02-19
linktitle: eureka server集群
menu:
  main:
    parent: tutorials
next: /tutorials/github-pages-blog
prev: /tutorials/automated-deployments
title: eureka server集群
weight: 10
---


启动多个eureka server,并两两注册。

(1) eureka server 1

``` 
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8762/eureka/,http://localhost:8763/eureka/
    register-with-eureka: false
spring:
  application:
    name: eureka
server:
  port: 8761
```

(2) eureka server 2

``` 
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/,http://localhost:8763/eureka/
    register-with-eureka: false
spring:
  application:
    name: eureka
server:
  port: 8762
```

(3) eureka server 3

``` 
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/,http://localhost:8762/eureka/
    register-with-eureka: false
spring:
  application:
    name: eureka
server:
  port: 8763
```

## 服务注册

每个应用服务同时往多个eureka server注册。

``` 
spring:
  application:
    name: org
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/,http://localhost:8762/eureka/,http://localhost:8763/eureka/
```
