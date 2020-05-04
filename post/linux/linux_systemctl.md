---
categories:
 - Linux
date: 2020-04-18
description: Linux 系统服务的使用
tags:
 - Linux
 - systemctl
title: "Linux 系统服务的使用"
url: /linux/linux_systemctl/
---

## 服务：常驻系统内存中的进程且可以提供一些系统和网络功能
## 现在最新的Linux系统都统一使用systemctl进行服务的管理

### 1.运行级别的分类 runlevel
> ```
> 运行级别0：系统停机状态
> 运行级别1：单用户工作状态，root权限，用于系统维护，禁止远程登陆 
> 运行级别2：多用户状态(没有NFS) 
> 运行级别3：完全的多用户状态(有NFS)
> 运行级别4：系统未使用，保留 
> 运行级别5：X11控制台
> 运行级别6：系统正常关闭并重启
> ```

### 2.管理服务 systemctl （root权限）
> systemctl [opt] xxx.service
> ```
> status 	查看当前服务状态
> start 	启动服务
> stop 	关闭服务
> restart 重启服务
> enable	设置开机启动
> disable	设置开机不启动
> reload 	后面不接具体服务名，重新加载配置文件
> mask	注销服务
> unmask	取消注销
> ```

### 3.一些常用命令 systemctl
> 查看当前已经启动的服务 systemctl list-units  
> 查看所有服务 systemctl list-unit-files  
> 查看服务有哪些依赖 systemctl list-dependencies xx.service  
> 查看服务有哪些依赖(反向) systemctl list-dependencies --reverse xx.service  

### 4.system 服务相关的一些目录( Centos 环境，Debian 类的环境可能会有稍许不同)
> ```
> /usr/lib/systemd/system/ 系统安装的软件默认启动脚本目录 
> /etc/systemd/system/ 用户根据自己需要建立的启动脚本目录
> /etc/sysconfig/ 服务初始化选项目录
> /var/lib/ 服务运行时产生的数据存储目录
> /etc/xxx/ 各服务配置目录
> ```

### 5.结合一个例子来具体讲解，一台机开启两个ssh服务
> 我们最常使用的ssh服务，系统默认ssh服务22端口，我现在想再开一个ssh服务，端口8888
> 1. 系统服务启动脚本 /usr/lib/systemd/system/sshd.service，将其复制到 /etc/systemd/system/ 下，并改名为 sshd2.service，文件内容如下
> > ```
> > [Unit]
> > Description=OpenSSH server daemon
> > Documentation=man:sshd(8) man:sshd_config(5)
> > After=network.target sshd-keygen.service
> > Wants=sshd-keygen.service
> > 
> > [Service]
> > Type=notify
> > EnvironmentFile=/etc/sysconfig/sshd
> > ExecStart=/usr/sbin/sshd -D $OPTIONS
> > ExecReload=/bin/kill -HUP $MAINPID
> > KillMode=process
> > Restart=on-failure
> > RestartSec=42s
> > 
> > [Install]
> > WantedBy=multi-user.target
> > ```
> > 因为要重启一个新的服务，所以要修改一下ExecStart这一行，读取新的配置文件 sshd2_config，改为
> > ```
> > ExecStart=/usr/sbin/sshd -D $OPTIONS -f /etc/ssh/sshd2_config
> > ```
> 2. 到 /etc/ssh/ 下，将 sshd_config 复制到 sshd2_config，并修改端口那一行
> > ```
> > Port 8888
> > ```
> 3. 运行命令 systemctl reload 重新加载一下配置
> 4. 运行命令 systemctl status sshd2.service 查看状态
> 5. 运行命令 systemctl start sshd2.service 开启服务
> 6. 运行命令 systemctl enable sshd2.service 设置开机启动
> 7. 在另一台机器上登录 ssh fancy@ip -p8888 就可以登录了  
> * 注意1，防火墙要打开8888端口  
> * 注意2，官方建议用户自己新建的服务脚本最好存放在 /etc/systemd/system/ 目录下，实际情况下存放在系统服务目录 /usr/lib/systemd/system/ 下也是没有问题的，看个人选择了

### 6.我们再来举个例子，做一个自己的服务
> 1. 在 /root/bin/ 下创建一个shell脚本 fancy_test.sh，并修改其权限，chmod u+x fancy_test.sh，内容如下
> > ```
> > #!/bin/bash
> > logdate=$(date +%s)
> > logdir="/root/log/"
> > logname=fancy.${logdate}.log
> > #echo $logname
> > touch ${logdir}${logname}
> > ```
> > 意思是，运行该服务时，在 /root/log/ 目录下创建一个日志文件
> 
> 2. 在 /etc/systemd/system/ 下创建启动脚本 fancy_test.service，输入一下内容
> > ```
> > [Unit]
> > Description=fancy_test server daemon
> > 
> > [Service]
> > Type=simple
> > ExecStart=/root/bin/fancy_test.sh
> > 
> > [Install]
> > WantedBy=multi-user.target
> > ```
> 
> 3. 运行命令 systemctl reload
> 4. 运行命令 systemctl start fancy_test.service
> 5. 此时你会看到在 /root/log/ 目录下创建了一个日志文件
> * 注意，我们这个是最简单的服务，执行几个命令而已，所以没有配置文件，也不会常驻内存，运行一次就结束
