---
layout: post
title:  "webflux-Mysql"
tags: webflux
---

### 支持Mono,FLux的客户端 (mysql, redis)
    
    使用示例 ： https://zhuanlan.zhihu.com/p/299069835
    
    
    https://spring.io/projects/spring-data-r2dbc
    <!-- Mysql https://mvnrepository.com/artifact/dev.miku/r2dbc-mysql  https://github.com/mirromutth/r2dbc-mysql-->
    <dependency>
        <groupId>org.springframework.data</groupId>
        <artifactId>spring-data-r2dbc</artifactId>
        <version>1.2.3</version>
    </dependency>
    <dependency>
        <groupId>dev.miku</groupId>
        <artifactId>r2dbc-mysql</artifactId>
        <version>0.8.2.RELEASE</version>
    </dependency>
    
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-redis-reactive</artifactId>
        <version>2.4.2</version>
    </dependency>
    
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-mongodb-reactive</artifactId>
        <version>2.4.2</version>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-webflux</artifactId>
        <version>2.4.2</version>
    </dependency>
    

### web协议

    1. 举例一次 http1.1/post请求
        
        Accpet线程(新链接轮询线程) 
            轮询操作系统返回的TCP链接句柄, 如果读到,则将这个链接传给IO线程.
            
        IO线程(输入输出线程)
            客户端 -> 发送request-header
            服务端 -> 判断content-length字段, 返回状态码100, Continue让客户端继续发送http-body
            客户端 -> 第一次发送 byte[缓冲区大小] 的数据
            客户端 -> 第二次发送 byte[缓冲区大小] 的数据
            客户端 -> 第三次发送 byte[缓冲区大小] 的数据
            客户端 -> 发送结束符号 \n\n
            
            业务线程(可选, 如果有阻塞代码, webflux没有业务线程, 因为宗旨是全流程无阻塞)
                服务端 -> 业务逻辑代码处理
            
            服务端 -> 返回response-header, 设置chunked发送或者content-length
            服务端 -> 第一次发送 byte[缓冲区大小] 的数据
            服务端 -> 第二次发送 byte[缓冲区大小] 的数据
            服务端 -> 第三次发送 byte[缓冲区大小] 的数据
            服务端 -> 发送结束符号 \n\n 或设置chunked长度
        
                
### 线程模型

    tomcat-IO模型. 
        accpet线程(接入新链接) -> IO线程 -> 业务线程 

    webflux-netty-IO模型. 
        accpet线程(接入新链接) -> IO线程
        