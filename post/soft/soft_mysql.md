---
categories:
 - Soft
date: 2020-05-12T16:23:06+08:00
description: "MySQL 服务器搭建及使用"
tags:
 - mysql
title: "MySQL 服务器搭建及使用"
url: "/soft/soft_mysql"
---

# 1. 树莓派安装 MySQL
> 安装
> > ```
> > apt install mariadb-server-10.0
> > ```
> 配置
> > ```
> > mysql_secure_installation
> > ```
> 登录
> > ```
> > mysql -uroot -pxxxxxx
> > ```
> 添加用户
> > ```
> > create user 'fancy'@'localhost' identified by 'xxxxxx';
> > grant all on *.* to 'fancy'@'localhost' identified by 'xxxxxx';
> > ```
> 然后 fancy 用户就可以登录使用了
> > ```
> > mysql -ufancy -pxxxxxx
> > ```
