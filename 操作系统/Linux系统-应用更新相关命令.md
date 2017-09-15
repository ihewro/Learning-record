---
title: Linux系统/应用更新相关命令
date: 2017-04-28 17:26:16
tags:
categories: linux
---

```bash
sudo apt-get update         #更新源

sudo apt-get -f install      #修正依赖关系

sudo apt-get upgrade      #更新已安装的包【程序】
  
sudo apt-get dist-upgrade    #升级系统

sudo apt autoremove     #清理系统残留

```


所以升级Linux，命令行就是

```bash
sudo apt-get update && sudo apt-get dist-upgrade -y

```

最后的`-y`就是所有交互式操作都自动填入 y（yes）。不需要手动再输入进行交互了～

