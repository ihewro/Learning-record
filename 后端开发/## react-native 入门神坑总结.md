## react-native 入门神坑总结


### 安装坑

官网的`Getting Started`有两个部分：
* `Quick Start`
* `Building Projects with Native Code`

对于新手的我，一开始就懵逼了。到底选择哪个？？？

第一个，是官方为了方便新手，为了不让新手搭建环境的痛苦，所以创造了`create-react-natvice-app`的命令行。

第二个，才是普通的搭建环境的做法。

安装过程中，主要是一定要翻墙，否则很痛苦。。。

### 第一个demo坑

```
react-native init AwesomeProject
```

创建第一个demo，

再运行

```
react-native run-android
```

就会发现报了第一个错误：找不到SDK

具体原因是，之前自动生成的项目的`android`目录下没有`local.properties`文件，这不是坑人嘛！这个文件用来指定SDK位置的，必须自己手动新建一个。

再运行一次，就会发现报了第二个错误：找不到`index.android.bundle`这个文件。
这个文件本来是在`android/app/src/assets/`目录下，但是却没有自动生成：

手动新建一个android/app/src/assets/index.android.bundle  
然后在项目根目录执行命令：
```
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
```

每次修改文件后不需要重新运行，

可以连续按两次R，或者按 command + M，选择 reload 即可。



### 项目目录结构神坑



网络上目前教程大多数是0.48 的，我现在用的是0.49，主要差别在于目录中的文件。



没有之前的index.android.js，取而代之的是

index.js和app.js

index.js + app.js = index.android.js

index.js内容比较简单，是负责申明并且导入app.js模块的

app.js里面才是主要内容！

