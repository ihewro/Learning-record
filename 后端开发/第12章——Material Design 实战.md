# 第12章——Material Design 实战

## 12.2 ToolBar





## 12.3 滑动菜单





## 12.4 悬浮按钮和可交互提示

### 12.4.2 snackbar

```java
Snackbar.make(view, "Data deleted", Snackbar.LENGTH_SHORT)
                        .setAction("Undo", new View.OnClickListener(){
                            @Override
                            public void onClick(View view) {
                                Toast.makeText(MainActivity.this,"数据已删除",Toast.LENGTH_SHORT).show();
                            }
                        })
                        .show();
```

### 12.4.3CoordinatorLayout



### 12.5 卡片式布局

### 12.5.1 CardView



### 12.5.2 AppBarLayout







## 12.6 下拉刷新



## 12.7 可折叠式标题栏

