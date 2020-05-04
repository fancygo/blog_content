---
categories: 
 - Linux
date: 2020-04-16
description: Linux系统知识
tags:
 - Linux
title: "Linux系统知识"
url: /linux/linux_proc/
---

### 进程切换过程
> ```
> 保存处理机上下文，包括程序计数器和其他寄存器。
> 更新PCB信息。
> 把进程的PCB移入相应的队列，如就绪、在某事件阻塞等队列。
> 选择另一个进程执行，并更新其PCB。
> 更新内存管理的数据结构。
> 恢复处理机上下文。
> ```
