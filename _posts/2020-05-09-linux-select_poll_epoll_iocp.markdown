---
layout: post
title:  "linux-select/poll/epoll/iocp"
tags: linux
---

下面对4种IO模式进行比较, 从select模式慢慢最终演进成iocp模式.

### IO模式之select

**函数原型如下**

    #include <sys/select.h>
    #include <sys/time.h>
    
    int select(int maxfdp1,fd_set *readset,fd_set *writeset,fd_set *exceptset,const struct timeval *timeout)
    返回值：就绪描述符的数目，超时返回0，出错返回-1
    
**函数参数介绍如下**

1.第一个参数maxfdp1指定待测试的描述字个数，
它的值是待测试的最大描述字加1（因此把该参数命名为maxfdp1），
描述字0、1、2...maxfdp1-1均将被测试。
因为文件描述符是从0开始的。

2.中间的三个参数readset、writeset和exceptset指定我们要让内核测试读、写和异常条件的描述字。
如果对某一个的条件不感兴趣，就可以把它设为空指针。
struct fd_set可以理解为一个集合，这个集合中存放的是文件描述符


**缺点**

poll和select同样存在一个缺点，

不论这些文件描述符是否就绪，大量文件描述符的数组被整体复制于用户态和内核的地址空间之间,

它的开销随着文件描述符数量的增加而线性增大。

 ---

### IO模式之poll

**函数原型如下**

    # include <poll.h>
    int poll ( struct pollfd * fds, unsigned int nfds, int timeout);

    struct pollfd {
        int fd;         /* 文件描述符 */
        short events;         /* 等待的事件 */
        short revents;       /* 实际发生了的事件 */
    }; 
    
poll的机制与select在本质上没有多大差别，但是poll没有最大文件描述符数量的限制。

**缺点**

poll和select同样存在一个缺点，

不论这些文件描述符是否就绪，大量文件描述符的数组被整体复制于用户态和内核的地址空间之间,

它的开销随着文件描述符数量的增加而线性增大。

 ---

### IO模式之epoll
    
    epoll是Linux内核为处理大批量文件描述符而作了改进的poll，
    是Linux下多路复用IO接口select/poll的增强版本，
    
    它能显著提高程序在大量并发连接中只有少量活跃的情况下的系统CPU利用率。
    
    另一点原因就是获取事件的时候，它无须遍历整个被侦听的描述符集，
    只要遍历那些被内核IO事件异步唤醒而加入Ready队列的描述符集合就行了。
    
    epoll除了提供select/poll那种IO事件的水平触发（Level Triggered）外，
    还提供了边缘触发（Edge Triggered），这就使得用户空间程序有可能缓存IO状态，
    减少epoll_wait/epoll_pwait的调用，提高应用程序效率。


**epoll 加了队列，用户可以对这个队列进行增删改查. 并且支持LE与ET两种使用方式**

即
1.epoll_create. 会返回队列句柄，
2.epoll_ctl 
    入参是 (
    1.队列句柄
    2.网络连接句柄
    3.事件类型(accept.read.write.clos)
    4.操作类型(增删改)

当产生硬件中断事件时，对这个队列进行增删改 (多个队列能在插入的时候提前分类,以减少查找次数).

这样就能在连接数大时，

减少内核句柄的遍历查找

与减少文件描述符的数组从内核态到用户态复制数量, 只复制用户需要查询的事件.

(注: select与poll每次都会把整个文件描述符数组复制到用户态内存里).

**缺点**

依旧依赖用户轮询, 只是在select与poll的基础上, 减少了内核内存与用户内存的复制

**优点**

内核微调


- LT（level triggered）是缺省的工作方式，

并且同时支持block和no-block socket.

在这种做法中，内核告诉你一个文件描述符是否就绪了，然后你可以对这个就绪的fd进行IO操作。

如果你不作任何操作，内核还是会继续通知你的，所以，这种模式编程出错误可能性要小一点。

传统的select/poll都是这种模型的代表。


- ET （edge-triggered）是高速工作方式，

只支持non-block socket。

在这种模式下，当描述符从未就绪变为就绪时，内核通过epoll告诉你。

然后它会假设你知道文件描述符已经就绪，并且不会再为那个文件描述符发送更多的就绪通知，

直到你做了某些操作导致那个文件描述符不再为就绪状态了（比如，你在发送，接收或者接收请求，或者发送接收的数据少于一定量时导致了一个EWOULDBLOCK 错误）。

但是请注意，如果一直不对这个fd作IO操作（从而导致它再次变成未就绪），内核不会发送更多的通知（only once），

不过在TCP协议中，ET模式的加速效用仍需要更多的benchmark确认。


- ET和LT的区别

LT事件不会丢弃，而是只要读buffer里面有数据可以让用户读，则不断的通知你。

而ET则只在事件发生之时通知。可以简单理解为LT是水平触发，而ET则为边缘触发。

LT模式只要有事件未处理就会触发，

ET则只在高低电平变换时（即状态从1到0或者0到1）触发。

 ---
 
### IO模式之iocp

中文名: 输入输出完成端口

外文名: Input/Output Completion Port

性质: 应用程序编程接口


- icop需要

**1.用于接受数据的回调方法**

**2.用于执行回调方法用的线程池 (当数据完成后)**

**3.设备列表** 

每当调用CreateIoCompletionPort函数时，操作系统会将该设备句柄添加到设备列表中；

每当调用CloseHandle关闭了某个设备句柄时，系统会将该设句柄从设备列表中删除

**4.队列**

IO完成队列
 
等待线程队列
 
释放线程队列

暂停线程队列
