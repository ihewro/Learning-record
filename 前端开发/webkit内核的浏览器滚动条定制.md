## 自定义webkit内核的浏览器滚动条

> 参考文章：[自定义浏览器滚动条的样式，打造属于你的滚动条风格](https://www.lyblog.net/detail/314.html)



对于webkit内核的浏览器，滚动条可以**分为7个部分**。具体见图示



```css
::-webkit-scrollbar  
/*①滚动条整体部分，其中的属性有width,height,background,border（就和一个块级元素一样）等。*/

::-webkit-scrollbar-button      
/*②滚动条两端的按钮。可以用display:none让其不显示，也可以添加背景图片，颜色改变显示效果。*/

::-webkit-scrollbar-track         
/*③外层轨道。可以用display:none让其不显示，也可以添加背景图片，颜色改变显示效果。*/

::-webkit-scrollbar-track-piece        
/*④内层轨道，滚动条中间部分（除去）。*/

::-webkit-scrollbar-thumb               
/*⑤滚动条里面可以拖动的那部分*/

::-webkit-scrollbar-corner               
/*⑥边角*/

::-webkit-resizer                       
/*⑦定义右下角拖动块的样式*/
```
注意的点：

1. `::-webkit-scrollbar`的`width `和`height`的含义 ：
   1. 水平滚动条下，`width`不起作用，`height`控制滚动条的高度
   2. 竖直滚动条下，`height`不起作用，`width`控制滚动条的宽度
2.  webkit内核官方提供了一个滚动条的样例demo [戳这儿](http://trac.webkit.org/export/41842/trunk/LayoutTests/scrollbars/overflow-scrollbar-combinations.html)