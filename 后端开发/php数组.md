---
title: php数组
date: 2017-04-19 18:54:01
tags:
categories: PHP
---

## 引导

PHP数组分为两个组成部分：**数组元素**和**索引**（又称关键字）。

我们通过索引来获取数组中的元素的值。

从索引方面可分为：

* 数字索引数组
* 关联数组

从维度上面可分为：

* 一维数组
* 多维数组

<!--more-->

## 数字索引数组

### 初始化数组

1. 不需要任何初始化。

PHP数组和其他的变量一样，数组可以不需要初始化或创建，**第一次使用他们的时候，他们会自动创建**。

如：

```php
$products[0] = 'Tires';
$products[1] = 'oil';
$products[2] = 'spark plugs';
```

如果$producs数组不存在，第一行代码自动创建只有一个元素的数组。

2. 你也可以预先初始化一个数组。

```php
$products = array("Tires,oil,spark plugs");
```

3. 你还可以初始化一个空数组

```PHP
$products = array();
$products[0] = 'Tires';
$products[1] = 'oil';
$products[2] = 'spark plugs';
```

上面三种方法的效果是等价的。

注意：PHP数组是**动态创建大小的** ，这一点很方便。

### range()函数创建数组

PHP提供了一个`range()`函数，使我们可以方便创建特殊类型的数组。

range()有三个参数。第一和第二个参数分别表示数组起始和终止的位置。

其中第三个参数是可选的，表示元素之间的间隔。

1. 比如，创建一个1-10的奇数数组。

```php
$odds = range(1,10,2)
```

2. 比如，创建a-z的数组。

```php
$letters = range('a','z');
```



### 访问数组中元素

#### 通过**$数组名[索引]**的方式

大多数编程语言的数字索引数组都是如此

#### 通过循环方式

1. for循环

```php
for($i =0;$i<2;$i++){
  echo $products[$i];
}
```

2. foreach循环

```php
foreach($products as $product){
  echo $product;
}
```



## 关联数组

关联数组索引不再是位置序号而是自定义名称。

### 初始化数组

1. 不需要任何初始化

```php
$prices['Tires'] = 100;
$prices['oil'] = 10;
$prices['spark plug'] = 4;
```

2. 初始化一个数组

```php
$prices = array('Tires'=>100, 'oil'=>10,'spark plugs'=>4);
```

3. 初始化一个空数组

```
$prices = array();
$prices['Tires'] = 100;
$prices['oil'] = 10;
$prices['spark plug'] = 4;
```

上面的代码均可以创建以产品名称为索引，以价格为值的关联数组。效果是完全等价的。

### 访问数组

#### 通过**$数组名[’索引‘]**

和数字索引数组一样，使用**$数组名['索引']**，如`$prices['Tires']`

#### 通过循环

1. foreach()循环

```php
foreach($prices as $key => $value){
	echo "$key - $value <br />";
}
```

`$key`表示当前元素的索引，`$value`表示当前元素的值。

2. while() + each()函数

```php
while($element = each($prices)){
  echo "$element['key'] - $element['value'] <br />";
}
```

这里使用了一个之前没使用过得函数`each()`。

该函数会返回数组当前元素的键名和键值，并将内部指针移到下一个元素。如下：

```php
$element[0] == 键名 
$element[1] == 键值 

$element['key'] == 键名
$element['value'] == 键值
```

在这个代码中，`$element`是一个数组。调用`each()`时候，他将返回一个数组(`$element`)，这个数组带有4个数值和4个指向该数值的索引。

3. while() + each() + list()函数

```php
while(list($product,$price) = each($prices)){
  echo "$product - $price <br />"
}
```

这里又用到了一个新的函数`list()`。

list()函数将each()函数返回的数组中的0和1位置的值赋值给了`$product`和`$price`两个变量。

`list($key,$value)`和`each(array)`组合使用，**即将数组当前元素的键名和键值分别赋值给`$key`和`$value`两个变量**。



综上所述，对于关联数组的循环访问元素，最有效，最方便的还是第一种方法。



## 多维数组

### 初始化数组

一维数组是一些（索引=>值）的集合。

二位数组就是**把一维数组中的值变成一维数组**。即（索引=>一维数组）的集合

如下面的表格信息，

| code | description | price |
| ---- | ----------- | ----- |
| TIR  | Tires       | 100   |
| OIL  | Oil         | 10    |
| SPK  | Spark Plug  | 4     |

直接初始化二维数组，

```php
$products = array(array('TIR','Tires',100),
                 array('OIL','Oil',10),
				array('SPL','Spark Plug',4));
```

二维数组包含了三个子数组。

子数组不仅可以是数字索引的一维数组，还可以是一维关联数组。

即

```php
$products = array(array('code'=>'TIR','desciption'=>'Tires','price'=>100),
                 array('code')=>'OIL','desciption'=>'Oil','price'=>10),
				array('code'=>'SPK','desciption'=>'Spark Plug','price'=>4));
```

### 访问数组元素

#### 通过`$数组名[索引1][索引2]`

和一维数组类似，通过索引1访问二维数组中的某个子数组，再通过索引2访问子数组的某个元素。

如 

```php
$products[0][0] == TIR;
$[0]['code'] == TIR;
```

### 通过循环

#### 子数组是数字索引数组

这类比较简单一点，使用双重循环即可，和一维数字索引数组类似。

```php
for($i=0;$i<3;$i++){
  for($j=0;$j<3;$j++){
    echo "|$products[$i][$j]";
  }
  echo "|<br />";
}
```

#### 子数组是关联数组

子数组是关联数组，则不能使用二重循环，原因在于子数组的索引不再是序号而是描述性的文字。

```php
for($row=0;$row<3;$row++){
  echo "|$products[$row]['code']|$products[$row]['description']|$products[$row]['price']|<br />";
}
```

和一维的关联数组类似，可以使用each()函数获取每个子数组，然后再用list()函数获取0,1位置的值。

```php
for($row=0;$row<3;$row++){
  while(list($key,$value) = each($products[$row]))
    echo "|$value";
  echo "|<br />";
}
```

## 对数组的操作

### 数组操作符

只有一个特殊的操作符集合适用于数组。

| 操作符  | 名称   | 示例          | 结果                                       |
| ---- | ---- | ----------- | ---------------------------------------- |
| +    | 联合   | `$a+$b`     | 将`$b`中元素添加到`$a`的末尾。如果`$b`中的元素与`$a`中的一些元素具有相同的索引，他们将不会添加。 |
| ==   | 等价   | `$a == $b`  |                                          |
| !=   | 不等价  | `$a !=$b`   |                                          |
| <>   | 不等价  | `$a<>$b`    |                                          |
| ===  | 恒等   | `$a === $b` |                                          |
| !=== | 不恒等  | `$a!===$b`  |                                          |

### 数组常用的函数

#### 访问数组中的元素



#### 对数组元素修改

* array_push(array,value1,value2…)：把一个或者多个元素添加到数组的末尾
* array_pop(array) ：删除数组的最后一个元素

#### 统计数组元素的个数

#### 对数组的元素排序

