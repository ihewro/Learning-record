---
title: hexo博客多设备同步写作
date: 2017-04-06 15:09:44
tags:
---

首先需要明确的一点是，`hexo g -d` 会将**publc文件夹**中的本地文章上传到github仓库的`master`分支（取决与`deploy`的branch 填写的值），而不是**我们的整个文件夹**。

其次我们写静态博客的文件夹下面是没有**.git**文件夹的，也就是说，我们的博客文件夹下面并没有`git init`，并不是git仓库。

<!--more-->

```ruby
$ ls -a
.  ..  _config.yml  .gitignore  node_modules  package.json  scaffolds  source  themes
```

那github上面的如何知道我们git commit的记录呢？

当我们执行了`npm install hexo-deployer-git --save`之后，目录下面会有一个**.deploy_git**文件夹，我猜想hexo 是通过 **.deploy_git**文件夹 将 **publc**文件夹的文章上传至github。

----

好了，上面的话，是我个人帮助自己理解hexo的运行原理的一些思考。

关于如何多设备同步hexo博客，分为两个部分：在**本设备**和**其他设备**

原理是这样的：

> 本设备

1. 在hexo文件夹中建立Git仓库，链接到远程仓库。
2. 新建一个分支`hexo`，把本地仓库的所有文件上传到github的`hexo`分支上面（根据`.gitignore`文件决定哪些文件会被上传）

**新建的`.gitignore`文件内容**

```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
.deploy_git
```



> 其他设备

1. 克隆github上面的hexo分支的所有内容
2. 安装hexo 的必要插件（根据package.json文件中内容）

---

详细的讲每个过程的步骤就是：

> 本设备

1. ```ruby
   git init
   git remote add <github仓库地址>
   ```

2. ```ruby
   git checkout -b hexo //创建hexo分支，并且切换至该分支
   ```

3. ```ruby
   git add.
   git commit -m "update"
   ```

4. ```ruby
   git push -u origin hexo
   ```





> 其他设备

1. ```ruby
   git clone <github仓库地址> <本地仓库目录名称>
   //每次在另一个设备写文章，从github上面拉取hexo分支
   ```

2. ```
   npm install //安装必要插件
   ```

3. ```ruby
   npm install hexo-deployer-git --save //安装hexo-deployer-git工具
   ```

---

OK~一切搞定。