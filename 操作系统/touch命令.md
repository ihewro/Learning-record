---
title: touch命令
date: 2017-03-16 09:24:28
tags:
categories: linux命令
---

### 命令格式

touch [OPTION]... FILE...

### 命令功能

一是用于把**已存在的文件**的时间标签更新为系统当前的时间，它们的数据将原封不动的保留下来；

二是用来**创建空文件**。

<!--more-->

### 命令选项

| 选项                 | 含义                                       |
| ------------------ | ---------------------------------------- |
| `-t`               | 使用指定的日期时间。**参数的时间格式**：  [[CC]YY]MMDDhhmm[.SS]（如：201703181047.44） |
| `-d`               | 使用指定的日期时间。                               |
| `-r`               | **参数：**<参考文件或者目录> <指定文件或者目录>  把指定的文件或者目录的日期时间，统统设成和参考文件或者目录的日期相同 |
| `-c`/`--no-create` | 不建立任何文档                                  |

