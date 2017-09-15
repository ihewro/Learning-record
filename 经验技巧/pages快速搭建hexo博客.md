---
title: github pages快速搭建hexo博客
date: 2016-11-25 23:12:56
tags:
---

githubpage除了在国内有些地区访问速度不好，还是有很多优点的，比如无限流量，无限空间。

静态博客框架有很多，hexo个人认为更简单容易上手，因为有官方中文文档。

hexo原理就是通过本地一个程序扫描`source`目录内容，建立索引，根据你 `theme` 文件夹的主题生成页面到 public 文件夹。然后通过`git`方式把`pubilc`文件夹内容传到github。github pages能够解析并且展示出来。

演示地址：<http://ihewro.top>

<!--more-->

----

## 安装nodejs 和 git 和cmder

* [nodejs](https://nodejs.org/en/):进入官网点击`首页绿色的左边的按钮`就会自动下载，一键傻瓜式安装。配套会自动安装npm
* [git](https://git-scm.com/):点击`downlode` 下载自动安装。安装完成，会有一个`git`文件夹。`git bash`就是最重要的一个命令窗口
* [cmder](http://cmder.net/):如果你不喜欢git的命令行窗口，windows环境下推荐使用`cmder`命令行工具，美观，强大，完整版支持git命和Linux命令，完全可以替代`git` + `windows自带的cmd`。（本文步骤在`cmdeer`上操作）

## git 连接远程仓库

因为本地仓库要同步，所以必须本地连接github仓库。方法见  [30分钟git 快速入门-操作远程仓库](https://www.ihewro.com/archives/469/)

## 创建github仓库

官方说明
> Head over to GitHub and create a new repository named username.github.io, where username is your username (or organization name) on GitHub.

> If the first part of the repository doesn’t exactly match your username, it won’t work, so make sure to get it right.

翻译过来就是：

> 仓库一定要取名为`username.github.io` 比如我就是`ihewro.github.io`。否则不会正常工作！

## 克隆仓库到本地文件夹

比如我：
本地新建了一个文件夹，取名为`blog`。打开`cmder（命令行工具）`。

`git clone <仓库的ssh地址>`

> 例如：
```
λ git clone git@github.com:ihewro/ihewro.github.io.git
Cloning into 'ihewro.github.io'...
warning: You appear to have cloned an empty repository.
```

这样提示，证明已经成功clone了！

## 全局安装hexo

```
$ cnpm install -g hexo-cli
```

输入 `hexo -v` 查看是否成功
```
λ hexo -v
hexo-cli: 1.0.2
os: Windows_NT 10.0.14393 win32 x64
http_parser: 2.7.0
node: 6.9.1
v8: 5.1.281.84
uv: 1.9.1
zlib: 1.2.8
ares: 1.10.1-DEV
icu: 57.1
modules: 48
openssl: 1.0.2j
```

OK！

## 在当前文件夹部署hexo

上一条命令只是把hexo安装在系统的一个公用文件夹里，你可以在系统任何位置创建hexo。在**当前文件夹**（比如我：`ihewro.github.io`文件夹）部署hexo命令：

```
<!--把hexo部署到当前文件夹-->
hexo init

<!--根据hexo的`package.json`配置文件安装必要的模块-->
cnpm install
```
到这步结束，hexo本地就安装完成了！


## 本地预览网站

步骤是：（清除一开始的静态文件）——生成静态文件——启动本地服务

* 仅仅两步骤，不需要`push`等其他指令，非常方便
* `（清除一开始的静态文件）`一般不需要操作，仅仅在出现错误时候，可以尝试先清除旧的静态文件

1. 清除一开始的静态文件（第一次当然不需要啦！）

```
hexo clean
```

2. 生成静态文件


```
hexo generate
hexo g
```
上面两个均可，任选一个即可！

选项：（是跟在指令后面的）

| 选项               | 描述          |
| :--------------- | :---------- |
| `-d`, `--deploy` | 文件生成后立即部署网站 |
| `-w`, `--watch`  | 监视文件变动      |

3.启动本地服务

```
hexo server
hexo s
```
上面两个均可，任选一个即可！

| 选项               | 描述              |
| :--------------- | :-------------- |
| `-p`, `--port`   | 重设端口            |
| `-s`, `--static` | 只使用静态文件         |
| `-l`, `--log`    | 启动日记记录，使用覆盖记录格式 |



## 部署网站到github pages

步骤是：本地配置部署信息——（清除一开始的静态文件）——生成静态文件——部署网站

1. 本地配置部署信息

打开`_config.yml`文件，在deploy部分填写配置信息，把repository值设置为刚刚复制好的ssh地址。

```
deploy:
  type: git
  repo: <your-github-repo-ssh-address>
  branch: master
```
**冒号后面必须有一个空格**


2. 清除一开始的静态文件（第一次当然不需要啦！）

3. 生成静态文件

4. 部署网站
```
hexo deploy
hexo d
```

选项:
| 参数                | 描述           |
| :---------------- | :----------- |
| `-g`,`--generate` | 部署之前预先生成静态文件 |

如果上面这个步骤报错：`ERROR Deployer not found : github`，尝试安装`hexo-deployer-git`:

```
cnpm install hexo-deployer-git --save
```

## 文章相关

### 新建文章

```
$ hexo new [layout] <title>
$ hexo n [layout] <title>
```

* [layout]是指你的文章布局。默认有三种`post`（文章页面）、`page`（独立页面）、`draft`（草稿页面），在`scaffolds`文件夹里存储了就是这些模板和布局
* 执行命令后，会在对应的文件夹中生成.md文件。
* 在.md 文件的分界线下面使用markdown语法书写文章即可！

有这样几个问题解决方法：
1. **添加分类** ：默认布局里面没有`category`，打开scaffolds/post.md文件，在tages:上面加入`categories:`,保存后，重新执行`hexo new [layout] <name>`命令，会发现新建的页面里有categories:项了。
2. **添加标签** ：有两种方法：
    1. ```tages: [标签1,标签2,...标签n]```
    2. ​
``` 
 tages: 
- 标签1
- 标签2
...
- 标签n
```

文章上方的`front-matter`除了上面常用的参数，还有更多    见[官方文档](https://hexo.io/zh-cn/docs/front-matter.html)

### 修改分类路径

比如，我这样写：
```
categories: 技巧
```
那么访问`技巧`分类的路径就是 `./categories/技巧` 如果要改`分类路径`，比如让分类路径为英文.

打开根目录下的配置文件_config.yml，找到如下位置做更改：

```
# Category & Tag
default_category: uncategorized
category_map:
	技巧: trick
	生活: life
	其他: other
tag_map:
```
在这里`category_map`:是设置分类的地方，每行一个分类，冒号前面是分类名称，后面是访问路径。

这样打开`技巧`分类时候的路径就变成了`./categories/trick`。


## 更换主题

更改`_config.yml`文件里面的`theme`字段，对应了`theme`文件夹里面的主题文件夹名称。

然后
```
hexo clean
```
并删除`.deploy_git`文件夹。
执行命令
```
hexo g -d 
```


## hexo博客一些文件夹及文件介绍

* `node_modules`：npm下载一个一些包和模块都在这个文件夹里面
* `public`：已生成的静态文件 (public)。
* `scaffolds`: 中文意思`支架`，存储了文章的模板文件。即当你新建一片文章自动填充的模板内容。
* `_config.yml`:博客站点的配置文件


## 绑定自定义域名

* 在github仓库中新建一个文件，名称为`CNAME`，没有后缀。内容填你的域名地址，不加`http://`。如：ihewro.top  
* 在域名解析里，添加CNAME解析，解析地址为你的githubpage地址，如我的：ihewro.github.io  不用加`http://`

## 参考文章

[如何使用Hexo搭建Github Pages博客](https://levblanc.github.io/2015/07/13/building-github-pages-blog-with-hexo/)
[hexo官方文档](https://hexo.io/zh-cn/docs/)
[Hexo常见问题解决方案](https://xuanwo.org/2014/08/14/hexo-usual-problem/)
[Hexo使用攻略：（四）Hexo的分类和标签设置](http://ijiaober.github.io/2014/08/05/hexo/hexo-04/)