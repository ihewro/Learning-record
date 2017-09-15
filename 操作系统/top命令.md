---
title: top命令
date: 2017-03-19 22:06:20
tags:
---

##  界面信息说明

### 界面

```basic
top - 21:48:39 up  8:57,  2 users,  load average: 0.36, 0.24, 0.14
Tasks: 322 total,   2 running, 320 sleeping,   0 stopped,   0 zombie
%Cpu(s):  5.0 us,  1.7 sy,  0.0 ni, 93.0 id,  0.0 wa,  0.3 hi,  0.0 si,  0.0 st
KiB Mem:   1010504 total,   937416 used,    73088 free,    23708 buffers
KiB Swap:  1046524 total,   280708 used,   765816 free.   365556 cached Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND      
 8096 root      20   0  320624  38508  21192 S  1.7  3.8   0:41.03 Xorg         
13536 tabalt    20   0  697336 104272  56776 S  1.7 10.3   0:08.29 gnome-langu+ 
 9426 tabalt    20   0 1213228  72976  16860 S  1.0  7.2   2:07.27 compiz       
  197 root      20   0       0      0      0 S  0.3  0.0   0:36.13 kworker/0:2  
 1009 root      20   0  303112   3392   1500 S  0.3  0.3   0:00.93 polkitd      
 9670 tabalt    20   0  325932   4300   2256 S  0.3  0.4   0:40.27 vmtoolsd     
14016 root      25   5   43940   2408   2000 S  0.3  0.2   0:01.12 http         
14149 tabalt    20   0  591180  19504  12820 S  0.3  1.9   0:00.45 gnome-termi+ 
    1 root      20   0   33648   1972    744 S  0.0  0.2   0:01.79 init         
    2 root      20   0       0      0      0 S  0.0  0.0   0:00.00 kthreadd     
    3 root      20   0       0      0      0 S  0.0  0.0   0:02.80 ksoftirqd/0  
    4 root      20   0       0      0      0 S  0.0  0.0   0:00.00 kworker/0:0  
    5 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 kworker/0:0H 
    7 root      20   0       0      0      0 S  0.0  0.0   0:05.55 rcu_sched    
    8 root      20   0       0      0      0 R  0.0  0.0   0:03.43 rcuos/0      
    9 root      20   0       0      0      0 S  0.0  0.0   0:00.00 rcuos/1      
   10 root      20   0       0      0      0 S  0.0  0.0   0:00.00 rcuos/2 
```

<!--more-->

### 信息详解

#### 第一行显示服务器概况

```ba
top - 21:48:39 up  8:57,  2 users,  load average: 0.36, 0.24, 0.14
       /         /        /                \
   当前时间  运行时长   当前登录用户数  平均负载（1分钟、5分钟、15分钟）
```

显示服务器运行多长时间，当前有多少个用户登陆，服务器负荷情况等等。使用`uptime`命令可以获得同样的结果。

- 平均负载的值越小代表系统压力越小，越大代表系统压力越大。通常，我们以**最后一个数值，也就是15分钟内的平均负载**作为参考来评估系统的负载情况。

