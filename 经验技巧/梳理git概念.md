---
title: git两大重要概念——仓库和分支
date: 2017-04-05 22:09:02
tags:
categories: git
---

参考文章：

[Git 工作区、暂存区和版本库](http://www.runoob.com/git/git-workspace-index-repo.html)

[Git 图解、常用命令和廖雪峰教程笔记总结](https://segmentfault.com/a/1190000008617626)

## 仓库

git 版本控制中最重要的是一个概念是**仓库**

仓库包括两个部分：**工作区** 和 **版本库**。

版本库又分为两个部分：**暂存区** 和 **分支区**。

<!--more-->

**工作区（workplace）**：就是你在电脑中看到的目录，在这个目录中装着你的代码

**版本库**：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

**暂存区（index/stage）**：一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。

**本地仓库（local respository）**：包括了版本库和工作区两个部分

**远程仓库（remote respository）**：包括版本库和工作去两个部分



用图片来表示这几个关系就是：

![git_workpalce](https://cdn.ihewro.com/img/git_workpalece.jpg)

----

## 分支

git 版本控制中更重要的一个概念是**分支**

分支概念有点类似与windows 10 下的多个桌面工作区，彼此之间的工作互不干扰。但是必要的时候，可以将某个工作去的窗口拖到另一个工作区下面。

如上图所示，

1. 此时的`HEAD`实际是指向master 分支的一个"游标"。所以图示的命令中出现 HEAD 的地方可以用 master 来替换。
2. 图中的 objects 标识的区域为 Git 的对象库，实际位于 ".git/objects" 目录下，里面包含了创建的各种对象及内容。

#### 执行`git add`命令的时候

暂存区的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。

#### 执行`git commit`命令的时候

暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。

