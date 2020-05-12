+++
categories = ["Linux"]
date = "2019-11-05"
description = "一些Linux常用命令"
tags = ["Linux"]
title = "Linux常用的命令"
url = "/linux/linux_cmd/"
+++

### 用户管理
> 1.添加用户
> ```
> useradd fancy
> ```
> 2.添加组
> ```
> groupadd fancy
> ```
> 3.设置密码
> ```
> passwd fancy
> echo "xxxxx" | passwd fancy --stdin
> ```
> 5.加入sudo用户
> ```
> sudo echo "%fancy ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
> ```

### 后台运行
> ```
> nohup ./a.out&
> ```

### 遍历删除所有文件
> ```
> find . -name .svn -exec rm -rf {} \;
> ```
 
### 时间
> 1.计算指定时间的时间戳
> ```
> date +%s -d '2015-11-10 01:01:01'
> ```
> 2.时间戳转换为实际时间
> ```
> date -d @1233631748
> ```
> 3.设置系统时间
> ```
> date -s "20091112 18:30:50"
> ```

### 文件夹大小
> ```
> du -s ./
> du -h --max-depth=1
> du -sh *|sort -nr
> ```

### KILL
> 1.查看信号定义
> ```
> kill -l
> ```
> 2.给进程发信号
> ```
> kill -s SIGHUB 进程号
> ```

### 查看公网ip
> ```
> curl cip.cc
> ```

### netstat
> ```
> netstat -anpt
> ```

### basename 返回绝对路径的最后一个
> ```
> basename /home/fc/hello
> 会打印出hello
> ```

### lastlog 返回最近登陆用户

### htop 管理进程

### ctrl-z 和 fg 配合使用

### sudo!! 使用 sudo 运行上一条没有 sudo 的命令

### 一系列控制命令
> ```
> CTRL + U -剪切光标前的内容
> CTRL + K -剪切光标至行末的内容
> CTRL + Y -粘贴
> CTRL + E -移动光标到行末
> CTRL + A -移动光标到行首
> ALT + F -跳向下一个空格
> ALT + B -跳回上一个空格
> ALT + Backspace -删除前一个单词
> CTRL + W -剪切光标后一个单词
> ```

### 在指定文件中查找字符串，比 find 会快一点
> ```
> grep -rn --color --include=*.go $1
> ```
