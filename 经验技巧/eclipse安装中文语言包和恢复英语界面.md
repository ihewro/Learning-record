---
title: eclipse安装中文语言包和恢复英语界面
date: 2017-03-01 21:27:59
tags:
---

eclipse版本信息：

Eclipse Java EE IDE for Web Developers.

Version: Neon Release (4.6.0)
Build id: 20160613-1800

以下文字理论上在其他eclipse版本同样有效。

<!--more-->

## 安装中文语言包

[进入eclipse官方下载语言包的页面](http://www.eclipse.org/babel/downloads.php) （注：这个页面全英文，主要是介绍eclipse的翻译计划）



一直拖到这里，复制这个框里面的地址。（注意，要复制和你版本一直的语言包！）

![downloads](https://cdn.ihewro.com/img/eclipse_dowlods.png)



点击`Help——Install New SoftWare`

在输入框中输入刚才复制的语言包地址，稍等一会会出现该语言包的所有插件。（限于国内网络环境，可以需要**配置代理**才能够下载）

选择`Babel labguage Packs in Chinese (Simplified)`

![software_eclipse](https://cdn.ihewro.com/img/software_eclipse.png)

然后选择`next` 直到安装完成。



重启一下，就会发现安装成功！



## 恢复英文原版

linux 下有一个文件搜索工具`ANGRYsearch`,非常实用。如果是deepin系统，则在深度商店里可以直接搜索并安装。

找到`eclipse.ini`文件

在最后一行加上`-Duser.language=en`。

![eclipse_ini](https://cdn.ihewro.com/img/eclipse_inin.png)

重启一下，就又变成英文了。

## eclipse配置代理

点击`windows——Prefenrence`

在`General——network Connections`的配置项中，如下图配置：

![eclipse_prefenrence](https://cdn.ihewro.com/img/eclipse_preference.png)

**前提是**你的linux已经开启了代理。