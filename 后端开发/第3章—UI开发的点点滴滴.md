# 第3章—UI开发的点点滴滴

## 3.1 如何编写程序界面

**不建议使用可视化编辑工具**，因为不具有很好的屏幕适配性。

## 3.2 常用控件的使用方法

### 3.2.1 TextView

```xml
<LinearLayout xmlns:android = "http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_height="match_parent"
    android:layout_width="match_parent">
    <TextView
        android:id="@+id/text_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="This is TextView"/>
</LinearLayout>
```

*    `android:id`：定义唯一标识符

*    `android:layout_height`、`android:layout_width`：定义控件的宽度和高度。Android的所有控件都具有这两个属性，可选值有三种：

     *    `match_parent`：表示让当前控件的大小和父布局的大小一样
     *    `fill_parent`：同上
     *    `wrap_content`：表示让当前的控件的大小能够**刚好包含里面的内容**

     除了使用上述值，也可以直接指定控件的宽和高的固定大小，但是有时在不同手机的屏幕的适配方面会出现问题。

*    `android:text`：指定TextView中显示的文本内容

*    `android:gravity`：指定文字的对齐方式，可选值有top、buttom、lefe、right、center等

*    `android:textSize`：指定文字的大小，使用sp作为单位

*    `android:textColor`：指定文字的颜色

### 3.2.2 Button

*    `andorid:textAllCaps`：控制是否将所有的英文字母自动进行大写转换

监听按钮的点击事件有两种写法：

1.   **匿名类的方式注册监听器**

```java
button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                
            }
        });
```

2.   **使用实现接口的方式注册**

```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button button = (Button) findViewById(R.id.button);
        button.setOnClickListener(this);
    }

    @Override
    public void onClick(View view) {
        switch (view.getId()){
            case R.id.button:
                break;
            default:
                break;
        }

    }
}

```

这样，注册按钮注册监听事件的时候，只需要写就可以了：

```java
button.setOnClickListener(this);
```



### 3.2.3 EditText

该控件允许用户在控件里输入和编辑内容，并可以在程序中对这些内容进行处理。

```xml
<EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/edit_text" />
```



**Android控件的用法都很相似**：

给控件定义一个ID，再定义控件的宽度和高度，然后再适当的加入一些控件特有的属性就差不多了。

*    `android:hint = "Type something here"`：输入框的提示信息
*    `android:maxLines`：指定输入框的最大行数

可以通过`editView.getText().toString()`来获取输入框内的文字。

### 3.2.4 ImageView

*    `android:src`：用来指定图片地址，图片放在drawable目录下，使用格式为@drawable/img_1。

还可以通过`setImageResource(R.drawable.img_2)`函数来更换图片地址。

### 3.2.5 ProgressBar

progressBar用于在界面上显示一个进度条，表示我们的程序正在加载一些数据。

```xml
<ProgressBar
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/progress_bar"/>
```

可以通过使用`setVisibility()`方法设置该控件的可见性的属性：visibility。

该属性可选值有3种：visible 、invisible、gone(表示控件不仅不可见，而且不再占用任何屏幕空间)。

```java
progressBar.setVisibility(View.GONE);
```



还可以变成水平进度条：

```xml
style="?android:attr/progressBarStyleHorizontal"
```



### 3.2.6 AlertDialog

在当前的界面弹出一个对话框，这个对话框是置顶于所有界面元素智商的，能够屏蔽掉其他的控件的交互能力。因此AlertDialog一般用来提示一些非常重要的内容或者警告信息。

```java
AlertDialog.Builder dialog = new AlertDialog.Builder(MainActivity.this);
                dialog.setTitle("This is Dialog");
                dialog.setMessage("Something important");
                dialog.setCancelable(false);
                dialog.setPositiveButton("OK", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {

                    }
                });
                dialog.setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {

                    }
                });
                dialog.show();
```



首先通过`AlertDialog.Builder`创建一个AlertDialog的实例，然后使用`setTitle`、`setMessage()`、`setCancelable`、`setPositiveButton`、`setNegativeButton`分别设置标题、内容、可否取消以及确定按钮的点击事件和取消按钮的点击事件。

setCancelable 表示不能通过Back键去掉显示对话框的。

最后调用`show()`显示对话框。

### 3.2.7 ProgressDialog

与上面不同的是，会在对话框中显示一个进度条，一般用于表示当前操作比较耗时，让用户耐心等待。

```java
ProgressDialog progressDialog = new ProgressDialog(MainActivity.this);
                progressDialog.setTitle("This is ProgressDialog");
                progressDialog.setMessage("Loading……");
                progressDialog.setCancelable(true);
                progressDialog.show();
```



## 3.3 详解4种基本布局

