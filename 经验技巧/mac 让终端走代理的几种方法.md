# mac 让终端走代理的几种方法

前提软件： shadowscoks



macOS 10.13 版本使用proxychains4 已经不行了，原因是macOS的sip安全机制。



## 第一种方法

使用软件Proxifier。



软件的具体使用方法就不说了，在设置rules的时候，应用名称填写ssh，而不是填具体的终端名称！代理走本地代理，然后就可以了。



比如在终端中输入：

```
git clone ...
```

时候，软件日志会显示该程序正在走的是代理。



也可以不设置应用名称，设置目标地址，就是当你的应用程序访问某个目标地址的时候，就会走特定的规则。



但是使用curl 命令下载的时候，会发现，仍然不走本地代理！！

```
curl ip.gs
```

显示的仍然是本地ip地址

而且

```
ping google.com 
```

 还是ping不通，虽然最后仍然ping不通，似乎因为ping走得是icmp协议...具体不是很懂

这个时候就要用到方法二了。



### 方法二

```bash
nano .bashrc

export ALL_PROXY=socks5://127.0.0.1:1080
alias setproxy="export ALL_PROXY=socks5://127.0.0.1:1080"
alias unsetproxy="unset ALL_PROXY"
```

修改.bashrc 文件，然后填入下面的规则。

```bash
source ~/.bashrc
```



以后就可以通过

```bash
setproxy
unsetproxy
```

来设置终端代理了。



这个时候发现

```
curl ip.gs
```

已经是代理的ip了。



完~



### 参考文章

https://www.zybuluo.com/yiranphp/note/611721

https://blog.fazero.me/2015/09/15/%E8%AE%A9%E7%BB%88%E7%AB%AF%E8%B5%B0%E4%BB%A3%E7%90%86%E7%9A%84%E5%87%A0%E7%A7%8D%E6%96%B9%E6%B3%95/