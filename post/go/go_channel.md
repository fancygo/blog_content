+++
categories = ["Go"]
date = "2019-11-07"
description = "Go channel 不同行为" 
tags = ["Go"]
title = "Go channel 不同行为" 
url = "/go/channel/"
+++

## panic
 * 向已经关闭的 chan 写数据
 * 重复关闭 chan

## 阻塞
 * 向未初始化的 chan 读写数据会导致 goroutine 永久阻塞
 * 向已满的 chan 写，从空 chan 读

## 0值
 * 读取已关闭的 chan，会成功读取数据，读完会读到0值


