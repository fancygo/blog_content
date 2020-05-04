---
categories:
 - Linux
date: 2020-04-24
description: Linux 后台模式运行脚本
tags:
 - Linux
title: "Linux 后台模式运行脚本"
url: /linux/linux_back/
---

> 1.最简单的方法就是在命令后面加个 &，但这种方式有个弊端，就是该命令进程会与当前会话关联，如果当前会话退出，该进程也会退出  
> 2.nohup [cmd] &，如此就可解决这个问题

