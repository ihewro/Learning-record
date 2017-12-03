# react入门（1）——JSX语法

JSX 是React的核心组成部分，它使用XML标记的方式去直接声明界面。

界面组件之间可以互相嵌套。可以理解为在JS中编写与XML类似的语言，一种**定义带属性树结构（DOM解构）的语法。**

它的目的不是要在浏览器或者引擎中实现，而是**通过各种编译器将这些标记编译成标准的JS语言。**

虽然你可以完全不适用JSX语法，只使用JS语法，但是还是推荐使用JSX，可以定义包含属性的树状结构的语法，类似HTML标签那样的使用，而且更便于代码的阅读。

使用JSX语法后，你必须要引入babel的JSX解析器，把JSX转换为JS语法，这个工作会由babel自动完成。同时引入babel后，你就可以使用新的es6语法，babel会**帮你把es6语法转换为es5语法，兼容更多的浏览器。**



## 1. 最简单的demo

```xml
<!DOCTYPE html>
    <html>
    <head>
      <meta charset="UTF-8" />
      <title>Hello React!</title>
      <script src="vendor-js/react.js"></script>
      <script src="vendor-js/react-dom.js"></script>
      <script src="vendor-js/babel-core/browser.min.js"></script>
    </head>
    <body>
      <div id="example"></div>
      <script type="text/babel">
        ReactDOM.render(
          <h1>Hello, world!</h1>,
          document.getElementById('example')
        );
      </script>
    </body>
  </html>
```

在这个简单例子中，看不出有任何使用JSX语法的地方，其中`<h1>Hello, world!</h1>`就是使用了JSX语法。

HTML语法直接写在Javascript语言之中，**不加任何引号**，这就是JSX语法，它允许HTML与Javascript标签的混写。转换成普通的js语言就是：

```html
<script type="text/javascript">
      ReactDOM.render(
        React.DOM.h1(null,'hello,world!'),
        document.getElementById('example')
      );
</script>
```



这里有两个需要注意的地方：

*    `<script>`标签的type属性为`type/babel`，这是React 独有的JSX语法。跟JavaScript不兼容。凡是页面中直接使用JSX的地方，都要加上这个特殊的属性。
*    开头的地方用到了三个库：react.js  react-dom.js browser.min.js，它们必须首先加载。其中react.js 是React的核心库。react-dom.js 是提供与DOM相关的功能，browser.min.js 的作用是将JSX转换成普通的js语法。

`ReactDOM.render`是React最基本的写法，将模板转为HTML语法，并插入指定的DOM节点。



##2. JSX 特点 



## 3. JSX基本语法规则

