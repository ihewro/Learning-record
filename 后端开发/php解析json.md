---
title: php解析json
date: 2017-04-04 11:58:28
tags:
categories: php
---

很多api返回的数据格式都是json格式，所以需要我们用php来格式化jason，获取我们需要的内容。



从5.2版本开始，PHP原生提供[json_encode()](http://www.php.net/manual/en/function.json-encode.php)和[json_decode()](http://www.php.net/manual/en/function.json-decode.php)函数，前者用于编码，后者用于解码。

<!--more-->

## json_encode()

