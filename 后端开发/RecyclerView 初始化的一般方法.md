记录以便复用。

## 1. 布局文件中写入RecyclerView

```xml
<android.support.v7.widget.RecyclerView
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/rank_list_exhibition_recycler_view"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="cn.edu.buct.areatour.features.exhibition.search.rank.RankItemFragment" />

```

## 2. 新建Adapter

recyclerView 使用过程中需要使用适配器（Adapter）绑定数据的。

recyclerView使用过程中分为两种情况：
* 每一个条目的布局都是重复，仅有数据不同
* 每一个条目的布局是不一样的

这两种不同的情况在本项目中都有使用到。

第一种比如景区列表的RecyclerView，以图搜图的识别结果的显示等等都是这种简单的情况。
第二种比如搜索界面的RecyclerView 就分为两种布局：一个是{大家都在搜}，一个是{常用栏目（如景区排行榜、二维码搜索这些栏目）}。

下面就这两种不同情况，分别介绍相应的adapter的创建情况：

### 2.1 每个条目布局是重复的

下面以{以图搜图搜索结果显示的RecyclerView}为例（search/searchbyimage/SearchByImageResultAdapter.java）

> **1. 新建adapter 继承 `RecyclerView.Adapter<RecyclerView.ViewHolder>`**

因为`RecyclerView.Adapter`是一个抽象类，所以使用必须先新建一个子类继承该类。

```java
public class SearchByImageResultAdapter extends RecyclerView.Adapter<RecyclerView.ViewHolder> {
    @Override
    public RecyclerView.ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        return null;
    }

    @Override
    public void onBindViewHolder(RecyclerView.ViewHolder holder, int position) {

    }

    @Override
    public int getItemCount() {
        return 0;
    }
}
```

> **2. 重写父类的三个方法**

这里必须重写父类的三个方法分别是：

* `onCreateViewHolder()`: 在这里面引入**子项的布局文件**，并返回该布局的ViewHoder对象。我们可以暂时将**ViewHoder理解为RecyclerView中每个子项的数据的容器。**

* `onBindViewHolder()`：上面的方法仅仅是引入了子项的布局文件，每个子项的数据一般都在这个函数里面赋值，处理。

* `getItemCount()`：返回子项的数目

这里必须更详细的介绍`ViewHolder`，ViewHoder也是一个类的实例。

因为`RecyclerView.ViewHolder`也是一个抽象类，所以对于**我们特定子项的数据容器**，必须新建一个子类继承该父类。

```java
    class SearchByImageResultsViewHolder extends RecyclerView.ViewHolder {

        TextView searchRank;
        TextView searchName;
        TextView searchCalorie;
        TextView searchConfidence;
        View ll_search_calorie;

        public SearchByImageResultsViewHolder(View itemView) {
            super(itemView);
            searchRank = itemView.findViewById(R.id.search_rank);
            searchName = itemView.findViewById(R.id.search_name);
            searchConfidence = itemView.findViewById(R.id.search_confidence);
            searchCalorie = itemView.findViewById(R.id.search_calorie);
            ll_search_calorie = itemView.findViewById(R.id.ll_search_calorie);
        }

    }
```

在ViewHoder的构造函数里面，我们一般是绑定子项布局中的组件ID，**以便我们可以在onBindViewHolder()通过hoder.ll_search_calorie 来为组件赋值。**

更值得一提是的`getItemCount()`返回的数目一般不是我们手动填写整数，而是我们在这个适配的构造函数中，会传递一个数据List，ItemCount即该List的大小。即

```java
    private List<ImageSearchResultsModule> moduleList;

    public SearchByImageResultAdapter(List<ImageSearchResultsModule> moduleList) {
        this.moduleList = moduleList;
    }

    @Override
    public int getItemCount() {
        return moduleList.size();
    }
```

【小结】：
按照我的理解:

Adapter相当于该组件(RecyclerView)的数据源，ViewHoder就是该组件子项的数据源。
我们在`onCreateViewHolder()`创建每个子项的ViewHolder。
在`onBindViewHolder()`为每个子项赋值。

### 2.2 每个条目是不同的

这里以搜索界面的SearchContentAdapter为例（search/SearchContentAdapter.java）

> **1. 新建adapter 继承 `RecyclerView.Adapter<RecyclerView.ViewHolder>`**

```java
public class SearchContentAdapter extends RecyclerView.Adapter<RecyclerView.ViewHolder> {
  
	@Override
    public RecyclerView.ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
    
    }
	@Override
    public void onBindViewHolder(RecyclerView.ViewHolder holder, int position) {
        
    }
    @Override
    public int getItemViewType(int position) {
		
    }

    @Override
    public int getItemCount() {
        return 2;
    }
}
```
>    **2. 重写父类的四个方法**

这里是和上面的情况的最大区别，需要多重写一个函数`getItemViewType()`。

如果够细心的话，你会发现`onCreateViewHolder()`函数中有一个`viewType`参数，我们在第一种情况下根本用不到。

**每个不同的条目都一种不同的ViewType**。

比如，我们的搜索界面中，

{大家都在搜}是一个布局文件，我把它的viewType命名为：

```java
    private static final int SEARCH_HOT_INFO = 0;
```

{很多栏目（如景区榜、二维码搜索）}是另一个布局，我把它的viewType命名为：

```java
    private static final int SEARCH_COLUMN = 1;
```

这样在**创建子项的ViewHolder，根据不同的viewType引入不同的子项布局文件，返回不同的ViewHolder**：

```java
    @Override
    public RecyclerView.ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {

        if (viewType == SEARCH_HOT_INFO) {
            View view = LayoutInflater.from(UIUtils.getContext()).inflate(R.layout.item_search_hot_info, parent, false);
            return new SearchHotInfoViewHolder(view);

        } else if (viewType == SEARCH_COLUMN) {

            View view = LayoutInflater.from(UIUtils.getContext()).inflate(R.layout.item_search_colum, parent, false);
            return new SearchColumnViewHolder(view);
        }
        return null;
    }
```



`getItemViewType()`接收的参数是`position`。也是手机屏幕从上往下滑动的位置，从上往下依次是0 、1、2……

你可能会疑惑这个position的高度到底多高，到底多大的范围是属于这个position的。

**事实上，position是根据你的子项来分的：**

```java
    @Override
    public int getItemViewType(int position) {
        if (position == 0){
            return SEARCH_HOT_INFO;
        }else if (position == 1){
            return SEARCH_COLUMN;
        }
        return super.getItemViewType(position);
    }
```

上面这部分代码基本上是个模板，按照这上面套写即可，即使你可能暂时不是很理解。



## 3.将RecyclerView组件与该Adapter数据源绑定起来 

这部分内容基本是固定的。

```java
        searchImageResultRecyclerView.setLayoutManager(new LinearLayoutManager(UIUtils.getContext()));
        SearchByImageResultAdapter adapter = new SearchByImageResultAdapter(moduleList);
        searchImageResultRecyclerView.setAdapter(adapter);
```

这三行代码尤其最容易丢的是第一行代码。一定要多注意。



