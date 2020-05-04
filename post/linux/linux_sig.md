---
categories:
 - Linux
date: 2020-04-24
description: Linux 信号相关
tags:
 - Linux
 - sig
title: "Linux 信号相关"
url: /linux/linux_sig/
---

## Linux利用信号与进程进行通信

### 常用信号
> ```
> 1   SIGHUP  挂起进程
> 2   SIGINT  终止进程
> 3   SIGQUIT 停止进程
> 9   SIGKILL 无条件终止进程
> 15  SIGTERM 尽可能终止进程
> 17  SIGSTOP 无条件停止进程
> 18  SIGTSTP 停止进程
> 19  SIGCONT 继续运行停止的进程
> ```
> kill -l 命令可以查看所有信号

### 在shell脚本中捕捉信号
> trap [cmd] [sig]  
> 下面程序会捕捉 SIGINT 信号  
> ```
> trap "echo 'get sigint'" SIGINT
> 
> count=1
> while [ ${count} -le 10 ]
> do
>     echo "count: ${count}"
>     sleep 1
>     count=$[ ${count} + 1 ]
> done
> ```

### 恢复默认信号
> trap - [sig]
