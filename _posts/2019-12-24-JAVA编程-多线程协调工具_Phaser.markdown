---
layout: post
title:  "JAVA编程-多线程协调工具_Phaser"
tags: JAVA编程
---

###  目录
    
   1.Phaser是一个更强大的、更复杂的同步辅助类
    
   2.内部维护的数据
   
   3.API
    
   4.继承
    
   5.状态说明：只要不是终止状态下，就可以动态的把线程注册到phaser中。


### 1.Phaser是一个更强大的、更复杂的同步辅助类，可以代替CyclicBarrier CountDownLatch的功能，但是比他们更强大。 
        
Phaser类机制是在每一步结束的位置对线程进行同步，当所有的线程都完成了这一步，才能进行下一步。 
        当我们有并发任务并且需要分解成几步执行的时候，这种机制就非常适合。 
        CyclicBarrier CountDownLatch 只能在构造时指定参与量，而phaser可以动态的增减参与量。
        phaser 使用说明：


### 2.内部维护的数据

     //状态, 用一个字段原子操作
     * unarrived  -- 未到达的参与者       (bits  0-15)
     * parties    -- 总参与者            (bits 16-31)
     * phase      -- 年龄阶段            (bits 32-62)
     * terminated -- 是否终止            (bit  63 / sign)
    private volatile long state;
    //上一级
    private final Phaser parent;
    //根级
    private final Phaser root;
    //被阻塞线程的就绪队列, 如果年龄是奇数用evenQ,偶数用oddQ,以达到减少并发的目的.
    private final AtomicReference<QNode> evenQ;
    private final AtomicReference<QNode> oddQ;
    
![phasestatelong.jpg](/images/postimg/phasestatelong.jpg)

### 3.API

- 模拟代替CountDownLatch功能，只需要当前线程arriveAndAwaitAdvance()之后运行需要的代码之后，就arriveAndDeregister()取消当前线程的注册。
- phaser有一个重大特性，就是不必对它的方法进行异常处理。置于休眠的线程不会响应中断事件，不会抛出interruptedException异常， 只有一个方法会响应：AwaitAdvanceInterruptibly(int phaser).

- 使用phaser.arriveAndDeregister(); //注销当前线程，该线程就不会进入休眠状态，也会从phaser的数量中减少
- 使用phaser.arriveAndAwaitAdvance(); //等待参与者达到指定数量，才开始运行下面的代码

- arrive()：这个方法通知phase对象一个参与者已经完成了当前阶段，但是它不应该等待其他参与者都完成当前阶段，必须小心使用这个方法，因为它不会与其他线程同步。
- awaitAdvance(int phase)：如果传入的阶段参数与当前阶段一致，这个方法会将当前线程至于休眠，直到这个阶段的所有参与者都运行完成。如果传入的阶段参数与当前阶段不一致，这个方法立即返回。
- awaitAdvanceInterruptibly(int phaser):这个方法跟awaitAdvance(int phase)一样，不同处是：该访问将会响应线程中断。会抛出interruptedException异常
        将参与者注册到phaser中：

- register():将一个新的参与者注册到phase中，这个新的参与者将被当成没有执完本阶段的线程。
- bulkRegister(int parties)：将指定数目的参与者注册到phaser中，所有这些新的参与者都将被当成没有执行完本阶段的线程。
        减少参与者 

- 只提供了一个方法来减少参与者：arriveAndDeregister():告知phaser对应的线程已经完成了当前阶段，并它不会参与到下一阶段的操作中。
       强制终止 
- 当一个phaser么有参与者的时候，它就处于终止状态，使用forceTermination()方法来强制phaser进入终止状态，不管是否存在未注册的参与线程，当一个线程出现错误时，强制终止phaser是很有意义的。
       当phaser处于终止状态的时候，arriveAndAwaitAdvance() 和 awaitAdvance() 立即返回一个负数，而不再是一个正值了，
如果知道phaser可能会被终止，就需要验证这些方法的值，以确定phaser是不是被终止了。被终止的phaser不会保证参与者的同步。


### 4.继承

    也可以继承它实现是否停止在某个阶段
    public class MyPhaser extends java.util.concurrent.Phaser {
        //指定初始参与者, 或主动调用register()方法可以+1参与者.
        public MyPhaser(int parties) {
            super(parties);
        }
        /**
         * 在到达时触发
         * @param phase 当前阶段
         * @param registeredParties 当前剩余参与者人数, 只要还有参与者就说明还没执行完.调用arrive系列的方法会减少参与者.
         * @return 是否结束(返回true=唤醒其他所有参与者,并且本次不会阻塞,继续向下执行)
         */
        @Override
        protected boolean onAdvance(int phase, int registeredParties) {    //在每个阶段执行完成后回调的方法
            switch (phase) {
                case 0:
                    return false;
                case 1:
                    return false;
                case 2:
                    return false;
                case 3:
                    //只在第三阶段终止
                    return true;
                default:
                    return true;
            }
        }
    }
    
    public class StudentTask implements Runnable {
        private Phaser phaser;
        public StudentTask(Phaser phaser) {
            this.phaser = phaser;
        }
        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName()+"到达考试");
            phaser.arriveAndAwaitAdvance();
    
            doExercise1();
            System.out.println(Thread.currentThread().getName()+"做第1题完成...");
            phaser.arriveAndAwaitAdvance();
    
            doExercise2();
            System.out.println(Thread.currentThread().getName()+"做第2题完成...");
            phaser.arriveAndAwaitAdvance();
            
            doExercise3();
            System.out.println(Thread.currentThread().getName()+"做第3题完成...");
            phaser.arriveAndAwaitAdvance();
        }
    }
    
     public static void main(String[] args) throws InterruptedException {
            Thread[] threads = new Thread[5];
            //5个参与者
            MyPhaser phaser = new MyPhaser(threads.length);
            for (int i = 0; i < threads.length; i++) {
                threads[i] = new Thread(new StudentTask(phaser), "Student "+i);
                threads[i].start();
            }
            //等待所有线程执行结束
            for (Thread thread : threads) {
                thread.join();
            }
            System.out.println("Phaser has finished:"+phaser.isTerminated());
        }
    }
    
### 5.状态说明：只要不是终止状态下，就可以动态的把线程注册到phaser中。

一个Phaser对象有两个状态：

活跃态：当存在参与同步的线程的时候，Phaser就是活跃的，并且在每个阶段结束的时候进行同步。

终止态：当所有的线程都取消注册的时候，Phaser就处于终止态，此时Phaser没有任何参与者。