布局是一种可用于放置很多控件的容器，它可以按照一定的规律调整内部控件的位置。

布局的内部除了放置控件外，也可以放置布局，通过多层布局的嵌套，可以完成一些比较复杂的界面。

### 3.3.1 线性布局

LinearLayout又称作线性布局。会将它所包含的控件在线性方向上依次排列。

*    通过`android:orientation`属性指定了排列方向，可选值有vertical和horizontal。

**注意：**如果LinearLayout的排列方向是 horizontal，内部的控件的**宽度就不能指定为match_parent**，同理，排列方向是 vertical，内部控件的**高度就不能指定为match_parent**。

*    通过`android:layout_weight`使用权重的方式**指定控件的大小**（如果是水平布局，则指定宽度，否则指定高度）。这个属性是用在控件属性上的。



### 3.3.2 相对布局

RelativeLayout又称作相对布局。它可以通过相对定位的方式让控件出现在布局的任何位置。



**相对父布局定位：**

```xml
<RelativeLayout xmlns:android = "http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button1"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true"
        android:text="Button 1"/>

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button2"
        android:layout_alignParentRight="true"
        android:layout_alignParentTop="true"
        android:text="Button 2"/>

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button3"
        android:layout_centerInParent="true"
        android:text="Button 3"/>

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button4"
        android:layout_alignParentBottom="true"
        android:layout_alignParentLeft="true"
        android:text="Button 4"/>

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button5"
        android:layout_alignParentBottom="true"
        android:layout_alignParentRight="true"
        android:text="Button 5"/>
</RelativeLayout>
```



如上所示，使用了`android:layout_alignParentLeft`、`android:layout_alignParentTop`、`android:layout_alignParentBottom`、`android:layout_centerInParent`的属性。



**相对于控件进行定位：**



```xml
<RelativeLayout xmlns:android = "http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button3"
        android:layout_centerInParent="true"
        android:text="Button 3"/>
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button1"
        android:layout_above="@+id/button3"
        android:layout_toLeftOf="@+id/button3"
        android:text="Button 1"/>
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button2"
        android:layout_above="@+id/button3"
        android:layout_toRightOf="@+id/button3"
        android:text="Button 2"/>
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button4"
        android:layout_below="@+id/button3"
        android:layout_toLeftOf="@+id/button3"
        android:text="Button 4"
        />
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button5"
        android:layout_below="@+id/button3"
        android:layout_toRightOf="@+id/button3"
        android:text="Button 5"/>
</RelativeLayout>
```



*    `android:layout_above`和`android:layout_below`属性的可选值是控件的id,即让一个控件位于另一个控件的上方或者下方。
*    `android:layout_toRightOf`和`android:layout_toLeftOf`表示让一个控件位于另一个控件的右侧和左侧。
*    `android:layout_alignLeft`表示让一个控件的左边缘和另一个控件的左边缘对齐
*    `android:layout_alignRight`表示让一个控件右边缘和另一个控件的右边缘对齐。

### 3.3.3 帧布局

FrameLayout 又称作帧布局。

所有的控件都会默认摆放在**布局的左上角**。

*    `android:layout_gravity`指定控件的对齐方式

### 3.3.4 百分比布局

在这种布局中，我们可以**不再使用`wrap_content`和`match_parent`等方式来指定控件的大小，而是允许直接指定控件在布局中所占的百分比**。

百分比布局只为`Frame-layout`和`RelativeLayout`进行了功能扩展，形成了`PercentFrameLayout`和`PercentRelativeLayout`两个全新的布局。

首先需要在`app/build.gradle`配置文件中引入，在点下`sync now` 按钮即可：

```xml
compile 'com.android.support:percent:24.2.1'
```

修改布局文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.percent.PercentFrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app = "http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/button1"
        android:layout_gravity="left|top"
        android:text="Button 1"
        app:layout_heightPercent="50%"
        app:layout_widthPercent="50%"/>

    <Button
        android:id="@+id/button2"
        android:layout_gravity="right|top"
        android:text="Button 2"
        app:layout_heightPercent="50%"
        app:layout_widthPercent="50%" />


    <Button
        android:id="@+id/button3"
        android:text="Button3"
        android:layout_gravity="left|bottom"
        app:layout_widthPercent = "50%"
        app:layout_heightPercent = "50%" />
    <Button
        android:id="@+id/button4"
        android:text="Button 4"
        android:layout_gravity = "right|bottom"
        app:layout_widthPercent = "50%"
        app:layout_heightPercent = "50%" />
</android.support.percent.PercentFrameLayout>

