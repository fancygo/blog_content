+++
categories = ["Linux"]
date = "2020-04-14"
description = "Vim使用过程中相关问题"
tags = ["Vim"]
title = "Vim使用过程中相关问题"
url = "/linux/linux_vim/"
+++

> 因为从大学的时候就开始使用Vim，所以到现在用的最顺手Idea的也就是Vim了，这篇文章就用来记录一下使用过程中的一些问题。

1. 我们经常遇到把其他环境代码复制到Vim中时出现缩进的问题，这时候复制完进入Vim后先输入
> :set paste 
2. 然后再粘贴，就好了，粘贴完记住输入命令回到原设置
> :set nopaste
3. 批量在行首添加字符
> Ctrl + V 选择最左边一排  
> 上下移动  
> 输入大写的  
> 输入字符  
> 按两下 ESC  
4. vim 命令行运行 Linux 命令
> 命令行模式中在命令前加上 ! 即可
