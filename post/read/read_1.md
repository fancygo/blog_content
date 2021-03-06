---
categories:
 - Read
date: 2020-04-19
description: "读许式伟架构课记录1"
tags:
 - Linux
 - Go
title: "读许式伟架构课记录1"
url: /read/read_1/
---

### 1. 线程的主要成本
> 时间成本
> * 线程切换的开销，主要是寄存器的保存与恢复  
> * 线程的调度  
> * 线程之间的同步与互斥   
>
> 空间成本
> * 线程执行状态
> * 线程局部存储
> * 线程的堆栈

> 这里面堆栈的成本是比较大的，单个线程的堆栈都是MB级别的  
> 线程的调度和同步互斥的开销也需要考量  
> 如果有大量的网络连接，使用多线程的方式会大量消耗空间; 使用Epoll的方式又会使线程调度和同步互斥成本增长太多  
---
### 2. 为了解决线程的问题，很多语言内置线程。Go的goroutine设计就很好
> 优点
> * 初始堆栈4k，然后按需增长
> * 同步IO的编程模式
> * 不再使用"线程局部存储"
> * 提供完整的同步互斥工具
> * 提供完整的IO调用封装
> * 另外我想补充的，Go实现的在语言内部调度goroutine，在时间成本上比系统线程调度要改善很多，同步互斥的成本不知道会不会改善
---
### 3. 不要排斥锁的使用
> * 我也见过很多言论，说Go提倡用channel，所以用channel带替锁显得很厉害
> * 其实channel内部也是需要锁来实现的，所以凡事用channel来代替锁，只会更慢不会更快
> * 使用锁注意两点，要记住解锁，Go1.14对defer已经优化的很好了，所以可以放心爽快的defer Unlock了，另外粒度自己把控好就行，不能太大又不能太小- -

