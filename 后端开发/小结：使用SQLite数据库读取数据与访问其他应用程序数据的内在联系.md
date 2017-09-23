#  小结：使用SQLite数据库读取数据与访问其他应用程序数据的内在联系



## SQLite数据库读取数据



**获取数据库db：**



*    新建一个MyDatabaseHelper 继承 SQLiteOpenHelper类
*    通过` new MyDatabaseHelper(this,"BookStore.db", null, 2);`获得 MyDatabaseHelper的一个实例`dbHelper`
*    通过`dbHelper.getWritableDatabase()`获得/创建该应用程序的数据库`db`，执行这个方法的时候会调用`onCreate()`方法！在这个方法里面可以完成建表任务。



**使用数据库db的一系列方法：**



>    查找数据

`db.query(<表名>,约束条件)`返回一个cursor对象

>    增加数据

`db.insert(<表名>,null,<ContentValuse的实例>)` 

ContentValuse用来存储数据

>    更新数据

`db.update(<表名>,<ContentValuse的实例>,约束条件)`

>    删除数据

`db.delete(<表名>,约束条件)`



## 读取其他应用程序数据的方法



**获取ContentResolver类：**

*    通过Context的`getContentResolver()`方法获得`ContentResolver`类的实例，此时会调用ContentResolver类的`onCreate()`方法。



**使用ContentResolver一系列方法：**



>    查找数据

`getContentResolver().query()`

>    增加数据

`getContentResolver.insert(uri,values);`

>    更新数据

`getContentResolver.update(uri,values,"column1 = ? and column2 = ?".new String[]{"text","1"});`

>    删除数据

`getContentResolver.delete(uri,"column1 = ? and column2 = ?".new String[]{"text","1"});`



这里的uri作用 = 指定应用程序 + 指定具体的表名



## 总结

这两者对数据的查找、增加、更新、删除数据的一系列方法基本是相同，区别在于一个传入<表名>，而一个传入的是Uri对象。

前者是使用Database 对象（通过`dbHelper.getWritableDatabase`获得该对象）进行对数据库进行操作

后者通过ContentResolver对象（通过`Context的`getContentResolver()方法获得该对象）进行对数据库进行操作。