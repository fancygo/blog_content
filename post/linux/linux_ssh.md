---
categories:
 - Linux
date: 2020-04-16
description: Linux ssh的使用
tags:
 - Linux
 - ssh
title: "Linux ssh的使用"
url: /linux/linux_ssh/
---

> ssh是我们最常用的登录到远程服务器的方式，它使用非对称加密方式进行数据传输

### 1. 生成秘钥对
> ```
> ssh-keygen -t rsa -C "717632318@qq.com"
> ```
> 生成的秘钥对存放在~/.ssh/下，id_rsa为私钥，id_rsa.pub为公钥

### 2.密码登录
> ```
> ssh -P 22 <remote_user>@<remote_ip> 输密码
> ```

### 3.私钥文件登录
> ```
> ssh -P 22 -i ~/.ssh/id_rsa <remote_user>@<remote_ip>
> ```

### 4.免密登录
> 将本机的公钥文件id_rsa.pub中的内容存放到远端机~/.ssh/authorized_keys中，没有该文件可以新建一个
> ```
> ssh -P 22 <remote_user>@<remote_>
> ```

### 5.sftp的使用
> 登录方式和ssh类似
> ```
> ssh -P 22 <remote_user>@<remote_ip> 输密码
> ssh -P 22 -i ~/.ssh/id_rsa <remote_user>@<remote_ip>
> ssh -P 22 <remote_user>@<remote_>
> ```
> sftp上传和下载命令
> ```
> get <filename>
> put <filename>
> get -r <dirname> #下载整个目录
> put -r <dirname> #上传整个目录
> ```

### 6.限制root远程登录
> 修改文件/etc/ssh/sshd_config配置
> ```
> 添加
> PermitRootLogin no
> ```
> 重启sshd服务