```

最外场使用了`PercentFrameLayout`，由于百分比布局不是内置在系统的SDK中，所以**需要把完整的包路径写出来**。然后还必须定义一个app的命名空间，这样才能使用百分比布局的自定义属性。

*    `app:layout_widthPercent`:指定按钮的宽度为布局的50%
*    `app:layout_heightPercent`:指定控件的高度为布局的50%

PercentFrameLayout 布局 是继承FrameLayout的特性。



## 3.4 创建自定义控件

### 3.4.1 引入自定义布局



**创建一个标题栏布局（title.xml）：**



```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@drawable/title_bg">

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/title_back"
        android:layout_gravity="center"
        android:layout_margin="5dp"
        android:text="Back"
        android:textColor="#fff"
        android:background="@drawable/back_bg"/>

    <TextView
        android:id="@+id/title_text"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:gravity="center"
        android:text="Title Text"
        android:textColor="#fff"
        android:textSize="24sp"/>

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/title_edit"
        android:layout_gravity="center"
        android:layout_margin="5dp"
        android:text="Edit"
        android:textColor="#fff"
        android:background="@drawable/edit_bg"/>

</LinearLayout>
```



*    `android:background`:用来指定控件的背景图片
*    `android:layout_margin`：用来指定控件在上下左右方向上偏移的距离

最后在主活动的`activity_main.xml`引入该布局即可：

```xml
    <include layout="@layout/title"></include>
```



**隐藏系统自带的标题栏：**

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    ActionBar actionBar = getSupportActionBar();
    if (actionBar != null){
        actionBar.hide();
    }
}
```





### 3.4.2 创建自定义控件



首先要知道： 自定义控件 =  布局文件 + 控件的各种事件方法



上面的自定义布局，只是简单的引入布局，并不算是自定义控件。



**创建自定义控件类：（TitleLayout.java）**

```java
public class TitleLayout extends LinearLayout {
    public TitleLayout(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        LayoutInflater.from(context).inflate(R.layout.title,this);
    }
}
```

然后在`activity_main.xml`中**不再简单的引入布局文件，而是引入自定义控件**，和引入普通控件的格式一样：

```xml
<com.example.hewro.uicustomviews.TitleLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
```



最后就是在`TitleLayout.java`中写出相关控件的的方法：



```java
        Button titleBack = (Button)findViewById(R.id.title_back);
        Button titleEdit = (Button)findViewById(R.id.title_edit);

        titleBack.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View view) {
                ((Activity)getContext()).finish();
            }
        });

        titleEdit.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(getContext(),"You clicked Edit button", Toast.LENGTH_SHORT).show();
            }
        });
```



## 3.5 最常用和最难用的控件—ListView

当我们程序有大量的数据需要展示的时候，就可以借助ListView 来实现。ListView 允许用户通过手机上下滑的方式将屏幕外的数据滚动到屏幕内，同时屏幕上原有的数据则会滚出屏幕。



### 3.5.1 简单用法



1.   在布局文件添加ListView的控件

```xml
<ListView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/list_view">
    </ListView>
```

但这时候的ListView是没有内容的！！

2.   需要在启动函数中添加内容：

```java
ArrayAdapter<String> adapter = new ArrayAdapter<String>(MainActivity.this, android.R.layout.simple_list_item_1,data);
ListView listView = (ListView) findViewById(R.id.list_view);
listView.setAdapter(adapter);
```

使用`setAdapter()`函数设置ListView的内容，**接收的参数是ArrayAdapter 适配器**。

构造`ArrayAdapter`需要三个参数：当前上下文，ListView**子项布局**的ID，以及需要适配的数据。

**注意**：我们使用了`android.R.layout.simple_list_item_1`作为ListView子项布局的ID，这是一个Android内置的布局文件，里面只有一个TextView,可用于简单的显示一段文本。



### 3.5.2 定制ListView的界面

上面的界面之所以简单，是因为我们在构建适配器的时候简单的使用了`android.R.layout.simple_list_item_1`。只能显示一段文本。所以如果定制的话

**第一步就是自定义布局（fruit.xml）**：

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ImageView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/fruit_image"/>
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/fruit_name"
        android:layout_gravity="center_vertical"
        android:layout_marginLeft="10dp"/>
</LinearLayout>
```

在简单的例子中因为我们只显示一段文字，所以适配器的类型是`String`，但现在想要显示图片+文字，所以：

**第二步就是自定义适配器的数据类型（新建类Fruit）**：

```java
public class Fruit {
    private String name;
    private int imageId;

    public Fruit(String name,int imageId){
        this.name = name;
        this.imageId = imageId;
    }

    public String getName(){
        return name;
    }

