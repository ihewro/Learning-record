---
title: Python中的命令行解析参数工具介绍
date: 2017-05-12 21:44:27
tags:
categories: python
---


首先要知道什么是命令行参数解析

比如，

```Python
python ex15.py [<参数1> <参数2> ……]
```

下面的工具就是负责解析这些参数，以方便程序中使用。

## sys.argv

这是我第一个接触到的。

```python

import sys

for arg in sys.argv:

	print arg

```

可以看出，sys.argv[0]，即第一个参数是执行脚本的名字，所以，一般获取参数从 第二位开始，即sys.arg[1:]

这种方法非常简单，实现的功能也很少，如果想让脚本看起来专业点：比如支持长短格式，长格式添加=，帮助信息等完善的参数操作，通过相应的类库可以较快实现


## argparse



## 参考文章：

1. [Argparse简易教程](https://blog.ixxoo.me/argparse.html)
2. [Python中的命令行解析工具介绍](http://lingxiankong.github.io/blog/2014/01/14/command-line-parser/)
3. [Python 命令行参数解析](http://www.ueffort.com/python-ming-ling-xing-can-shu-jie-xi/)
