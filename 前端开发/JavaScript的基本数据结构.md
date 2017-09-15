---
title: JavaScript的基本数据结构
date: 2017-05-13 10:47:28
tags: 
categories: javascript
---

## 使用JavaScript的两种方式

### 直接使用
* 在任何可以设置URL的地方都可以使用`javascript: + 代码`使用。

* `<script>`标签内书写代码

### 外部引用

```javascript
<script src="" type="text/javascript"></script>
```

## 数据类型和变量

### 定义变量
JavaScript是弱类型语言，和PHP、Python很相似。
* 隐式定义
  什么用，就什么时候定义

* 显式定义
  使用`var`关键字定义变量
```javascript
var x;
x = "good !"
alert(x);
```

### 类型转换
#### 自动类型转换

#### 强制类型转换
* toString()
* parseInt()
* parseFloat()

### 变量范围
**javascript的变量没有块范围。**

什么是块？：
一对花括号{}括起来的区域就是块。

一般的编程语言，如果在if块的内部定义的变量，在if语句的外部将不可访问。
而且变量的作用域是从定义的位置开始的。这很人性化吧？

JavaScript就逆天了！

* 全局变量： 直接定义的变量, **如果没有用var定义，默认为全局变量。**
* 局部变量（函数作用域变量）： 在函数内部定义的变量。

看两段代码吧～

```javascript
var scope = 111;
function test2(){
    alert(scope); //undefined
    var scope = 222;
    alert(scope);///222
}
test2();
alert(scope);//111
```

再看一下c语言写的相似的代码：

```c
#include <stdio.h>
void main (){
	int n = 111;
    if (1) {
        printf("%d\n", n); //111
        int n = 222;
        printf("%d\n", n); ///222

    }

    printf("%d\n", n);///111
}
```

看第一段代码，第一处alert的地方，输出却是`undefined`而不是`111`，说好的全局变量可以在函数局部使用呢？？

原来是下面的局部变量`scope`在整个函数中都是生效的！！但是赋值却是在赋值的位置开始的。

从这个两种结果，可以总结出：

1. javascript局部变量是在整个函数块中生效，不受其他块（如if块等）的约束，而且**不是从定义的位置开始生效的**。

   一般的编程语言局部变量是在相应的块中生效，并且在块中的定义位置开始生效的。

2. JavaScript局部变量的**值还是从赋值的位置开始生效的**。和其他语言一致

3. JavaScript局部变量与全局变量同名，局部变量优先，局部变量修改不会影响全局变量。和其他的语言一致。

### 基本数据类型

#### 数值类型

> 科学计数法

```javascript
a = 3E2 //3*10^2
b = 3e2 //3*10^2
```

> NaN

NaN（Not a Number）是一个特殊的数值，表示非数。

0/0 或者 infinity 和 -infinity 和其他数值运算的结果都是NaN。

isNaN(X)用来检查变量X是否是NaN。

> infinity和-infinity

分别表示正无穷大和负无穷大。

当数值变量的值超过表数范围时，会出现该两个值。（如1e2992、 -2e1212）

正数/0 也会得到infinity

负数/0 会得到-infinity

#### 字符串类型

```javascript
a = "hello hewro!";
b = "b";
```

javascript没有字符的概念！

字符和字符串是等价的。

对字符串的操作，使用的是javascript的内建类String。

如：

```JavaScript
a = "I love you";
b = "huyi";
c = a.slice(0,6) + b;//0到第7个字符（不包括第7个）
alert(c);// I love huyi
```

##### 常用的字符串操作

1. charAt(index):获取某个位置的字符
2. charCodeAt(index): 返回某个位置字符所对应的Unicode字符
3. length: 返回字符串的长度
4. toUpperCase():将字符串中的所有字母转换成大写字母
5. toLowerCase():将字符串中的所有字母转换成小写字母
6. fromCharCode(): 通过String.fromCharCode(unicode,unicode...)调用将一系列的Unicode值转换成字符串
7. ​

#### 布尔类型

True Or False