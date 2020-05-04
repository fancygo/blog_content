---
categories:
 - Linux
date: "2020-04-14"
description: Git常用命令
tags:
 - Linux
 - Git
title: "Git常用命令"
url: /linux/linux_git/
---

### 非详细教程，仅供查阅

1. git初始认证 
    ```
    ssh-keygen -t rsa -C "717632318@qq.com" 生成秘钥对
    将.ssh/id_rsa.pub 中的公钥放到github中
    ```
2. 初始化目录
    ```
    git init
    ```
3. 添加文件
    ```
    git add <filename>
    ```
4. 删除文件
    ```
    git rm <filename>
    ```
5. 提交
    ```
    git commit -m "log" <filename>
    ```
6. 查看修改状态
    ```
    git status
    ```
7. 查看提交日志
    ```
    git log
    git log --pretty=online
    ```
8. 检出提交过的文件
    ```
    git checkout --<filename>
    ```
9. 回滚到某一版本号
    ```
    git reset --hard <commititd>
    ```
10. 查看操作过命令日志
    ```
    git reflog
    ```
11. 拉取远程库，两种方法，分别使用两种协议
    ```
    git clone https://github.com/fancygo/hello.git
    git clone git@github.com:fancygo/hello.git
    ```
12. 将本地库与远程库链接
    ```
    git remote add origin git@github.com:fancygo/*.git
    ```
13. 提交本地库修改到远程
    ```
    git push origin master
    ```
14. 拉取远程库修改
    ```
    git pull origin master
    ```
15. 打tag
    ```
    git tag <tagver>
    ```
16. 提交tag
    ```
    git push origin <tagver>
    git push --tags 
    ```
17. 创建并切换分支
    ```
    git checkout -b <branchver>
    ```
18. 提交分支
    ```
    git push -u oring <branchver>
    ```
19. 创建分支
    ```
    git branch <branchver>
    ```
20. 切换分支
    ```
    git checkout <branchver>
    ```
21. 查看分支
    ```
    git branch -a
    git branch
    ```
22. 合并分支到当前分支
    ```
    git merge <ver>
    ```
23. 删除分支
    ```
    git branch -d <ver>
    ```
24. 查看远程库信息
    ```
    git remote -v
    ```
