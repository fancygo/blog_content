---
categories:
 - Linux
date: 2020-04-16
description: Linux ansible的使用
tags:
 - Linux
 - ansible
title: "Linux ansible的使用"
url: /linux/linux_ansible/
---

### 1.安装直接可以按照此教程 http://www.ansible.com.cn/
> 我的机器一台树莓派，使用
> ```
> 将这行代码
> deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main
> 加到 /etc/apt/sources.list 里，然后执行如下命令
> sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
> sudo apt update
> sudo apt install ansible
> ```
> 还有两个云服务器是Centos，使用如下命令安装
> ```
> sudo yum install ansible
> ``` 

### 2.配置
> 我的管理机是树莓派，从机是两台云服务器  
> 在管理机配置文件 /etc/ansible/hosts 中配置从机 IP ，配置代码如下
> ```
> // fancy_srv 是服务器组的名称，fancy_qq 和 fancy_qq_cli 是两台服务器的名称，可按需要随意设置名字，
>  ansible_ssh_port 和 ansible_ssh_host 是从机服务器的 ssh 端口和 IP
> (使用之前应先配置好 ssh 服务，官方建议使用秘钥文件登录的方式，配置方法可见 http://fancygo.cn/linux/linux_ssh/ )
> [fancy_srv]
> fancy_qq ansible_ssh_port=22 ansible_ssh_host=xxx.xxx.xxx.xxx
> fancy_qq_cli ansible_ssh_port=22 ansible_ssh_host=xxx.xxx.xxx.xxx
> ```

### 3.测试
> 在管理机中断输入如下命令，all表示向所有主机发送ping测试
> ```
> ansible all -m ping
> ```
> 若配置正确会返回如下信息
> ```
> fancy_qq_cli | SUCCESS => {
>    "ansible_facts": {
>        "discovered_interpreter_python": "/usr/bin/python"
>    }, 
>    "changed": false, 
>    "ping": "pong"
> }
> fancy_qq | SUCCESS => {
>     "ansible_facts": {
>        "discovered_interpreter_python": "/usr/bin/python"
>    }, 
>    "changed": false, 
>    "ping": "pong"
> }
> ```

### 4.这是ansible最简单的使用方法，更多功能还需学习
---
