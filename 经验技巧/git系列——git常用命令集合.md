---
title: git系列——git常用命令集合
date: 2017-04-20 14:58:39
tags:
categories: git
---

这篇文章不会详细讲解每个指令，只是列举常用的指令，方便使用和查找。

<!--more-->
### 初始化或者获取仓库

```bash
git init #把当前文件夹初始化成一个本地仓库
git clone <远程仓库地址> [文件夹名称] #拉取一个远程仓库并给本地文件夹取名
```

### 文件修改与回退

```bash

```

### [远程库操作](https://wiki.ihewro.com/2017/04/05/git%E7%B3%BB%E5%88%97%E2%80%94%E2%80%94%E6%93%8D%E4%BD%9C%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/)

```bash
git remote -v #查看远程仓库
git remote add <远程仓库名称> <远程仓库地址> #链接某个远程仓库并给远程仓库取名
git remote rm <远程仓库名称> #删除某个远程仓库
git fetch <远程仓库名称> #拉取远程仓库的更新，更新本地的所有远程分支
git merge <远程仓库名称>/<远程仓库的分支> #将本地远程分支的更新合并到本地的当前分支
git pull <远程仓库名> <远程分支名>:[本地分支名] #拉取远程仓库的某个分支的更新，更新本地的远程分支，并合并到本地的某个分支
git push <远程仓库名> <本地分支名>:[远程分支名] #推送本地的分支更新到远程仓库的某个分支
```



