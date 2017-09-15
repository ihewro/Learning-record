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

它可以通过相对定位的方式让控件出现在布局的任何位置。



### 3.3.3 帧布局



### 3.3.4 百分比布局

