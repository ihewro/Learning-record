# react-native 入门（3） ——State(状态)

我们使用两种数据来控制一个组件：`props` `state`。

*    `props`在**父组件**中指定，一经指定，在**被指定的组件的生命周期中则不能再改变**
*    对于需要改变的数据，我们需要使用`state`


一般我们在类的 `constructor` 中初始化 `state`，然后在需要修改的地方调用`setState`方法。

```react
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Blink extends Component {
  constructor(props) {
    super(props);
    this.state = { showText: true };

    // 每1000毫秒对showText状态做一次取反操作
    setInterval(() => {
      this.setState(previousState => {
        return { showText: !previousState.showText };
      });
    }, 1000);
  }

  render() {
    // 根据当前showText的值决定是否显示text内容
    let display = this.state.showText ? this.props.text : ' ';
    return (
      <Text>{display}</Text>
    );
  }
}

class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text='I love to blink' />
        <Blink text='Yes blinking is so great' />
        <Blink text='Why did they ever take this out of HTML' />
        <Blink text='Look at me look at me look at me' />
      </View>
    );
  }
}

AppRegistry.registerComponent('BlinkApp', () => BlinkApp);
```
这里核心部分是

```react
this.state = { showText: true };

this.setState(previousState => {
        return { showText: !previousState.showText };
});
```

