# react-native 入门（4） ——样式

和css语法基本类似，但是样式的属性名都是驼峰命名法。

一般采用`StyleSheet.create`来集中定义组件的样式。如：

```react
const styles = StyleSheet.create({
  bigblue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});

```

在使用的时候，直接引用对应的样式即可。



```react
class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigblue}>just bigblue</Text>
        <Text style={[styles.bigblue, styles.red]}>bigblue, then red</Text>
        <Text style={[styles.red, styles.bigblue]}>red, then bigblue</Text>
      </View>
    );
  }
}

```

