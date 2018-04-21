## RecycleView与ListView、GridView等控件相比的优点
 多样式：可以对数据的展示进行自己的定制，（线性布局、网格布局、瀑布流布局等）
 定向的刷新：可以对指定的item数据进行刷新
 刷新动画：支持对item刷新添加动画
 添加装饰：可以自定义添加分割线样式

## 内部类
RecycleView的很多核心功能都是通过内部类来实现的

RecycleView.LayoutManager   负责item视图布局的显示管理
RecycleView.ItemDecoration   给每一项item视图添加修饰的View   
RecycleView.Adapter   为每一项item创建视图
RecycleView.ViewHolder   继承item视图的子布局
RecycleView.ItemAnimator


## 参考
https://mp.weixin.qq.com/s/LAm4m9klItuQpr4Sd2_mvQ
