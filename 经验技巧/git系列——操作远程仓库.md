---
title: git系列——操作远程仓库
date: 2017-04-05 14:19:28
tags:
---

> 参考文章
> [Git远程操作详解](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)
> [Git 参考手册](http://gitref.org/zh/remotes/#fetch)
>
> [Git 图解、常用命令和廖雪峰教程笔记总结](https://segmentfault.com/a/1190000008617626)
>
> [Git 真正理解 git fetch, git pull 以及 FETCH_HEAD](https://ruby-china.org/topics/4768)

操作远程仓库的一般过程是：
1. 添加远程仓库地址 或者 克隆远程仓库
2. 拉取远程仓库信息获更新本地仓库
3. 推送本地仓库内容至远程

对应的命令是：
* git remote / git clone 
* git fetch / get merge / get pull
* git push

下面分别对上面的四个过程，6个命令，进行总结。

![git_workpalce_2](https://cdn.ihewro.com/img/git_workpalce2.jpg)

<!--more-->

## 一、git remote / git clone

操作远程仓库的第一步，有两种方式，这两种方式对应了不同的工作环境的情况：

1. 添加远程仓库地址 ：本地已经有了git仓库了，这时候需要同步到远程，此时使用`git remote`
2. 克隆远程仓库：本地没有git仓库，直接从远程拉下来，此时使用`gir clone`


### git remote

Git要求，每个远程仓库都必须指定一个仓库名称，便于区别。`git remote`正是用来管理远程仓库名称的一个命令。

> git remote  列出远端别名

* 没有任何选项，Git会列出本地仓库连接的远程仓库的名称

如果你的本地仓库是`git clone`拉取下来的，Git会默认将远程仓库取名为“origin”。

```ruby
$ git remote
origin
```

* 加上`-v`选项，你还看可以看到每个别名的实际链接地址

```ruby
git remote -v
origin	git@git.coding.net:ihewro/test.git (fetch)
origin	git@git.coding.net:ihewro/test.git (push)
```

在此你看到了该链接两次，是因为 Git 允许你为每个远端仓库添加不同的推送与获取的链接，以备你读写时希望使用不同的协议。

> git remote add 让本地仓库链接到远程仓库

命令的格式是：

```ruby
git remote add <name> <url>
```

`<name>`是给远程仓库取名，如果该选项为空，则取默认名称“origin”。

> git remote rm 取消与远程仓库的链接

命令的格式是：

```ruby
git remote rm <name>
```



### git clone

使用`git clone`意味着，你在本地没有建立仓库，直接从远程仓库拉取下来。

它的一般格式为：

```ruby
git clone <版本库的网址> <本地目录名>
```

`<本地目录名>`如果省略，则默认为远程仓库的名称。

`<版本库的网址>`支持多种协议。除了HTTP(s)以外，还支持SSH、Git、本地文件协议等。



## 二、git fetch / get merge / get pull

### git fetch

远程仓库已经更新，但是本地仓库却没有同步更新，这时候，需要使用`git fetch`拉取到本地。

当本地仓库与远程仓库链接之后（通过`git remote add`或者`git clone`），本地存储了**本地仓库分支**和**本地远程分支**两个信息。

* 本地仓库分支在你每次`git add + git commit`时候会修改信息
* 本地远程分支并不是实时更新变化的，而是固定不变的，只有在你使用了`git fetch`之后才会更新。

`git fetch`作用就是**通过网络更新本地存储远程分支**。

命令格式是：

```ruby
git fetch <远程仓库名称>
```

### git merge

然后你可以执行 `git merge [alias]/[branch]` 将远程仓库上的任何更新合并到**你的当前分支**。

如果远程仓库（origin）的master分支有更新，本地仓库现在的分支是`dev`，使用

```ruby
git merge origin/master
```

会把更新的内容合并到`dev`分支上面。

### git pull

 `git pull` = `git fetch ` + `git merge` 

命令格式为：

```ruby
git pull <远程仓库名> <远程分支名>:<本地分支名>
```

意思为，更新本地存储的远程仓库的某个分支 并 与本地的某个分支合并。

* 省略`<远程仓库名> `前提是本地仓库只链接了一个远程仓库

* 省略`<本地分支名>`，默认与**本地仓库的当前分支**合并。这个命令等同于

```ruby
git fetch <远程仓库名>
git merge <远程仓库名>/<远程分支名>
```
* 省略`<远程分支名>:<本地分支名>`前提是已经建立了远程仓库的某个分支**与当前分支的链接关系**（追踪关系）。

```ruby
git branch --set-upstream-to=origin/<分支> 
```

比如，在`git clone`的时候，所有本地分支默认与远程主机的同名分支已经建立了追踪关系.


## 三、git push

命令格式是：

```ruby
git push <远程仓库名> <本地分支名>:<远程分支名>
```

**注意：**

>  分支推送顺序为：<本地分支名>:<远程分支名>

>  分支拉取顺序为：<远程分支>:<本地分支>

* 省略`<远程仓库名> `前提是本地仓库只链接了一个远程仓库
* 省略`<本地分支名>`则表示**删除指定的远程分支**，因为这等同于推送一个空的本地分支到远程分支。
* 省略`<远程分支名>`则默认推送至**与当前分支同名的远程分支**，如果该远程分支不存在，则会被新建。
* 省略`<远程分支名>:<本地分支名>`前提是已经建立了远程仓库的某个分支**与当前分支的链接关系**（追踪关系）。

