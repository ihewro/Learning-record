# 处理Activity 与 Fragment 的toolbar 重复问题



在安卓开发中，很常见的一种需求就是点击底部按钮，中间内容切换。

如果需要滑动切换的话，中间部分用ViewHolder 实现。

如果不需要滑动切换，使用普通Fragment 跳转就足够了。

不同的碎片公用同一个底部导航栏，但是顶部的toolbar却可能不一样，这是非常常见的需求，比如搜索界面，toolBar 就和普通的顶部栏不一样。

## 第一种方法

**主活动不设置toolbar，每个fragment都设置一个独自的toolbar。**



## 第二种方法



主活动设置toolbar，需要设置特殊的顶部toolbar时候

```java
((AppCompatActivity) getActivity()).getSupportActionBar().hide();
((MainActivity)getActivity()).setSupportActionBar(spotListToolbar);
setHasOptionsMenu(true);
```



在其他的碎片中使用

```java
((MainActivity) getActivity()).setToolbar();
```

setToolbar是定义在MainActivity中：

```java
public void setToolbar() {
       setSupportActionBar(toolbar);
       getSupportActionBar().show();
}
```

