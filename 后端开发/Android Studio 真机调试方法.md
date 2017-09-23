# Android Studio 真机调试方法

 mac OS 系统

华为手机

## 设备连接到AS

```bash
system_profiler SPUSBDataType
```

在终端输入该命令，然后找到手机的`Product ID`和`Vendor ID`：

![](https://ws1.sinaimg.cn/large/006tKfTcly1fjtk6x1v4qj310y0rwwic.jpg)复制到

nano ~/.android/adb_usb.ini 文件里面。



![](https://ws4.sinaimg.cn/large/006tNc79ly1fjtk77skenj310y0rw76j.jpg)



最重要的是开启**USB调试模式**！！！

## AS 不显示程序的logcat信息

1.   拨号界面输入：*#*#2846579#*#*   进入测试菜单选择界面。（一般手机都有，但不是全部，比如联想部分机型等）
2.   ProjectMenu – 后台设置 – LOG设置
3.   LOG打开

还是无法输出的话，可以尝试重启手机。



