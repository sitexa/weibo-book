# 基础服务

## 1,基础服务项目: go-base

![](/images/base01.png)

多模块项目。go-base-common 公用组件；go-base-facade pojo组件；go-base-service 服务组件；go-spring-dependencies spring统一依赖组件。

## 2，go-base-common

公用组件，由各模块抽取出来，统一打包，统一引用。

## 3，go-base-facade

pojo 组件，供相关联模块引用。

## 4，go-base-service

基础服务组件。包括用户、组织机构等服务。

## 5，go-spring-dependencies

维护spring公共依赖，供其他模块继承。
