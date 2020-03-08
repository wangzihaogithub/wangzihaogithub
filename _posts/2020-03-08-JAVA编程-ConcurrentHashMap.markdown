---
layout: post
title:  "JAVA编程-ConcurrentHashMap"
tags: JAVA编程
---

### 实现差异

**jdk1.7** 

1. 数组 + 数组 + 链表实现 (`数组 + HashMap`)

2. final Segment[] 会初始化Segment[],不初始化HashEntry[]


**jdk1.8** 

1. 数组 + 链表实现 (`HashMap`)

2. volatile Node[] 不初始化的数组


 ---
 
### java1.7的ConcurrentHashMap细节 (数组 + Map实现)

**1.内部关键字段**

    class Segment {
         private HashEntry[] entries = null;//我其实就是HashMap的实现
    }
    
    final Segment[] segments //让每次操作都落到不同的Map上,减少并发颗粒度
    
    
**2.临界区竞争点** 

    1.初始化某个段(Segment)时 entries[] = new HashEntry[];  
        方式: cas + lock 
    2.操作某个段(Segment)中的 entries时;   
        方式: 上锁 trylock重试失败大于64次就lock

    
**3.如何降低并发度** 

    1. Segment[].length越大,并发度越高, 并发级别参数(concurrencyLevel)控制着Segment[].length
    2. 操作某个Segment中的Map会出现竞争,则trylock + lock


 ---
 
### java1.8的ConcurrentHashMap细节 (数组 + 链表实现)

**1.知识前提**

        1. HashMap的结构 (数组 + 链表) 
                数组: Node[] table
                链表: Node = {key,value,next}
                
        2. Node的子类有 
                ForwardingNode(扩容期间临时用)
                ReservationNode(方法computeIfAbsent或compute时用.这个类的查询find()永远返回null)
                TreeBin,TreeNode (链表长度大于8时用)

        3. 查询请求是由table[index].find()方法处理的
    
**2.内部关键字段**
 
    volatile Node[] table = {key,value,next} //用来实现存储
    volatile Node[] nextTable = {key,value,next}//用来实现扩容期间的查询


**3.临界区竞争点** 

        1.put触发=初始化表时,     
            table[] = new Node[32]; 
            竞争点: cas + cas失败会Thread.yield直到成功
            时机: table等于null时
            
        2.put触发=存储数据时(初始化节点),
            table[i] = new Node; 
            竞争点: cas无线重试
            时机: table[i]等于null时
            
        2.put触发=存储数据时(拉链表),
            table[i].next = new Node; 
            竞争点: synchronized(Node)
            时机: hash落点一样时[index]
            
        3.put触发=树化时,
            table[i] = new TreeBin; 
            竞争点: synchronized(Node) 
            时机: table[i].next拉链大于8个的时候,会改为TreeBin
            
        4.put触发=扩容时,
            table[i] = new ForwardingNode; 
            竞争点: synchronized(Node)
            时机: 1. Node链表长度达到8，但table[].length却小于64时。
                 2. (当前size / 当前table[].length) > 负载因子(0.75)
                 
        5.clear触发=清空时,
            table[i] = null; 
            竞争点: synchronized(Node)
            时机: 方法调用后一定会锁

        5.merge触发=赋值时,
            table[i].next = new Node; 
            竞争点: synchronized(Node)
            时机: hash落点一样时[index]
            
        5.remove触发=删除时,
            table[i].next = pred.next; (移除链表引用)
            竞争点: synchronized(Node)
            时机: hash落点一样时[index]
                      
        6.其他增删改操作时
            竞争点: synchronized(Node)
            时机: hash落点一样时[index]
            
**4.树化后的结构如下**

        table[i] = new TreeBin(new TreeNode());
        
                    TreeNode(parent)
                    TreeNode(我)
        TreeNode(left)      TreeNode(right)
    
    
    
**5.扩容伪代码如下** 

         说明:   查询请求是由table[]的Node.find()方法处理的.
         扩容前: nextTable[index] = table[index];
                table[index] = new ForwardingNode(nextTable);
                ForwardingNode重写了find()方法, 如果遇到查询请求,会查nextTable表.
         扩容后: this.table = nextTable;
         
         
![cchashmap_resize1.jpg](../../../images/postimg/cchashmap_resize1.jpg)

![cchashmap_resize2.jpg](../../../images/postimg/cchashmap_resize2.jpg)

![cchashmap_resize3.jpg](../../../images/postimg/cchashmap_resize3.jpg)

![cchashmap_resize4.jpg](../../../images/postimg/cchashmap_resize4.jpg)
