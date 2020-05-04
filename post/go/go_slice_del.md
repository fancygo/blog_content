+++
categories = ["Go"]
date = "2020-02-22"
description = "删除Go切片中的某些值" 
tags = ["Go"]
title = "删除Go切片中的某些值" 
url = "/go/slicedel/"
+++

1. 方法1
> ```
> func del(data []int, d int) []int {
>     i := 0
>     for _, v := range data {
>         if v != d {
>             data[i] = v
>             i++
>         }
>     }
>     return data[:i]
> }
> ```

2. 方法2
> ```
> func del2(data []int, d int) []int {
>     for i := 0; i < len(data); i++ {
>         if data[i] == d {
>             data = append(data[0:i], data[i+1:len(data)]...)
>             i--
>         }
>     }	
>     return data
> }
> ```
