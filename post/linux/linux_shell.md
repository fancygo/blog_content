---
categories:
 - Linux
date: 2020-04-15
description: Linux shell编程
tags:
 - Linux
 - Shell
title: "Linux shell编程"
url: /linux/linux_shell/
---

#### 1. 进程列表
> ```
> 命令外加上括号会变成进程列表，当前shell会生成一个子shell来执行括号内的一组命令  
> echo $BASH_SUBSHELL是否是1可用来显示是否是子shell  
> (ls; pwd; ps x; echo $BASH_SUBSHELL)  
> ```

#### 2. echo 输出变量值或字符串
> ```
> echo "Hello Fancygo"  
> echo -n "Hello Fancygo" #输出后不换行  
> ```

#### 3. 命令替换，两种方式 \`\` 和 $()
> ```
> a=`date`
> b=$(date)
> 此时a和b的值就是date命令的输出内容，命令替换会创建一个子shell来执行，所以子shell内的变量在外面是无效的
> ```

#### 4. 条件判断
> ##### 1. 普通if判断，该判断只能判断命令执行的返回码
> > ex: 该段代码会打印success
> > ```
> > if pwd 
> > then
> >     echo "success"
> > else
> >     echo "fail"
> > fi
> > ```
> ##### 2. test判断，可以判断某个条件是否成立
> > ex: 该段代码会分别判断val1和val2是否存在，打印success和fail
> > ```
> > val1="1"
> > val2=""
> > if test ${val1}
> > then
> >     echo "success"
> > else
> >     echo "fial"
> > fi
> > if test ${val2}
> > then
> >     echo "success"
> > else
> >     echo "fial"
> > fi
> > ```
> ##### 3.test判断的另一种书写方法就是给把test去掉，然后给判断条件加上[]，且[与命令之间有空格，命令与]之间也有空格(没空格会出错哦)
> ##### 4.数值比较(只能比较整数)
> > ```
> > n1 -eq n2   n1是否与n2相等
> > n1 -ge n2   n1是否大于等于n2
> > n1 -gt n2   n1是否大于n2
> > n1 -le n2   n1是否小于等于n2
> > n1 -lt n2   n1是否小于n2
> > n1 -ne n2   n1是否不等于n2
> > ```
> > ex: 该段代码会打印val1 = val2， val = 10
> > ```
> > val1=10
> > val2=10
> > 
> > if [ ${val1} -eq ${val2} ]
> > then
> >     echo "val1 = val2"
> > else
> >     echo "val1 != val2"
> > fi
> > 
> > if [ ${val1} -eq 10 ]; then
> >     echo "val = 10"
> > else
> >     echo "val != 10"
> > fi
> > ```
> ##### 5. 字符串比较
> > ```
> > str1 = str2    str1与str2是否相等
> > str1 != str2   str1与str2是否不相等
> > -n str1        str1长度是否非0
> > -z str1        str1长度是否为0
> > ```
> > ex: 该段代码会打印str1=str2，str1!=str3，str1 长度非0，str4 长度是0
> > ```
> > str1="fancygo"
> > str2="fancygo"
> > str3="fc"
> > str4=""
> > 
> > if [ ${str1} = ${str2} ]
> > then
> >     echo "str1=str2"
> > fi
> > 
> > if [ ${str1} != ${str3} ]
> > then
> >     echo "str1!=str3"
> > fi
> > 
> > if [ -n ${str1} ]
> > then
> >     echo "str1 长度非0"
> > fi
> > 
> > if [ -z ${str4} ]
> > then
> >     echo "str4 长度是0"
> > fi
> > ```
> 
> ##### 6. 文件比较，不举例了
> > ```
> > -d file  file是否存在并是一个目录
> > -e file  file是否存在
> > -f file  file是否存在并是一个文件
> > -r file  file是否存在并可读
> > -s file  file是否存在并非空
> > -w file  file是否存在可写
> > -x file  file是否存在并可执行
> > -O file  file是否存在并属于当前用户所有
> > -G file  file是否存在并且默认组和当前用户相同
> > file1 -nt file2 file1是否比file2新
> > file1 -ot file2 file1是否比file2旧
> > ```
> 
> ##### 7. 复合条件
> > ```
> > [ condition1 ] && [ condition2 ]
> > [ condition1 ] || [ condition2 ]
> > ```
> 
> ##### 8. case条件，类似C语言、Go语言中的switch，格式如下(分号注意哦，不能省略)
> > ```
> > case val in
> > pattern1 | pattern2) 
> >     cmd1;;
> > pattern3) 
> >     cmd2;;
> > * ) 
> >     default;;
> > esac
> > ```
> > ex: 打印fa | fancy
> > ```
> > val1="fancy"
> > 
> > case ${val1} in
> >     "fc")
> >         echo "fc";;
> >     "fa" | "fancy")
> >         echo "fa | fancy";;
> >     *)  
> >         echo "default";
> > esac
> > ```

