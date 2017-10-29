# pjax中文文档


## pjax = 缓存区 + ajax

pjax 是一个jQuery插件，它使用ajax和pushState 来实现快速的浏览体验，与此同时，地址栏、页面标题都会随之变化。

pjax通过使用ajax获取到HTML，并将获取到的Html内容加载到替换容器中，然后使用pushState更新浏览器的URL，。让页面加载速度大大增快有两个原因：

* 大部分的页面资源(css、js)被重新执行或重新应用
* 切换页面只会渲染页面的部分页面，不会重新渲染整个页面布局

### 该项目目前的状态

它可能会得到重要bug的修复，但不太可能会得到新的特性或增强。

## 安装

pjax需要jQuery1.8或者更高版本。


### npm

```
npm install jquery-pjax
```

### 独立脚本

下载`jquery.pjax.js`并包含在您的网页中：

```curl
curl -LO https://raw.github.com/defunkt/jquery-pjax/master/jquery.pjax.js
```


## 用法
