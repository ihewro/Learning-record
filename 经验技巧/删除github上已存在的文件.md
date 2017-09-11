### 本地远程同步删除

```
git rm -rf <文件夹名称>
git rm <文件名称>
git commit -m "Remove some thing"
git push origin master
```

### 只删除远程文件

本地下次不想提交的，**需要加入到`.gitignore`文件里。**

```
git rm -rf --cached <文件夹名称>
git rm --cached <文件名称>
git commit -m "Remove some thing"
git push origin master
```
