---
title: grunt入门笔记
date: 2016-11-29 23:15:15
tags:
---

grunt在前端工具中算是很有用的一个工具。

想一想如果没有这个工具，我们需要手动新建一个压缩代码后的文件夹，每次修改原始文件，都要手动压缩一下，再保存到压缩后的文件夹，想想都要疯掉。所以，grunt前端必不可少。

以下内容分别是：

1. grunt安装和配置
2. grunt压缩一个js的实例分析
3. grunt 美化、压缩、合并代码文件或者代码文件夹里所有代码文件的代码实例


<!--more-->


## grunt的安装与配置


#### grunt的安装
grunt 依赖Node.js,所以请先确保安装完成Node.js.

* 首先安装 `grunt-cli`工具。
```
npm install grunt-cli -g
```
**记住**：这里是全局安装。windows系统可能需要开启管理员权限启动命令行。

**注意**：`grunt-cli`并不是`grunt`工具本身，只是安装了这个工具，而是用来调用和`gruntfile.js`同一目录的`grunt`。真正的`grunt`是安装在项目目录下面的。

* 然后进入你的项目目录，安装grunt（**grunt工具是要安装在项目目录里面的**）：
```
npm install grunt --save-dev
```
`--save-dev`就是告诉`package.json`，你在开发这个项目中依赖了这个插件，同时在`package.json`中的`devDependencies`也会出现你安装的这个插件的信息。方便你把项目传给别人，别人下载对应的插件。


#### grunt的配置

grunt如果正常使用，目录下面必须要有两个文件`package.json`和`gruntfile.js`。分别简单介绍配置这两个文件的方法。

1. package.json文件

这个文件存储的是`npm`的一些元数据。比如：项目名称、版本、依赖的一些插件等等。是采用键值对的形式写的。

如果一开始项目没有这个文件，可以执行`npm init` 初始化这个文件。

2. gruntfile.js

这就是一个js文件，采用的是js语法。文件内容主要分为三块：

1. 任务配置代码：

这里面包含的当然是你需要执行的一个个任务的具体内容，比如：你打扫卫生时候要干的，扫地、洗碗、擦桌子、擦窗户等等任务内容。


2. 插件加载代码：

你在这个过程中使用了哪些插件，把这些插件名称声明出来，仅仅的grunt是不能完成任务的，


3. 任务注册代码

第一步分条写了很多条任务的具体内容，最后一步就是把注册一个总任务名称，比如：打扫卫生。然后声明要干总任务里面的哪几条分任务。


下面以详细代码来写js的压缩。其余内容只需要更改任务配置代码的部分即可。

最后，认识一下grunt一些基本的插件：

* 合并文件：grunt-contrib-concat
* 语法检查：grunt-contrib-jshint
* Scss 编译：grunt-contrib-sass
* 压缩文件：grunt-contrib-uglify
* 监听文件变动：grunt-contrib-watch
* 建立本地服务器：grunt-contrib-connect

这些插件都是grunt使用过程中最常用的。我们这个项目中，使用到的只有第一个和第四个。

安装的命令：

```
npm install --save-dev grunt-contrib-concat grunt-contrib-uglify
```

-----

## js自动化压缩

首先要明白，这是一个 JS 文件，你可以写任意的 JS 代码，比如声明一个 对象 来存储一会要写任务的参数，或者是一个变量当作开关等等。


然后，所有的代码要包裹在
```
module.exports = function(grunt) {
    ...
};
```

这个没有为什么，照着写就对了。

然后在这个里面写三块的内容：

#### 任务配置代码

```
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    uglify: {
      options: {
        banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n'
      },
      build: {
        src: 'src/<%= pkg.name %>.js',
        dest: 'build/<%= pkg.name %>.min.js'
      }
    }
  });

```

解释上面的代码：
1. 首先在
```
grunt.initConfig({})里面写任务配置
```

2. `pkg`:读取目录下面的`package.json`文件，以便我们使用`package.json`里面的一些变量。
3. `uglfy`:指的是`压缩`任务。调用的是`grunt-contrib-uglify`插件。
    1. 首先配置了`option`：`banner`的配置项。意思是在文件的顶部加上压缩时间。
    2. 然后建立了一个子任务：`build`，名字自己取一个。内容是两个文件夹地址。`src`就是源文件地址。`dest`就是压缩后文件地址。

#### 插件加载代码

这个很简单，就相当于C语言中的函数申明。
```
grunt.loadNpmTasks('grunt-contrib-uglify');
```

#### 任务注册代码

最后一步是注册一个总任务名称，总任务里面包含了`任务配置代码`中的哪些任务。

```
grunt.registerTask('compass',[`uglify`])
```

