---
categories:
 - Linux
date: 2020-05-14T08:33:04+08:00
description: "Linux 性能"
tags:
 - Linux
 - performance
title: "Linux 性能"
url: "/linux/linux_performance/"
---

# 1. CPU 平均负载
> ### 1. 单位时间内, 活跃的进程数  
> > 活跃的进程是指处于可运行状态和不可中断状态的进程  
> > 可运行状态进程是指正在使用 cpu 和正在等待 cpu 的进程  
> > 不可中断状态进程是指正在等待某些操作完成的进程, 比如等待 i/o 响应  
>
> ### 2. uptime, top 等命令显示的 load average 平均负载解读
> ```
> watch -d uptime
> ```
> > 最直观的理解就是, 当这个值等于你机器 cpu 数量的时候, 正好跑满 cpu  
> > 例子: 
> > > 比如你的机器有 1 个 cpu, 那平均负载如果是 1 说明正好跑满, 大于 1 说名过载了, 小于 1 说明有空闲  
> > > 再比如你的机器有 4 个 cpu, 那这个临界值就是 4  
> > > uptime, top 会显示 3 个值, 代表过去 1, 5, 15 分钟的平均负载 
> 
> > 机器 cpu 个数查看方法:
> > > ```
> > > cat /proc/cpuinfo
> > > ```
> 
> > 平均负载和 cpu 使用率的区别
> > > 由于平均负载包含了等待 cpu 和等待 i/o 操作的进程, 所以平均负载注定和 cpu 使用率不会完全一一对应  
> > > 比如 i/o 密集型进程, cpu 使用率不会太高, 但是平均负载会高  
> > > 比如 cpu 密集型进程, cpu 使用率高, 平均负载也高  
---
# 2. stress-ng 压力测试工具
> ### 安装
> ```
> apt install stress-ng
> yum install stress-ng
> ```
> 
> ### 使用
> > ```
> > stress-ng -c 2 -t 20
> > ```
> > 模拟 cpu 密集型进程, 20 秒内 2 个进程跑满 cpu
>
> > ```
> > stress-ng -i 4 -d 1 -t 60
> > ```
> > 模拟 i/o 密集型进程, 60 秒内 4 个 workers 持续刷新内存到磁盘
>
> > ```
> > stress-ng -c 8 -t 20
> > ```
> > 模拟大量进程, 模拟 8 个进程跑满 cpu
---
# 3. 性能监测工具, sysstat 包
> ### 安装
> > ```
> > apt install sysstat
> > yum install sysstat
> > ```
### mpstat  
> ###### 监测 cpu 性能
> > mpstat -P ALL 5  
> > 持续间隔 5 秒输出 cpu 相关统计数据   
>
> > mpstat -P ALL 5 2   
> > 间隔 5 秒输出 cpu 相关统计数据, 一共 2 组, 并计算平均值   
>
> > ```
> > CPU:     处理器 ID  
> > %usr:    用户态进程 cpu 使用时间比  
> > %nice:   高优先级进程 cpu 使用时间比  
> > %sys:    内核态进程 cpu 使用时间比, 不包括硬中断和软中断  
> > %iowait: 硬盘 i/o 等待时间比  
> > %irq:    硬中断时间比  
> > %soft:   软中断时间比  
> > %steal:  虚拟机下, cpu 非自愿等待时间比  
> > %guest:  运行虚拟机的时间比   
> > %gnice:  高优先级虚拟机的时间比   
> > %idle:   出去等待 i/o 操作所有空闲时间比  
> > ```
### pidstat
> ###### 监测进程性能
> > pidstat -u  
> > 监测各进程 cpu 使用情况
> > ```
> > UID:    用户 ID  
> > PID:    进程 ID  
> > %usr:   进程在用户空间使用 CPU 时间比
> > %system:进程在内核空间使用 CPU 时间比
> > %guest: 进程在虚拟机使用 CPU 时间比
> > %wait:  进程等待执行时间比
> > %CPU:   进程使用 CPU 总时间比
> > CPU:    进程在哪个 CPU 上执行
> > Command: 进程执行的命令
> > ```
>
> > pidstat -r  
> > 监测各进程 内存 使用情况
> > ```
> > UID:      用户 ID  
> > PID:      进程 ID  
> > minflt/s: 任务每秒发生的次要错误, 这些错误不需要从磁盘中加载页
> > majflt/s: 任务每秒发生的主要错误, 这些错误需要从磁盘中加载页
> > VSZ:      虚拟内存使用大小(单位k)
> > RSS:      常驻内存, 即非交换区物理内存使用大小(单位k)
> > %MEM:     进程使用可用内存占比
> > Command: 进程执行的命令
> > ```
>
> > pidstat -d  
> > 监测各进程 i/o 使用情况
> > ```
> > UID:      用户 ID  
> > PID:      进程 ID  
> > kB_rd/s:  每秒从磁盘读取的数据大小(单位k)
> > kB_wr/s:  每秒写入或将要写入磁盘的数据大小(单位k)
> > kB_ccwr/s:每秒被取消写入磁盘的数据大小(单位k)
> > iodelay:  阻塞 i/o 的延迟时间
> > Command: 进程执行的命令
> > ```
>
> > pidstat -w  
> > 监测各进程 上下文切换 情况
> > ```
> > UID:      用户 ID  
> > PID:      进程 ID  
> > cswch/s:  每秒主动上下文切换的数量(task 需要的资源没有准备好, 那么它会主动发起上下文切换)  
> > nvcswch/s:每秒被动上下文切换的数量(task 时间片用完, 被动放弃 cpu)  
> > Command:  进程执行的命令
> > ```
>
> > pidstat -v  
> > 监测各进程 内部 信息
> > ```
> > UID:      用户 ID  
> > PID:      进程 ID  
> > threads:  与当前 task 关联线程数量
> > fd-nr:    与当前 task 关联文件描述符数量
> > Command:  进程执行的命令
> > ```
>
> > pidstat -t  
> > 以线程为单位进行 cpu 监测, 内容和 pidstat -u 相似, ID 改成了线程 ID
> > ```
> > TGID: 线程组 ID
> > TID:  线程 ID
> > ```
>
> > pidstat -[opt] -p [pid]  
> > 查看某个具体的进程的信息
>
> > pidstat -[opt] 5 1
> > 每 5 秒输出一次, 一共 1 组数据报表


---
# 20. Linux 性能图谱
![Linux 性能](/img/Linux_performance.png)
