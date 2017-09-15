---
title: Linux环境xampp本地部署wordpress遇到“上传文件ftp验证问题”
date: 2017-05-12 21:29:51
tags:
categories: wordpress
---

在Linux上面搭建了wp，上传主题的时候，告诉我要ftp账号？

喵喵喵？

我用的是xampp，也不知道ftp账号密码

找到配置文件httpd.conf，路径为： /etc/httpd.conf​

打开文件找到这一段
```
#
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.  
#
# User/Group: The name (or #number) of the user/group to run httpd as.
# It is usually good practice to create a dedicated user and group for
# running httpd, as with most system services.
#
User daemon
Group daemon ​​
```

把
```
User daemon
Group daemon ​​
```

改成
```
User 系统用户名（比如我就是hewro）
Group staff
```

然后重启一下apache服务

然后一切就都顺利了。
