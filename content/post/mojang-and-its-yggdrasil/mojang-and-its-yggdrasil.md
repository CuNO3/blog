---
title: 'Mojang and its Yggdrasil'
date: 2023-01-01T17:18:05+01:00
description: All the things about Yggdrasil API
slug: mojang-and-its-yggdrasil
date: 2022-03-06 00:00:00+0000
image: cover.png
categories:
    - Tech
tags:
    - Minecraft
draft: false
---

# Mojang and its Yggdrasil API

这篇文章是Mojang Yggdrasil API的入门教程。  
Yggdrasil是Mojang的（老）身份验证API，用于验证用户身份并获取用户信息。  
鉴于中文文档太少所以才有了本篇文章。

### Related Documents
[Authlib Injector Wiki](https://github.com/yushijinhun/authlib-injector/wiki)  
以下均为英文文档，英文不好的不要看了。  
[wiki.vg](https://wiki.vg/Authentication)  
[Mojang API Documentation](https://mojang-api-docs.netlify.app/)   
注：后面这个已失效，原文档fork位于[这里](yggdrasil-docs.netlify.app/),(还没有建成)

### 需要的知识
- HTTP协议
- JSON格式
- Java基础 （可选）（帮助你理解API里有些Java风格的东西）

### 开始：第一个问题：Yggdrasil，你为毛要了解它
如果你在学习和Minecraft有关的编程（Mod，Plugin，Server和其他的啥玩意），那么你迟早有一天会碰到Yggdrasil。

### 什么是Yggdrasil
我前面已经说过一遍：Yggdrasil是Mojang的（老）身份验证API，用于验证用户身份并获取用户信息。这个“老”是指之后还有一个巨硬收购后的微软账户登陆。它不是年龄最老的（去看wikivg你会知道还有1.6之前的另外一套系统），但是绝对是资格最老的。

### 它的流程？
一般来说是这样的:  
向服务器端点发送POST请求,带有载荷(根据请求不同可以是AccessToken, ClientToken, Username, Password或者其他信息)  
随后服务器端点返回一个JSON格式的响应,可能包含AccessToken,User等信息

### 标准的错误处理?
如果请求失败,服务器端点会返回一个HTTP状态码,并且在响应体中包含一个JSON格式的错误信息,包含错误代码和错误信息  
JSON格式如这样:
```json
{
    "error": "错误代码",
    "errorMessage": "错误信息",
    "cause": "可选的原因",
}
```

### 一些常见的错误代码
- ForbiddenOperationException: 服务器端点不支持该操作  
- IllegalArgumentException: 请求中包含了不合法的参数  
- UserMigratedException: 用户已经迁移到微软账户  
- UserNotFoundException: 用户不存在  
- InvalidCredentialsException: 用户名或密码错误  

### 什么是UUID?
UUID(Universally Unique Identifier),由ISO提出.  
在Minecraft里用于标明角色和实体.UUID对于每个角色来说是唯一的标识符.Minecraft里广泛应用了UUID用以判断交互.  
目前的UUID生成遵循[Version 4](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random))

### 什么是JWT
你可能会看到这个词,JWT(JSON Web Token),一种传递JSON令牌的编码格式,定义于[RFC 7519](https://tools.ietf.org/html/rfc7519),有关信息可以在[JWT.IO](https://jwt.io)查到.

### 剩余部分过几天继续更