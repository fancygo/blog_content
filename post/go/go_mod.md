+++
categories = ["Go"]
date = "2019-11-06"
description = "Go module 常用方法" 
tags = ["Go"]
title = "Go module 常用方法" 
url = "/go/module/"
+++

1. 升级Go到1.13

2. 设置各类环境变量
> ```
> export PATH=$PATH:~/go/bin
> export GOROOT=~/go
> export GOPATH=~/gopkg
> export GO111MODULE=on
> export GOBIN=~/gobin
> export GOCACHE=~/gocache
> export GOPROXY=https://goproxy.cn,direct
> ```

3. 新建目录fancygo（根据项目需要自行修改目录名字）
> ```
> mkdir fancygo
> cd fancygo
> ```

4. 创建 main.go 并写入代码, 并保存
> ```
> package main
> import(
>     "fmt"
> )
> func main() {
>     fmt.Println("fancygo")
> }
> ```

5. 生成go.mod文件
> ```
> go mod init
> ```

6. 运行
> ```
> go run main.go
> ```
