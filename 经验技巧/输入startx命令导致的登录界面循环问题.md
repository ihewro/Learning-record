---
title: deepin 15.4 输入startx命令导致的登录界面循环问题
date: 2017-05-12 21:34:19
tags:
categories: linux
---

方法：

1.  ctrl + alt +F3  进入tty3
2. cd ~
3. rm -rf .Xaut*
4.ctrl + alt +F7 回到登录界面，就可以登录了～

来源：http://blog.csdn.net/ww_bin/article/details/46461675
