---
layout: post
title:  "webflux-Mysql"
tags: webflux
---

### 支持Mono,FLux的客户端 (mysql, redis)

- 使用示例 ：[https://zhuanlan.zhihu.com/p/299069835](https://zhuanlan.zhihu.com/p/299069835 "https://zhuanlan.zhihu.com/p/299069835")

- spring官网 ：[https://spring.io/projects/spring-data-r2dbc](https://spring.io/projects/spring-data-r2dbc "https://spring.io/projects/spring-data-r2dbc")

- maven依赖(可选) :


    
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
    
                
### web线程模型

    tomcat-IO模型. 
        accpet线程(接入新链接) -> IO线程 -> 业务线程 

    webflux-netty-IO模型. 
        accpet线程(接入新链接) -> IO线程
        
        
### web协议

    1. 举例 http1.1/post请求
        
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
        
        
    2. 举例 http2请求

          14:07:17.954 [EventLoop-1] ResourceLeakDetectorFactory - Loaded default ResourceLeakDetector: io.netty.util.ResourceLeakDetector@51e8fe8a
          14:07:18.005 [EventLoop-1] InsecureTrustManagerFactory - Accepting a server certificate: CN=www.maimai.cn, OU=PositiveSSL, OU=Domain Control Validated
          14:07:18.030 [EventLoop-1] SslHandler - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] HANDSHAKEN: protocol:TLSv1.3 cipher suite:TLS_CHACHA20_POLY1305_SHA256
          14:07:18.037 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] OUTBOUND SETTINGS: ack=false settings={MAX_HEADER_LIST_SIZE=8192}
          14:07:18.049 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND SETTINGS: ack=false settings={MAX_CONCURRENT_STREAMS=128, INITIAL_WINDOW_SIZE=65536, MAX_FRAME_SIZE=16777215}
          14:07:18.051 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] OUTBOUND SETTINGS: ack=true
          14:07:18.053 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND WINDOW_UPDATE: streamId=0 windowSizeIncrement=2147418112
          14:07:18.053 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND SETTINGS: ack=true
          14:07:18.084 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] OUTBOUND HEADERS: streamId=3 headers=DefaultHttp2Headers[:path: /sdk/company/is_admin, :method: GET, :scheme: https, :authority: maimai.cn:443, accept-encoding: gzip, accept-encoding: deflate] streamDependency=0 weight=16 exclusive=false padding=0 endStream=true
          14:07:18.090 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] OUTBOUND HEADERS: streamId=5 headers=DefaultHttp2Headers[:path: /sdk/company/is_admin, :method: GET, :scheme: https, :authority: maimai.cn:443, accept-encoding: gzip, accept-encoding: deflate] streamDependency=0 weight=16 exclusive=false padding=0 endStream=true
          14:07:18.091 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] OUTBOUND HEADERS: streamId=7 headers=DefaultHttp2Headers[:path: /sdk/company/is_admin, :method: GET, :scheme: https, :authority: maimai.cn:443, accept-encoding: gzip, accept-encoding: deflate] streamDependency=0 weight=16 exclusive=false padding=0 endStream=true
          14:07:18.091 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] OUTBOUND HEADERS: streamId=9 headers=DefaultHttp2Headers[:path: /sdk/company/is_admin, :method: GET, :scheme: https, :authority: maimai.cn:443, accept-encoding: gzip, accept-encoding: deflate] streamDependency=0 weight=16 exclusive=false padding=0 endStream=true
          14:07:18.091 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] OUTBOUND HEADERS: streamId=11 headers=DefaultHttp2Headers[:path: /sdk/company/is_admin, :method: GET, :scheme: https, :authority: maimai.cn:443, accept-encoding: gzip, accept-encoding: deflate] streamDependency=0 weight=16 exclusive=false padding=0 endStream=true
          14:07:18.106 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND HEADERS: streamId=5 headers=DefaultHttp2Headers[:status: 200, date: Mon, 08 Feb 2021 06:07:32 GMT, content-type: application/json; charset=utf-8, content-length: 2, set-cookie: seid=s1612764452590; Expires=Tue, 09-Feb-21 06:07:32 GMT; Max-Age=86400; Domain=maimai.cn; Path=/, set-cookie: guid=GRwEGxsYBBsdGAQbEx5WEhkZGxkcGlY=; Expires=Sat, 13-Feb-21 06:07:32 GMT; Max-Age=432000; Domain=maimai.cn; Path=/] padding=0 endStream=false
          14:07:18.112 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND DATA: streamId=5 padding=0 endStream=true length=2 bytes=7b7d
          14:07:18.114 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND HEADERS: streamId=3 headers=DefaultHttp2Headers[:status: 200, date: Mon, 08 Feb 2021 06:07:32 GMT, content-type: application/json; charset=utf-8, content-length: 2, set-cookie: seid=s1612764452590; Expires=Tue, 09-Feb-21 06:07:32 GMT; Max-Age=86400; Domain=maimai.cn; Path=/, set-cookie: guid=GRwEGxsYBBsdGAQbEx5WEhkZGxkcGlY=; Expires=Sat, 13-Feb-21 06:07:32 GMT; Max-Age=432000; Domain=maimai.cn; Path=/] padding=0 endStream=false
          14:07:18.114 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND DATA: streamId=3 padding=0 endStream=true length=2 bytes=7b7d
          14:07:18.115 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND HEADERS: streamId=9 headers=DefaultHttp2Headers[:status: 200, date: Mon, 08 Feb 2021 06:07:32 GMT, content-type: application/json; charset=utf-8, content-length: 2, set-cookie: seid=s1612764452590; Expires=Tue, 09-Feb-21 06:07:32 GMT; Max-Age=86400; Domain=maimai.cn; Path=/, set-cookie: guid=GRwEGxsYBBsdGAQbEx5WEhkZGxkcGlY=; Expires=Sat, 13-Feb-21 06:07:32 GMT; Max-Age=432000; Domain=maimai.cn; Path=/] padding=0 endStream=false
          14:07:18.115 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND DATA: streamId=9 padding=0 endStream=true length=2 bytes=7b7d
          14:07:18.116 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND HEADERS: streamId=7 headers=DefaultHttp2Headers[:status: 200, date: Mon, 08 Feb 2021 06:07:32 GMT, content-type: application/json; charset=utf-8, content-length: 2, set-cookie: seid=s1612764452590; Expires=Tue, 09-Feb-21 06:07:32 GMT; Max-Age=86400; Domain=maimai.cn; Path=/, set-cookie: guid=GRwEGxsYBBsdGAQbEx5WEhkZGxkcGlY=; Expires=Sat, 13-Feb-21 06:07:32 GMT; Max-Age=432000; Domain=maimai.cn; Path=/] padding=0 endStream=false
          14:07:18.116 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND DATA: streamId=7 padding=0 endStream=true length=2 bytes=7b7d
          14:07:18.117 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND HEADERS: streamId=11 headers=DefaultHttp2Headers[:status: 200, date: Mon, 08 Feb 2021 06:07:32 GMT, content-type: application/json; charset=utf-8, content-length: 2, set-cookie: seid=s1612764452590; Expires=Tue, 09-Feb-21 06:07:32 GMT; Max-Age=86400; Domain=maimai.cn; Path=/, set-cookie: guid=GRwEGxsYBBsdGAQbEx5WEhkZGxkcGlY=; Expires=Sat, 13-Feb-21 06:07:32 GMT; Max-Age=432000; Domain=maimai.cn; Path=/] padding=0 endStream=false
          14:07:18.117 [EventLoop-1] http2.Client - [id: 0x9c, L:/192.168.101.167:56380 - R:maimai.cn/106.75.23.100:443] INBOUND DATA: streamId=11 padding=0 endStream=true length=2 bytes=7b7d
