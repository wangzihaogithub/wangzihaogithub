---
layout: post
title:  "JAVA编程-多线程协调工具_ReentrantLock"
tags: JAVA编程
---

### 1.来历

大多数情况下，**不仅不存在多线程竞争，还存在锁由同一线程多次获得的情况**，偏向锁与ReentrantLock就是在这种情况下出现的

在1.6前, synchronized关键字是用是用系统调用实现的(例如:pthread_mutex_t). 获取锁动作与释放锁动作.

在1.5出现了JUC库, 例如ReentrantLock.
   

| JDK版本 | 锁实现 | 获取锁动作 | 释放锁动作|
| :- | :- | :- |  :- | 
|1.5	|synchronized关键字|	系统调用 例如:pthread_mutex_t|	同上|
|1.5	|ReentrantLock|	在不存在资源竞争的情况下不会系统调用,反之|	同上|
|1.6	|synchronized关键字|	在不存在资源竞争的情况下不会系统调用,反之.依据对象头中的线程ID是否是当前持有线程,|	同上|
|1.6	|ReentrantLock|	在不存在资源竞争的情况下不会系统调用,反之|	同上|

### 2.关键词
 
 **volatile + cas操作, 等待队列, 线程持有者, 公平锁与非公平锁, 减少系统调用.**
   
### 3.ReentrantLock的实现
   
**内部变量** 
 
state + 等待线程的队列 + 当前线程持有者
 
**执行逻辑**
   
- 获取成功时; 获取state字段时,值为0或当前线程持有者是自己,则判定成功. 且state字段+1(cas操作). 
   
   **公平锁**会在获取成功后,会再检查是否需要排队
   
   **非公平锁**获取成功后直接使用返回,不检查是否需要排队.
           
- 获取失败时; 将当前线程追加到等待队列中,并且park当前线程(系统调用).
      
- 释放锁时; 状态变量-1, 如果没有人排队,则返回. 如果队列中有线程,则叫醒最早排队的那个线程(系统调用).