翻译过来就是：我要执行一个总任务，任务名称是`compass`，这个任务里面包含了`uglify`里面的所有子任务（也就是`bananer`和`build`）。

如果只想执行`uglify`里面的`build`子任务，可以这样写：

```
grunt.registerTask('compass',['uglify:build'])
```

最后在命令行里面输入
```
grunt compass
```

工具就会自动帮你压缩js代码了。
是不是很酷！

**这里需要注意的是，task 的命名不能与后面的任务配置同名，也就是说这里的 compress 不能命名成 uglify，这样会报错或者产生意外情况**

这样一个基本的完整的grunfile.js文件就完成了！

## grunt任务一些基本模板

上面的事例只能压缩单个文件，如果想要压缩`develope`文件夹里面的所有js，然后把压缩后的代码放到`js`文件里面该怎么做呢？

很简单！把`build`任务下面的代码换成下面这个

```
        uglify: {
            options: {
                banner: '/*! <%= pkg.name %> <%=grunt.template.today("yyyy-mm-dd") %> */\n'
            },
            build: {
                files: [
                    {
                        expand: true,
                        //相对路径
                        cwd: 'develope/',
                        src: '*.js',
                       //src: ['**/*.js', '!**/*.min.js'],  //不包含某个js,某个文件夹下的js
                        dest: 'js/',
                        rename: function (dest, src) {  
                                  var folder = src.substring(0, src.lastIndexOf('/'));  
                                  var filename = src.substring(src.lastIndexOf('/'), src.length);  
                                  //  var filename=src;  
                                  filename = filename.substring(0, filename.lastIndexOf('.'));  
                                  var fileresult=dest + folder + filename + '.min.js';  
                                  grunt.log.writeln("现处理文件："+src+"  处理后文件："+fileresult);  

                                  return fileresult;  
                                  //return  filename + '.min.js';  
                              } 
                    }
                ]
            }
        }
```

具体用法代码注释已经写得很清楚的，不再赘述。

压缩js还可以这样写：
```
     uglify: {
         options: {
         },
         dist: {
             files: {
                 'assets/js/default.min.js': 'assets/js/default.js'
             }
         }
     },
```

前面是目标地址，后面才是源文件地址。


压缩css可以这样仿照上面的压缩js：
```
      cssmin: {
            //文件头部输出信息
            options: {
                banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n',
                //美化代码
                beautify: {
                    //中文ascii化，非常有用！防止中文乱码的神配置
                    ascii_only: true
                }
            },
            my_target: {
                files: [
                    {
                        expand: true,
                        //相对路径
                        cwd: 'css/',
                        src: '*.css',
                        dest: 'dest/css/',
                        rename: function (dest, src) {  
                                var folder = src.substring(0, src.lastIndexOf('/'));  
                                var filename = src.substring(src.lastIndexOf('/'), src.length);  
                                //  var filename=src;  
                                filename = filename.substring(0, filename.lastIndexOf('.'));  
                                var fileresult=dest + folder + filename + '.min.css';  
                                grunt.log.writeln("现处理文件："+src+"  处理后文件："+fileresult);  

                                return fileresult;  
                              //return  filename + '.min.js';
                                }
                    }
                ]
            }
        }
```

如果想要把三个js文件合并成一个js文件怎么写呢？使用concat插件即可！

```
     concat: {
         options: {
             separator: ';',
             stripBanners: true
         },
         dist: {
             src: [
                 "js/config.js",
                 "js/smeite.js",
                 "js/index.js"
             ],
             dest: "assets/js/default.js"
         }
     }
```


cssmin插件还可以帮助我们同时进行css文件的合并和压缩。酷！

```
        cssmin: {
            options: {
                keepSpecialComments: 0
            },
            compress: {
                files: {
                    'assets/css/default.css': [
                        "css/global.css",
                        "css/pops.css",
                        "css/index.css"
                    ]
                }
            }
        }
```

## grunt.initConfig方法

上面给出的是一些grunt处理任务的模板，关于如何正确配置，下面有一些grunt.initConfig的规则：

就cssmin来讲，minify目标的参数具体含义如下：

expand：如果设为true，就表示下面文件名的占位符（即*号）都要扩展成具体的文件名。

cwd：需要处理的文件（input）所在的目录。

src：表示需要处理的文件。如果采用数组形式，数组的每一项就是一个文件名，可以使用通配符。

dest：表示处理后的文件名或所在目录。

ext：表示处理后的文件后缀名。

## 参考文章

[前端js和css的压缩合并之grunt](http://www.haorooms.com/post/qd_grunt_cssjs)
[Grunt 新手一日入门](http://yujiangshui.com/grunt-basic-tutorial/#项目文件传输与协作)