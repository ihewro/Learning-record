---
title: git系列——git30分钟快速入门
date: 2016-11-11 23:10:09
tags:
categories: git
---

git到底难不难？很多次被git吓到没有深入学习，但是git只是编程的一件额外的协助功能，所以肯定不会很难，学习了git教程之后，写下这部分内容，以期备用和帮助到你。当你一步步读完全文，并且入门git的时候，你会发现git的强大之处。所以，现在开始。（windows 系统环境）


<!--more-->


### **git简介**

你可能使用过github，git与github相比如球与球场的关系。git是版本控制工具，你每次更改代码都会被记录。而github桌面版正是采用了这种机制的一个平台。git不仅在github 桌面版应用，在一些IDE中也有集成，比如visual studio 2015中。但是熟悉git基本操作，可以让我们脱离这些集成git软件的限制，让我们所以的工作都在git的有效管理下。

### **下载git并初步认识**

[点击官网下载](https://git-scm.com/downloads)

安装完成之后在开始菜单里找到“Git”目录下应该有三个程序：`git Bash` / `git CMD` / `git GUI`。点击任何一个文件夹右键菜单应该都会有这三个选项。

* git Bash : git 命令行工具，我们接下来的大部分命令操作都将在此进行
* git CMD ：git 命令窗口，事实上与windows 提供的 CMD并没有区别，基本不需要使用
* git GUI： git 的图形化界面，使我们可以在不使用命令行情况下而点击几个按钮使用git版本控制，如add、commit 等。但是纯英文的界面让我更喜欢命令行的操作

### **设置用户信息**

恩恩，给操作git的操作者一些信息吧，这些信息将会在`git bash`某些操作中显示。（当然不设置也行，每次提交都是unknown...）

```ruby
$ git config --global user.name "ihewro" //给自己起个用户名
$ git config --global user.email  "abc@gmail.com" //填写自己的邮箱

```

### **创建仓库**

什么是仓库？英文名repository。在github同样可以看到这个名词。仓库包括两个部分：**版本库**和**工作区**。

工作区就是你所创建的代码文件夹。

版本库就是自动创建、默认隐藏的文件夹`.git`目录，版本库保存了工作区每个文件的修改记录，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。版本库又分为：`stage（暂存区）`和`分支区`。默认创建了`master`分支。

![0.jpg][1]
现在开始创建一个仓库。

在任何位置新建一个文件夹，取名为`github使用`。右键文件夹名称，点击`Git bash Here`，你会看到一个输入命令行的窗口。

输入命令：`git init`，仓库建立成功。

### **在仓库中添加文件**

我们建立一个空仓库，目的是在里面添加各种各样的文件，进行各种各样的代码修改，然后让git版本控制软件把我们的更改记录下来。
所以，我们开始在**仓库目录下** 名称为“readme.txt”文件吧。（推荐使用notepad++替代windows自带的记事本，完全免费，支持代码高亮，体积很小）
* 先使用 `git add readme.txt`命令行，把readme.txt文件修改添加到暂存区。正确的话是没有提示信息的。
* 再使用 `git commit -m "这里面是一些文字说明"` 命令行，这行命令是一次性提交暂存区的所有修改并保存到当前分支。正确的话会

说明：`git add`可以重复使用，一些命令代表一些小修改，`git commit` 代表了上面所有小修改的总结，即一次大修改

### **版本回退**

我们不断创建，不断想修改，每次大修改都会commit一次。这样我们的git里面就会保存很多次我们的修改记录。
首先使用`git log`命令可以查看我们commit的历史记录。如果想看更加简略的历史记录信息，请输入命令`git log --pretty=oneline`

```ruby
$ git log --pretty=oneline
26771120ea1ecf2713d050d6c36b92a37c485bc0 add onoe line
4276b844537928658f27ae287a623b733a5591ec merge bug fix 101
d6b2123d6966c9af215fa0f70dd9e3fcac3cf49b fix bug 101
5333fde1e6199ad1bcef25e42691231afdd5aff3 confict fixed
```

就像上面这样。上面每一串数字与字符的组合（如：`26771120ea1ecf2713d050d6c36b92a37c485bc0`）叫做版本号（commit ID）

版本回退有三种不同的情况：
* 修改了文件，并没有`add`
* 修改了文件，已经`add`，但没有`commit`
* 修改了文件，已经`add`，并且`commit`

1. 使用命令`$ git checkout -- readme.txt`，即把readme.txt文件在工作区的修改全部撤销
2. 先使用命令`$ git reset HEAD readme.txt`，即可以把暂存区的修改撤销掉（unstage），重新放回工作区。然后转换成第一种情况，使用命令行撤销工作区修改。
3. 使用`$ git reset --hard HEAD^`表示回退到上一版本。或者直接使用版本号如：`$ git reset --hard 3628164` 版本号不必写全，会自动匹配版本号。如果你已经回退到上一个版本号，忘记了之前的最后一个版本号，可以使用`$ git reflog`命令，这个命令会输出你的每一次命令记录。可以找到你的回退版本号。

### **操作远程仓库**

当然，我们本地建立仓库，更主要的是与远程仓库同步，跨平台合作更方面。这里以更加常用的github为例。

1. **获取公用密钥**

* 现在本地获取git公用密钥，然后填到github——setting——SSH keys——New SSH key 

```ruby
ssh-keygen -t rsa -C "abc@gmail.com" //填写email地址，然后一直“回车”ok
```

然后打开本地..\.ssh\id_rsa.pub文件。此文件里面内容为刚才生成的密钥。然后把该密钥复制到github的setting/ssh中，点击打开页面的add SSH key按钮，title任意，把key值复制进去。

经过上述配置，你的Git应该可以通过SSH连接GitHub服务器了，可以测试一把（配置完SSH key后，就表示本地能操作该用户下的库，能提交代码了）：

```
ssh -T git@github.com
```

提示像我这样：

```
Hi ihewro! You've successfully authenticated, but GitHub does not provide shell access. 那就说明连接成功了。
```

2. **创建远程仓库**

github上面点击`New Respository`

![2016-11-12_145315.png][2]

3. **克隆远程仓库**

* 先fork
* 在你的工作区打开`Git Bash`，使用命令`git clone git@github.com:ihewro/github-.git`，把`git@github.com:ihewro/github-.git` 替换成相应仓库的SSH地址。

4. 本地与远程仓库同步操作

第一次把本地仓库内容同步至github仓库，使用命令`$ git push -u origin master`,之后同步只需要使用命令`$ git push origin master`。


### **最后说明**

* 本文只是一个入门型文章，更多细节内容，可以学习这个教程：[git教程 by 廖雪峰](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
* 本文会根据我的学习程序做一定程度的修正和更新。如果你更喜欢图形界面操作，windows下可以使用：`GitKraken`。一些IDE，如VS ， github 桌面版 都集成了 git 系统，我们可以直接使用界面操作，而避免命令行的繁琐。
* 本文内容参考除以上提到链接，还有：
  [初学git：用git bash往github push代码](http://www.cnblogs.com/zichi/p/4703999.html)
  [git干货系列：（三）我提交错了我想撤销或者回退版本](http://www.jianshu.com/p/f0d6a5a4325f)


[1]: https://www.ihewro.com/usr/uploads/2016/11/3339818800.jpg
[2]: https://www.ihewro.com/usr/uploads/2016/11/3816137835.png