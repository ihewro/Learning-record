---
title: Java 的一些基本概念
date: 2017-02-28 22:19:43
tags:
---

### JAVA SE ，JAVA ME，JAVA EE 的区别

**1990年** 詹姆斯·高斯林 （Sun公司员工）等人开发Java雏形，命名为 Oak（橡树）.

**1995年** Sun 公司看到Oak的未来,以JAVA名称正式发布

**1998年** Sun公司发表JDK 1.2版本时候，使用了新名称Java 2 Platform，即“Java2平台”。修改后的JDK称为Java 2 Platform Software Developing Kit，即J2SDK。并分为分个版本：
1. J2SE —— 全称为Java Standard Edition，即标准版。
2. J2EE —— 全称 Java Enterprise Edition，即企业版
3. J2ME —— 全称 MicroEdition，即微型版

**2005年** Java的各种版本已经更名以取消其中的数字“2”了，即J2EE更名为Java EE, J2SE更名为Java SE，J2ME更名为Java ME。

<!--more-->


### JDK，JRE，JVM与SDK 区别

**JDK**——全称Java development toolkit，中文名称Java开发工具包。只要用来支持Java程序的开发，包括编译器（javac.exe）、开发工具（javadoc.exe、jar.exe、keytool.exe、jconsole.exe）和更多的类库（如tools.jar）等。

**JRE**——全称 Java Runtime Environment，中文名称Java运行环境。这个仅仅只是Java运行的环境，没有这个，Java无法运行，**一般JRE被包括在JDK中，也可以单独装一个独立的JRE**.

**JVM**——全称 Java Virtual Machine，中文名称 Java 虚拟机。JVM是JRE的一部分。

![jdk_jre_jvm](/images/jdk_jre_jvm.png  "jdk_jre_jvm")

上图，可以清楚的看清JDK JRE JVM 三者的联系区别。

在实际开发过程中
1. 我们首先**编写Java代码(.java)**
2. 然后通过**JDK中的编译程序（javac 命令）**将`.Java`文件编译成**Java字节码(.class)**
3. JRE加载和验证Java字节码(.class)
4. JVM解释字节码，映射到CPU指令集或O的系统调用，完成最终的程序功能。


**SDK**——全称 Software Develop Kit，中文名称 软件开发工具包。和**IDE**完全不同。可以简单理解为调用API	的工具包。各种不同类型的软件开发，都可以有自己的SDK。Windows有Windows SDK，DirectX 有 DirectX 9 SDK，.NET开发也有Microsoft .NET Framework SDK。JAVA开发当然也有自己的Java SDK。

### eclipse 的原理

**IDE**——全称 Integrated Development Environment，中文名称 集成开发环境。

eclipse是一个JAVA IDE（而不是SDK）。

eclipse本身是基于java实现的，因此，**运行eclipse的最低限度条件是JRE。**

如下图所示，在新建一个JAVA 工程的时候，是需要选择JRE 的版本的。eclipse 本身内置了一个`default JRE`。

JRE只提供了运行环境，但并没有提供编译java代码的能力，那eclipse怎么编译你的程序呢？

eclipse自己带了一个java编译器，我们通常称为`eclipse compiler`，它将`.java`文件编译成`.class`类文件。接着，eclipse会调用你的java工程绑定的jre来启动`.class`的类文件，输出信息。

![jre](/images/jre.png  "jre")


### 参考文章

[Java初学者首先下载 JDK 开发环境，然后再下 eclipse 对吗？那 tomcat是什么？还需要安装吗？](https://www.zhihu.com/question/20218920)

[J2EE,J2SE,J2ME,JDK,SDK,JRE,JVM区别](http://www.metsky.com/archives/547.html)

[SDK和API的区别？](https://www.zhihu.com/question/21691705)