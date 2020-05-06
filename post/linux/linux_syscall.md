---
categories:
 - Linux
date: 2020-05-05T14:26:01+08:00
description: "Linux 常用系统调用"
tags:
 - Linux
 - syscall
title: "Linux 常用系统调用"
url: "/linux/linux_syscall"
---

### 1. 内存管理
> 调整内存数据段 brk  
> 内存映射 mmap  

### 2. 文件管理
> 打开 open  
> 创建 creat  
> 关闭 close  
> 定位 lseek  
> 读取 read  
> 写入 write  

### 3. 进程管理
> 创建进程 fork
> 运行新二进制文件 execve
> 等待子进程结束 waitpid

### 4. 网络通信
> 创建套接字 socket
> 绑定端口 bind
> 发起连接 connect
> 监听 listen
> 接收连接 accept

### 5. 进程间通信
> 1. 消息队列
> > 创建队列 msgget  
> > 发送消息 msgsnd  
> > 接收消息 msgrcv  

> 2. 共享内存
> > 创建 shmget  
> > 将共享内存映射到内存空间 shmat  

> 3. 信号量
> > 抢占 sem_wait  
> > 释放信号量 sem_post  

### 6. 信号处理
> 发送信号 kill
> 信号处理 sigaction

