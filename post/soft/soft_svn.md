---
categories:
 - Soft
date: 2020-05-11T16:33:06+08:00
description: "svn 服务器搭建及使用"
tags:
 - Linux
 - svn
title: "svn 服务器搭建及使用"
url: "/soft/soft_svn"
---

# 1. svn 服务器安装( 我以下的命令皆在 root 权限下运行)
> Centos
> > ```
> > yum install subversion
> > ```
> 树莓派
> > ```
> > apt install subversion
> > ```
> 成功安装后，即可查看版本
> > ```
> > svnserve --version
> > ```

# 2. 创建仓库
> 在用户 home 目录下创建一个文件夹作为 svn 仓库（读者可自己选择在何目录下创建）
> > ```
> > mkdir svn
> > svnadmin create svn
> > ```

# 3. 修改权限
> svn 服务配置文件都存放在 svn/conf 下
> passwd 文件存放用户和密码，格式如下
> > ```
> > [users]
> > # 用户名 = 密码
> > fancy = 123456
> > soft = 123456
> > fc = 123456
> > test = 123456
> > ```
> authz 文件存放用户权限，格式如下
> > ```
> > # 用户组，组下存放各个成员用户名
> > [groups]
> > admin = fancy
> > dev = soft,fancy
> > ops = fc
> > test = test
> > # 各个文件夹的权限，rw 表示可读可写，r 表示只读 
> > # 我下面的配置表示，/ 目录 admin 组用户可读可写，dev 组用户可读，ops 组用户可读，其他用户没有权限
> > # /dev 目录只有 dev 组可读写，/ops 目录只有 ops 组用户可读写
> > [/]
> > @admin = rw
> > @dev = r 
> > @ops = r 
> > * =
> > [/dev]
> > @dev = rw
> > * =
> > [/ops]
> > @ops = rw
> > * =
> > ```
> svnserve.conf 文件是 svn 服务器启动配置，将下面几行的注释去掉即可
> > ```
> > auth-access = write   
> > password-db = passwd  
> > authz-db = authz  
> > realm = My First Repository  
> > ```

# 4. 启动 svn 服务
> svnserve  -d -r ./svn ，svn 就是刚创建的目录

# 5. 这个时候就可以正常使用 svn 了
---
