+++
categories = ["Crypt"]
date = "2019-11-23"
description = "最简易的密码，类似凯撒密码" 
tags = ["Crypt"]
title = "简易密码实现，类似凯撒密码（c语言和go语言）" 
url = "/crypt/caesar/"
+++

> 凯撒密码基本的理念就是位移取模  
> 我们来加密一段字符串a，密钥key取500，这里的key可以取任意的整数, m作为取值的范围，不能小于可取值的范围，这里取8位2进制的最大值256  
> 加密算法 cipher = （plain + key）mod m   
> 解密算法 plain = （cipher - key）mod m 因为括号里的值有可能是负数，需要处理一下  

> 1. 创建 main.c 并写入代码, 并保存  
> >  ```
> > #include <stdio.h>
> > #include <string.h>
> > int main() 
> > {
> >     char a[20] = "Hello fancy, 789";
> >     int key = 500;
> >     int m = 256;
> >     printf("plain = %s\n", a); 
> > 
> >     char b[20];
> >     for (int i = 0; i < strlen(a); i++)
> >     {   
> >         b[i] = (a[i] + key) % m;
> >     }   
> >     printf("cipher = %s\n", b); 
> >     char p[20];
> >     for (int i = 0; i < strlen(b); i++)
> >     {   
> >         char temp = (b[i] - key) % m;
> >         p[i] = temp > 0 ? temp : temp + m;
> >     }   
> >     printf("plain = %s\n", p); 
> >     return 0;
> > }
> >  ```
---
> 2. 编译
> > ```
> > gcc -std=c11 main.c
> > ```
---
> 3. 运行输出
> > ```
> > ./a.out
> > plain = Hello fancy, 789
> > cipher = <Y``cZUbWm +,-
> > plain = Hello fancy, 789
> > ```
---
> 4. go语言实现
> > ```
> > package main
> > 
> > import "fmt"
> > 
> > func main() {
> >     str := "Hello fancy, 789"
> >     key := rune(500)
> >     rg := rune(256)
> >     fmt.Printf("%s\n", str)
> > 
> >     a := []rune(str)
> >     b := make([]rune, len(a), len(a))
> >     for i := 0; i < len(str); i++ {
> >         b[i] = (a[i] + key) % rg
> >     }
> > 
> >     fmt.Printf("%s\n", string(b))
> > 
> >     p := make([]rune, len(str), len(str))
> >     for i := 0; i < len(str); i++ {
> >         temp := (b[i] - key) % rg
> >         if temp > 0 {
> >             p[i] = temp
> >         } else {
> > 		    p[i] = temp + rg
> >         }
> >     }
> >     fmt.Printf("%s\n", string(p))
> > }
> > ```
---
