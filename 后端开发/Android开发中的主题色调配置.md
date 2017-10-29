## Android开发中的主题色调配置

## 目录

请按照以下目录查询阅读：

*    命名空间
*    主题配置
     *    配置一般方法
     *    Theme.AppCompat 常用颜色属性的含义
*    控件配置
*    自定义控件配置
*    material 设计工具
*    参考文章
*    推荐阅读


## 命名空间

在了解Android 色调属性配置之前，必须先了解Android开发中的命名空间的概念。

>    XML 命名空间提供避免元素命名冲突的方法。—[w3school.com](http://www.w3school.com.cn/xml/xml_namespaces.asp)

概念很简单。比如小明有一本书，小王也有一本同样的书。我们在叙述的时候，就会在一本书的前面加上**命名空间**来区分。换句话说，**命名空间就是一个修饰词语**。

命名空间不是本文探讨的重点，以下简略介绍。

在Android 的布局文件中，常见的命名空间有以下几种：

* android: 在这个命名空间下有很多系统属性，常见的有`android:layout_width`等等

```xml
xmlns:android=”http://schemas.android.com/apk/res/android”
```

*    tool: 一个工具(tools)的命名空间,是帮助开发人员的工具.它的作用只于开发阶段发挥,当app被打包时,所有关于tools属性将都会被摒弃掉。这部分使用的时候可以再去查找相关资料。

```xml
xmlns:tools="http://schemas.android.com/tools"
```

*    app: 自定义控件属性的命名空间。在Android UI设计中，我们会设计一些自定义控件，然后申明一些自定义属性，最后在布局文件中使用这些属性，这个时候就用`app`这个命名空间。

```xml
xmlns:app=”http://schemas.android.com/apk/res-auto”
```

​	实际上，网络中很多教程的自定义属性的命名空间是这样的申明的：

```xml
xmlns:app=”http://schemas.android.com/apk/res/<自定义控件的包名>”
```

​	在Android Studio2.0以上，已经不推荐后者的写法了，统一使用第一种写法。

​	至于如何自定义控件，申明自定义属性、解析属性我们会在最后一节中探讨。

## 主题配置

### 配置的一般方法

>    **在AndroidManifest.xml中配置应用(Application)或者活动(Activity)的主题**



```xml
<application
        android:name=".common.BaseApplication"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:theme="@style/AppGreenTheme">
  		<activity android:name=".common.activity.BaseActivity"
                  android:theme="@style/AppGreenTheme">
  		</activity>
</application>
```

方法很简单，加上`android:theme`属性值就可以配置相应的Style了，属性值是下面介绍的。



>    **在valuse/style.xml文件中配置，基本格式如下**

```xml
    <style name="AppGreenTheme" parent="Theme.AppCompat.Light.NoActionBar">
      	<!--在下面自定义配置-->
        <item name="colorPrimary">@color/blue_primary</item>
        <item name="colorPrimaryDark">@color/blue_primary_dark</item>
        <item name="colorAccent">@color/blue_accent</item>
        <item name="android:textColorPrimary">@color/blue_primary_text</item>
        <item name="android:textColorSecondary">@color/blue_secondary_text</item>
        <item name="android:icon">@color/blue_icons</item>
        <item name="android:divider">@color/blue_divider</item>
        <item name="android:windowBackground">@color/blur_window_background</item>
    </style>
```

如上所示，新建一个`AppGreenTheme`绿色主题，`parent`标签中是继承的父主题`Theme.AppCompat.Light.NoActionBar`。

因为我们新建的活动都是继承自`AppCompatActivity`如果不继承这个父主题，就会由于某些颜色配置缺失导致编译错误（没有证实）。

下面的部分就是自定义配置，这里最为关键的是了解常见的系统提供的属性的含义

### Theme.AppCompat 常用颜色属性的含义

[Android Theme.AppCompat 中，你应该熟悉的颜色属性](http://yifeng.studio/2017/04/18/android-theme-appcompat-color-attrs/)

这篇文章中作者已经讲的很详细了，十分感激。


## 控件配置

控件的样式配置和主题是基本一直的，也是在`style.xml`中新建一个新的主题。

但是对于控件或者视图，需要添加`style`属性：

```xml
<TextView
    style="@style/CodeFont"
    android:text="@string/hello" />
```

该样式只会应该到当前控件中，不会应用到子控件或者子布局中。

不过，可以通过以主题形式应用样式，使所应用的样式作用于所有 `View` 元素。即`android:theme`属性添加样式。



## 自定义控件配置



## Material 设计工具

[Material Style官方标准文档](https://material.io/guidelines/style/color.html#)

[快速挑选Material Design的配色方案](http://www.jianshu.com/p/f4a7d8369caa)



## 参考文章

[Android中的命名空间](http://blog.csdn.net/wxx614817/article/details/52909766)

[Attr、Style和Theme详解](http://www.jianshu.com/p/dd79220b47dd)

[Android Theme.AppCompat 中，你应该熟悉的颜色属性](http://yifeng.studio/2017/04/18/android-theme-appcompat-color-attrs/)

[Android主题与Toolbar样式之间的关系](http://www.jianshu.com/p/221024169a5c)



## 推荐文章

[样式和主题](https://developer.android.com/guide/topics/ui/themes.html?hl=zh-cn)

[轻听变色之谜](http://mp.weixin.qq.com/s/m_wZM8xtJnph8PTdbH6s7Q)

[android 自定义控件使用declare-styleable进行配置属性（源码角度）](http://blog.csdn.net/vipzjyno1/article/details/23696537)

[在你的Android App中支持多主题](https://github.com/hehonghui/android-tech-frontier/tree/master/androidweekly/%E8%AE%A9%E4%BD%A0%E7%9A%84Android%E5%BA%94%E7%94%A8%E8%83%BD%E4%BD%BF%E7%94%A8%E5%A4%9A%E7%A7%8D%E4%B8%BB%E9%A2%98-Part-1#在你的android-app中支持多主题)