    public int getImageId(){
        return imageId;
    }
}
```



**第三步就是自定义适配器（FruitAdapter）继承自ArrayAdapter，并将泛型指定为Fruit类**：

简单例子中，我们直接使用的`ArrayAdatpter<String>`

```java
ArrayAdapter<String> adapter = new ArrayAdapter<String>(MainActivity.this, android.R.layout.simple_list_item_1,data);
```



但是由于这里我们的数据类型是自定义数据类型，当我们滚动屏幕时候，需要获得的内容类型不同，所以需要新建一个适配类，继承原来的适配，并且重写`getView()`方法：

```java
public class FruitAdapter extends ArrayAdapter {
    private int resourceId;

    public FruitAdapter(@NonNull Context context, @LayoutRes int resource, @NonNull List <Fruit> objects) {
        super(context, resource, objects);
        resourceId = resource;

    }

    @NonNull
    @Override
    public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        Fruit fruit = (Fruit) getItem(position);
        View view = LayoutInflater.from(getContext()).inflate(resourceId,parent,false);
        ImageView fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
        TextView fruitName = (TextView) view.findViewById(R.id.fruit_name);
        fruitImage.setImageResource(fruit.getImageId());
        fruitName.setText(fruit.getName());
        return view;

    }
}

```

在这个自定义的适配器类中，主要是**重写了getView函数**(用于滚动屏幕的时候返回布局)：

*    首先通过getItem方法得到当前项的Fruit实例，然后**使用LayoutInflater来为这个子项加载我们传入的布局**。
*    设置布局中的ImageView和TextView的内容
*    最后返回布局。



**最后一步是ListView 设置接收这个自定义适配器（fruitAdapter）:**

```java
        initFruits();
        FruitAdapter adapter = new FruitAdapter(MainActivity.this,R.layout.fruit_item,fruitList);
        ListView listView = (ListView) findViewById(R.id.list_view);
        listView.setAdapter(adapter);
```





### 3.5.3 提升ListView的效率



当ListView快速滚动的时候，会多次的调用getView函数，就会带来性能上的问题。

查看上一节的第三步代码，可以发现有两处地方可以通过缓存的方式优化：



**每次调用的时候，借助已存在的converView参数缓存布局（view）:**

```java
View view = LayoutInflater.from(getContext()).inflate(resourceId,parent,false);
```

普通的写法如上，每次getView的时候，都会去寻找ListView的布局文件。

`converView`参数用于将之前加载好的布局进行缓存，通过判断`converView`来决定是否要重新寻找布局文件。

```java
        if (convertView == null){
            view = LayoutInflater.from(getContext()).inflate(resourceId,parent,false);   
        }else {
            view = convertView;
        }
```



**自定义ViewHolder变量缓存布局中的控件位置：**

尽管如果布局文件已经缓存，但是每次仍然都要去寻找布局文件的控件：

```java
ImageView fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
TextView fruitName = (TextView) view.findViewById(R.id.fruit_name);
```



所以我们创建一个新的变量：`viewHoloder`来记录布局文件里的控件位置：

```java
        if (convertView == null){
            view = LayoutInflater.from(getContext()).inflate(resourceId,parent,false);
            viewHolder = new ViewHolder();
            viewHolder.fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
            viewHolder.fruitName = (TextView) view.findViewById(R.id.fruit_name);
            view.setTag(viewHolder);

        }else {
            view = convertView;
        }

        viewHolder = (ViewHolder) view.getTag();
        viewHolder.fruitImage.setImageResource(fruit.getImageId());
        viewHolder.fruitName.setText(fruit.getName());


    class ViewHolder{
        ImageView fruitImage;
        TextView fruitName;
    }
```



这里的viewHolder变量是一个内部类的实例，因为需要存储两个数据。

*    如果view没被缓存，首先寻找布局文件，其次寻找布局文件里面的控件，在通过view.setTag()，把布局文件里面的控件位置缓存到view里。
*    如果view被缓存了，直接通过`getTag()`从view将布局文件的控件位置取出即可，无需再次寻找控件。

这里最为关键的两个方法是：`setTag()`和`getTag()`。

### 3.5.4 ListView的点击事件

```java
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
                Fruit fruit = fruitList.get(i);
                Toast.makeText(MainActivity.this,fruit.getName(), Toast.LENGTH_SHORT).show();
            }
        });
```



使用`setOnItemClickListener`为ListView 每项注册一个点击事件的监听器。

## 3.6 更强大的滚动控件—RecycleView

RecycleView 是一个增强版的ListView。

### 3.6.1 RecycleView的基本用法

需要在`build.gradle`配置文件中引入：

```xml
    compile 'com.android.support:recyclerview-v7:26.0.0-alpha1'
```



### 3.6.2 实现横向滚动和瀑布流布局



### 3.6.3 RecyclerView 的点击事件





## 3.7 编写界面的最佳实践

