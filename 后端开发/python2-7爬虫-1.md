---
title: python2.7爬虫<1>
date: 2017-05-23 21:02:49
tags:
categories: python
---

## 什么是爬虫

~~爬虫就是一种生物，爬来爬去的~~

## 第一个爬虫

我们第一个爬虫的内容是爬下一个网页的源代码


```python
import urllib2 #导入必要库

response = urllib2.urlopen("http://www.baidu.com") # 打开网址获取源代码
print response.read() #打印源代码
```

我们这个程序只干了三件事：

1. 第一行导入的是`urllib2`

[拓展]：[urllib和urllib2有什么区别和联系]()

2. 第二行是`urllib2`提供的一个方法**urlopen()**，这个方法用来打开url，并返回网站的源代码
3. 第三行就是将`response`对象里面的内容打印下来。

现在再来看一下`urlopen`方法的详细信息：

```python
urlopen(url[, data][, timeout])
```

* 第一个参数是URL
* 第二个和第三个参数均为可选，data是访问URL时要传送的数据，第三个timeout是设置超时时间。
* data默认为空None，timeout默认为socket._GLOBAL_DEFAULT_TIMEOUT

`urlopen`方法返回了一个response对象，网站的源代码就存储在这里面。

----

我们还可以通过传递urllib2中的`Request`类的实例（构建请求）给`urlopen`方法（推荐这种方法）

创建一个`Request`对象和Java创建对象类似只是不用new关键字，

```python
request = urllib2.Request(url[, data][, headers])
response = urllib2.urlopen(request)
```

上面的代码即等价为：
```python
import urllib2 #导入必要库

request = urllib2.Request("http://www.baidu.com")
response = urllib2.urlopen(request) # 打开网址获取源代码
print response.read() #打印源代码
```

**特别注意一点是**：虽然`data`和`headers`都是可选参数，但是如果`data`为空，这时需要传递header参数，需要特别指定是`headers`是多少，如果`data`不为空，则按照普通的传参方式即可

```python
request = urllib2.Request(url, headers= headers)
request = urlib2.Request(url, data, header)
```

## 进阶一：设置headers

上面`Request`构建方法里面有一个参数是`headers`，这个参数非常有用。

header是啥呢，经常调试网页小伙伴对这个很清楚，见下图:

![](https://cdn.ihewro.com/img/headers.png)

直接看下面的代码，大家就一目了然，非常简单。

```python
import urllib2

url = "http://www.baidu.com"
user_agent = 'Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)'

request = urllib2.Request(url, headers=headers)
response = urllib2.urlopen(request)
```



## 进阶二：传递data

数据请求分为：get请求和post请求

[拓展]：[get请求和post请求之间的区别]()


### get请求

get请求请求的参数是之间显示在url地址上面的。

所以，只需要将`url`添加上请求的参数和值即可。

```python
import urllib
import urllib2

values = {"username":"1016903103@qq.com","password":"XXXX"}
data = urllib.urlencode(values) 
url = "http://passport.csdn.net/account/login"
geturl = url + "?"+data
request = urllib2.Request(geturl)
response = urllib2.urlopen(request)
print response.read()
```

### post 请求

```python
import urllib
import urllib2

values = {"username":"1016903103@qq.com","password":"XXXX"}
data = urllib.urlencode(values) 
url = "https://passport.csdn.net/account/login?from=http://my.csdn.net/my/mycsdn"
request = urllib2.Request(url,data)
response = urllib2.urlopen(request)
print response.read()
```

## 进阶三：cookie的使用

有的网站对用户信息是有cookie存储的，尤其是用户登录后，用户的浏览器就会通过cookie保存用户的信息。

所以，我们使用Python发送模拟请求的时候，如果想爬下模拟登录后的页面，我们就必须发送cookie。

```python

```