### 4.synchronized关键字的实现 (源码没看懂, 希望能有大神带入门)
    
   synchronized由字节码指令(**monitorenter** 与 **monitorexit**)实现.

   下面代码摘自 [https://download.java.net/openjdk/jdk6/](https://download.java.net/openjdk/jdk6/ "https://download.java.net/openjdk/jdk6/")

**monitorenter指令的实现**

目录地址 /hotspot/src/share/vm/interpreter/interpreterRuntime.cpp:585
    
     IRT_ENTRY_NO_ASYNC(void, InterpreterRuntime::monitorenter(JavaThread* thread, BasicObjectLock* elem))
     if (PrintBiasedLockingStatistics) {
       Atomic::inc(BiasedLocking::slow_path_entry_count_addr());
     }
     Handle h_obj(thread, elem->obj());
  
     if (UseBiasedLocking) {
       // Retry fast entry if bias is revoked to avoid unnecessary inflation
       ObjectSynchronizer::fast_enter(h_obj, elem->lock(), true, CHECK);
     } else {
       ObjectSynchronizer::slow_enter(h_obj, elem->lock(), CHECK);
     }
 
目录地址 /hotspot/src/share/vm/runtime/synchronizer.cpp:158
         
    void ObjectSynchronizer::fast_enter(Handle obj, BasicLock* lock, bool attempt_rebias, TRAPS) {
     if (UseBiasedLocking) {
        if (!SafepointSynchronize::is_at_safepoint()) {
          BiasedLocking::Condition cond = BiasedLocking::revoke_and_rebias(obj, attempt_rebias, THREAD);
          if (cond == BiasedLocking::BIAS_REVOKED_AND_REBIASED) {
            return;
          }
        } else {
          assert(!attempt_rebias, "can not rebias toward VM thread");
          BiasedLocking::revoke_at_safepoint(obj);
        }
        assert(!obj->mark()->has_bias_pattern(), "biases should be revoked by now");
     }
     slow_enter (obj, lock, THREAD);
    }
    
    void ObjectSynchronizer::slow_enter(Handle obj, BasicLock* lock, TRAPS) {
      markOop mark = obj->mark();
      assert(!mark->has_bias_pattern(), "should not see bias pattern here");
      if (mark->is_neutral()) {
        // Anticipate successful CAS -- the ST of the displaced mark must
        // be visible <= the ST performed by the CAS.
        lock->set_displaced_header(mark);
        if (mark == (markOop) Atomic::cmpxchg_ptr(lock, obj()->mark_addr(), mark)) {
          TEVENT (slow_enter: release stacklock) ;
          return ;
        }
        // Fall through to inflate() ...
      } else
      if (mark->has_locker() && THREAD->is_lock_owned((address)mark->locker())) {
        assert(lock != mark->locker(), "must not re-lock the same lock");
        assert(lock != (BasicLock*)obj->mark(), "don't relock with same BasicLock");
        lock->set_displaced_header(NULL);
        return;
      }
    
      // The object header will never be displaced to this lock,
      // so it does not matter what the value is, except that it
      // must be non-zero to avoid looking like a re-entrant lock,
      // and must not look locked either.
      lock->set_displaced_header(markOopDesc::unused_mark());
      ObjectSynchronizer::inflate(THREAD, obj())->enter(THREAD);
    }
    

**monitorexit指令的实现**

目录地址 /hotspot/src/share/vm/interpreter/interpreterRuntime.cpp:610

     IRT_ENTRY_NO_ASYNC(void, InterpreterRuntime::monitorexit(JavaThread* thread, BasicObjectLock* elem))
     Handle h_obj(thread, elem->obj());
     if (elem == NULL || h_obj()->is_unlocked()) {
       THROW(vmSymbols::java_lang_IllegalMonitorStateException());
     }
     ObjectSynchronizer::slow_exit(h_obj(), elem->lock(), thread);
     // Free entry. This must be done here, since a pending exception might be installed on
     // exit. If it is not cleared, the exception handling code will try to unlock the monitor again.
     elem->set_obj(NULL);
     
目录地址 /hotspot/src/share/vm/runtime/synchronizer.cpp:240   
  
    // This routine is used to handle interpreter/compiler slow case
    // We don't need to use fast path here, because it must have
    // failed in the interpreter/compiler code. Simply use the heavy
    // weight monitor should be ok, unless someone find otherwise.
    void ObjectSynchronizer::slow_exit(oop object, BasicLock* lock, TRAPS) {
      fast_exit (object, lock, THREAD) ;
    }
    
    void ObjectSynchronizer::fast_exit(oop object, BasicLock* lock, TRAPS) {
      assert(!object->mark()->has_bias_pattern(), "should not see bias pattern here");
      // if displaced header is null, the previous enter is recursive enter, no-op
      markOop dhw = lock->displaced_header();
      markOop mark ;
      if (dhw == NULL) {
         // Recursive stack-lock.
         // Diagnostics -- Could be: stack-locked, inflating, inflated.
         mark = object->mark() ;
         assert (!mark->is_neutral(), "invariant") ;
         if (mark->has_locker() && mark != markOopDesc::INFLATING()) {
            assert(THREAD->is_lock_owned((address)mark->locker()), "invariant") ;
         }
         if (mark->has_monitor()) {
            ObjectMonitor * m = mark->monitor() ;
            assert(((oop)(m->object()))->mark() == mark, "invariant") ;
            assert(m->is_entered(THREAD), "invariant") ;
         }
         return ;
      }
      mark = object->mark() ;
      // If the object is stack-locked by the current thread, try to
      // swing the displaced header from the box back to the mark.
      if (mark == (markOop) lock) {
         assert (dhw->is_neutral(), "invariant") ;
         if ((markOop) Atomic::cmpxchg_ptr (dhw, object->mark_addr(), mark) == mark) {
            TEVENT (fast_exit: release stacklock) ;
            return;
         }
      }
      ObjectSynchronizer::inflate(THREAD, object)->exit (THREAD) ;
    }