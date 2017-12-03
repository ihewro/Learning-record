# react-native入门（2）——Props(属性)

“属性”这个在前端开发中经常遇到。

比如某个`div` `span`标签等等，都有很多属性，来描述该标签的特征。

在react-native中属性可以用来描述{内置组件}和{自定义组件}都特征，使用方法和HTML语言基本类似。



## 1. 内置组件的属性

```react
import React, { Component } from 'react';
import { AppRegistry, Image } from 'react-native';

class Bananas extends Component {
  render() {
    let pic = {
      uri: 'https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg'
    };
    return (
      <Image source={pic} style={{width: 193, height: 110}} />
    );
  }
}

AppRegistry.registerComponent('Bananas', () => Bananas);
```



上面的代码中，使用了Image的加载图片组件，这和HTML语言中的`<img>`使用基本一致。

注意Image组件的`source`属性的值为`{pic}`，外围有一层大括号，这个括号把`pic`这个**变量**嵌入到了JSX语句中了。

括号的意思是括号内部是一个js变量或者是表达式，需要执行后取值。这是JSX语法的一种。



## 2. 自定义组件的属性

```react
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Greeting extends Component {
  render() {
    return (
      <Text>Hello {this.props.name}!</Text>
    );
  }
}

class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{alignItems: 'center'}}>
        <Greeting name='Rexxar' />
        <Greeting name='Jaina' />
        <Greeting name='Valeera' />
      </View>
    );
  }
}

AppRegistry.registerComponent('LotsOfGreetings', () => LotsOfGreetings);
```

上面代码中，`Greeting`就是自定义组件，内部渲染中使用了`this.props.name`就是在调用`name`属性的值。



当使用该组件的代码中为该组件的这个属性赋值，上行代码中就能取到该属性的值。