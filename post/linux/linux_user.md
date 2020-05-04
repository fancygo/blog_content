---
categories:
    - Linux
date: 2020-04-17
description: Linux 用户管理
tags:
    - Linux
title: "Linux 用户管理"
url: /linux/linux_user/
---

### 1.添加用户 useradd
> 1.useradd -D  
> 查看添加用户的默认值
> ```
> GROUP=100 //新用户组ID
> HOME=/home //新用户home目录位于该目录下
> INACTIVE=-1 //密码过期后不会被禁用
> EXPIRE= //密码未设置过期日期
> SHELL=/bin/bash //默认shell
> SKEL=/etc/skel //该目录下的文件会被复制到用户home目录下
> CREATE_MAIL_SPOOL=yes //在mail下创建一个用于接收邮件的文件
> ```
> 
> 2.useradd -m [user]  
> 添加一个用户，并创建home目录。Centos系统下不加参数也可以创建home目录，但我的树莓派不加参数就不会创建目录。
> 
> 3.useradd -D -[opt] [content]  
> 修改默认值
> ```
> -b 修改默认home目录位置
> -e 修改过期日期
> -g 修改组名称或GID
> -s 修改默认shell
> ex：useradd -D -s /bin/sh
> ```

### 2.删除用户 userdel
> 1.userdel [user]  
> 删除用户
> 
> 2.userdel -r [user]  
> 删除用户并删除用户home目录
> 
> 3.修改已有用户 usermod  
> usermod -[opt] [user]
> ```
> -L 锁定用户，使其无法登陆
> -U 解除锁定
> -p 修改密码
> -G 将一个用户加到一个组里 usermod -G <grpname> <username>
> ex: usermod -L fcuser
> ex: usermod -G group user
> ```

### 3.修改密码 passwd
> 1.passwd [user]  
> 修改用户密码  
> 2.passed -e [user]  
> 强制user下次登陆的时候修改密码

### 4. 批量修改密码 chpasswd
> chpasswd \< userpasswd.txt
> userpasswd.txt里面以 user:passwd 的格式存储

### 5. 修改默认登陆shell chsh
> chsh -s /bin/sh [user]

### 6. 修改用户账户有效期 chage
> chage -[opt] [user]
> ```
> -l 查看账户有效期
> -d 设置上次修改密码时间
> -E 设置密码失效时间
> -I 设置密码失效到锁定账户的时间
> -W 设置密码失效前多少天提醒
> ex: chage -d 40 fcuser
> ex: chage -d 2020-04-16 fcuser
> ```
 
### 7. 添加新组 groupadd 
> groupadd [grpname]
> 
### 8. 修改组名 groupmod
> groupmod -n [oldname] [newname]
> groupmod -g [oldgid] [newgid]
