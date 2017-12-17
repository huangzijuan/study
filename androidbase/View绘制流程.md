## 相关知识点
每一个Activity都与一个Window相关联，用户界面则由Window所承载

## ViewRoot
负责View绘制的整个流程，每个应用程序窗口的decorView都有一个与之关联的ViewRoot对象，这种关联关系是由WindowManager来维护的。
整个View树的绘制流程在ViewRoot.java类的performTraversals()函数展开。

## 绘制过程
View的绘制过程可以分为以下三个阶段

#### measure
判断是否需要重新计算View的大小，需要的话则计算

#### layout
判断是否需要重新计算View的位置，需要的话则计算
decorView的layout()方法的调用为布局整个控件树的起点
在setFrame()方法中会判断View的位置是否发生了改变，若发生了改变，则需要对子View进行重新布局，对子View的局部是通过onLayout()方法实现了。

#### draw
判断是否需要重新绘制View，需要的话则重新绘制

1. 绘制背景
2. 通过onDraw()绘制自身内容
3. 通过dispatchDraw()绘制子View
4. 绘制滚动条

## 参考
http://www.codekk.com/blogs/detail/54cfab086c4761e5001b253f
http://www.jianshu.com/p/060b5f68da79
