---
categories:
 - Linux
date: 2020-04-23
description: Linux 日志服务系统
tags:
 - Linux
 - log
title: "Linux 日志服务系统"
url: /linux/linux_log/
---

> 日志记录了系统运行过程中的重要信息，当系统出现错误的时候，可以通过其来分析问题  
> Linux有自己的一套日志管理服务系统，即 rsyslog.service，系统管理服务可见 http://fancygo.cn/linux/linux_systemctl/
---
> 日志存放目录 /val/log/  
> 日志系统配置 /etc/rsyslog.conf  
---
> 设置日志服务器  
> 1. 两台机，svr修改 rsyslog.conf，如下，这两行原本是注释掉的
> > ```
> > $ModLoad imtcp
> > $InputTCPServerRun 514
> > ```
> 2. 重启日志服务
> > ```
> > systemctl restart rsyslog.service
> > ```
---
> 设置网络日志  
> 1. cli 修改 rsyslog.conf，如下，表示往ip上发所有日志
> > ```
> > #*.* @@[ip]
> > ```
> 2. 重启日志服务
> > ```
> > systemctl restart rsyslog.service
> > ```
