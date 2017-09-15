---
title: upyun使用命令行upx管理文件
date: 2017-03-01 13:15:06
tags:
categories: 杂烩
---

使用环境：linux deepin 15.4 64位

其他linux环境应该适用该篇文章

## 下载upx

[访问github-upx](https://github.com/polym/upx)

选择下载Linux 64位（可执行程序二进制下载地址）

下载到/home/hewro/Downloads 目录下。

再该目录下打开终端，输入命令，将打包的环境直接复制到 `bin`目录下。

```bash
cp -rf upx-linux-amd64-v0.1.6 /usr/bin/upx
```

然后输入命令，给upx可操作文件的权限。

```bash
chmod +x /usr/bin/upx
```

这时候，就已经安装好了，可以直接输入`upx`命令，查看帮助。

<!--more-->

### 语法

```
upx [global options] command [command options]
```

**选项**

| command | 含义                                       |
| ------- | ---------------------------------------- |
| login   | 登录又拍云存储                                  |
| pwd     | 显示当前所处目录                                 |
| ls      | 显示当前目录中的文件和目录信息，加 `–d`， 仅显示目录信息          |
| cd      | 改变工作目录（进入一个目录），加 `..`，回到上一级目录            |
| get     | 下载一个文件或目录                                |
| put     | 上传一个文件或目录                                |
| sync    | 增量文件同步，类似 rsync                          |
| mkdir   | 创建目录                                     |
| rm      | 删除文件，支持通配符 `*`；加 `–d`，删除目录；加 `–a`，删除目录和文件；加 `–async`，异步方式删除文件或目录 |
| info    | 显示登录的服务名、操作员信息和当前所在目录                    |
| logout  | 退出又拍云存储                                  |

| global options | 含义                 |
| -------------- | ------------------ |
| -h             | 显示帮助信息             |
| -v             | 显示 UPX 版本信息或处理过程信息 |



## 使用upx

### 登录管理

> 登陆

```bash
upx login
```

正确输入`BucketName`,`Operator`,`Password` 三项就可以登录成功。

![upx-login](https://cdn.ihewro.com/img/upx-login.png)

> 注销

```bash
upx logout
```

### 目录管理

> 显示当前目录名称

```bash
upx pwd
```

![upx_pwd](https://cdn.ihewro.com/img/upx-pwd.png)


> 查看当前目录与状态

```bash
upx info
```

![upx_info](https://cdn.ihewro.com/img/upx-info.png)

> 列出当前目录下的信息

```bash
//加上 -d 只会列出目录信息，文件信息不会显示
upx ls -d
```

![upx_ls](https://cdn.ihewro.com/img/upx-ls.png)

> 创建目录

```bash
upx mkdir <文件夹名称>
```

> 删除目录

```bash
upx rm -d <文件夹名称>
```



### 文件管理

> 上传文件

* 上传单个文件

```bash
upx put <本地路径> <云存储路径>

//eg.把test.png 上传到 img 目录下
upx put /home/hewro/test.png /img
//eg. 云存储路径为空，则上传到当前目录下
```

* 上传整个文件夹文件

```bash
//eg. 把 floder 整个文件夹上传到根目录
upx put /home/hewro/floder /
```

* 增量文件同步

```bash
//增量文件同步,加 -v,显示增量文件同步过程信息
upx sync <本地目录> <云存储目录> -v
```

增量文件同步，即将本地目录文件与云存储目录文件先进行校验比较，然后将未上传的文件增量上传。

> 删除文件

* 删除单个文件

```bash
upx rm <文件名称>
```

* 删除整个文件夹

```bash
//加 -d，删除目录
upx rm -d <文件夹名称>
```

> 下载文件

```bash
upx get <云存储路径> <本地路径>
```