#### 5. 循环命令 for
> ```
> for val in list
> do
>     cmd
> done
> ```
> ##### 1. 读取列表中的值
> > ```
> > for val in fc0 fc1 fc2 fc3 fc4 
> > do
> >     echo ${val}
> > done
> > 
> > 会打印出
> > fc0
> > fc1
> > fc2
> > fc3
> > fc4
> > ```
> > shell会自动以空格来划分列表
> 
> ##### 2. 当列表中出现单引号，需要将其转义，或用双引号来定义用到单引号的词，不然会出错
> > ```
> > for val in fc0 fc\'1 fc2 "fc'3" fc4
> > do
> >     echo ${val}
> > done
> > 
> > 会打印出
> > fc'1
> > fc2
> > fc'3
> > fc4
> > ```
> 
> ##### 3. 当列表的词组中出现空格时，需要用双引号来定义该词
> > ```
> > for val in "fc0 fc1" fc2 fc3 fc4 
> > do
> >     echo ${val}
> > done
> > 
> > 会打印出
> > fc0 fc1
> > fc2
> > fc3
> > fc4
> > ```
> 
> ##### 4. shell允许你使用命令替换来当做列表的值
> > ```
> > for val in $(cat test.sh)
> > do
> >     echo ${val}
> > done
> > 
> > 这里的test.sh是当前目录下的一个文件，该段程序会输出test.sh里的所有分割出来的词
> > $()就是之前讲过的命令替换
> > ```
> 
> ##### 5.修改默认字段分隔符
> 之前说过shell会默认把空格当做分割符来分割列表，其实还有两个，制表符和换行符  
> shell用过环境变量IFS来指定换行符，所以在程序中可以按照需要改成我们想要的分隔符  
> 但是在修改之前最好把之前的值保存下来，用完之后恢复到默认状态   
> > ```
> > vim file输入以下字符
> > fc0 
> > fc1 fc2 
> > fc3 fc4 
> > fc5
> > ```
> > ```
> > IFS_OLD=${IFS}
> > IFS=$'\N'
> > for val in $(cat file)
> > do
> >     echo ${val}
> > done
> > IFS=${IFS_OLD}
> > 
> > for val in $(cat file)
> > do
> >     echo ${val}
> > done
> > 
> > 程序会打印出
> > fc0 
> > fc1 fc2
> > fc3 fc4
> > fc5
> > fc0
> > fc1
> > fc2
> > fc3
> > fc4
> > fc5
> > 修改过IFS的那个循环会以换行符作为分隔符
> > 恢复默认后的那个循环会以空格和换行作为分隔符
> > ```
> 
> ##### 6.c语言风格的for格式
> > ```
> > for (( i=1; i <= 10; i++ ))
> > do
> >     echo ${i}
> > done
> > ```
> 

#### 6. 循环命令 while，until
> ```
> var=10
> while [ ${var} -gt 10 ]
> do
>     echo ${var}
>     var=$[ ${var} - 1 ]
> done
> ```
>
> ```
> var=1
> until [ ${var} -gt 10 ]
> do
>     echo ${var}
>     var=$[ ${var} + 1 ]
> done
> ```

#### 7. 命令行参数
> 1. ${num} 代表第几个参数
> 2. $# 代表参数的个数
> 3. ${!#} 代表最后一个参数
> 4. $* 代表所有参数的整体，不可遍历单个参数
> 5. $@ 代表所有参数，可遍历单个参数
> 6. $$ 代表当前进程PID
> 7. 完整的命令行选项和参数处理代码
> > ```
> > while getopts ab:c opt
> > do
> >     case "$opt" in
> >         a)  echo -n "opt -a, cur pos is ${OPTIND}";;
> >         b)  echo "opt -b, with value ${OPTARG}";;
> >         c)  echo "opt -c";;
> >         *)  echo "unknow opt: $opt";;
> >     esac
> > done
> > 
> > echo ${OPTIND}
> > shift $[ ${OPTIND} - 1 ]
> > count=1
> > for para in "$@"
> > do
> >     echo "para #${count}: ${para}"
> >     count=$[ ${count} + 1 ]
> > done
> > ```

#### 8. 重定向
> ```
> 0 标准输入
> 1 标准输出
> 2 标准错误
> ```
> 1. 错误重定向
> > ```
> > [cmd] 2> err.log
> > ```
> 2. 错误和数据分别重定向
> > ```
> > [cmd] 1> data.log 2> err.log
> > ```
> 3. 错误和数据分别追加重定向(不会覆盖)
> > ```
> > [cmd] 1>> data.log 2>> err.log
> > ```
> 4. 错误和数据重定向到同一文件
> > ```
> > [cmd] &> err.log
> > ```
> 5. 在脚本中永久重定向，加入下面两句
> > ```
> > exec 1> data.log
> > exec 2> err.log
> > ```
> > 然后需要错误重定向的语句要修改成这样
> > ```
> > echo "this is a err" >&2
> > ```
