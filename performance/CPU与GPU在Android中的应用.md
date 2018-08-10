## CPU
CPU负责包括Measure，Layout，Record，Execute的计算操作

## GPU
GPU负责Rasterization(栅格化)操作

## 硬件加速
硬件加速可以在一下四个级别开启或关闭：

Application
Activity
Window
View

### 基于软件的绘制模型
在软件绘制模型下，视图按照如下两个步骤绘制：

1. Invalidate the hierarchy（注：hierarchy怎么翻译？）

2. Draw the hierarchy

应用程序调用invalidate()更新UI的某一部分，失效(invalidation)消息将会在整个视图层中传递，计算每个需要重绘的区域（即脏区域）。然后Android系统将会重绘所有和脏区域有交集的view。很明显，这种绘图模式存在缺点：

1. 每个绘制操作中会执行不必要的代码。比如如果应用程序调用invalidate()重绘button，而button又位于另一个view之上，即使该view没有变化，也会进行重绘。

2. 可能会掩盖一些应用程序的bug。因为android系统会重绘与脏区域有交集的view，所以view的内容可能会在没有调用invalidate()的情况下重绘。这可能会导致一个view依赖于其它view的失效才得到正确的行为。

### 基于硬件的绘制模型
Android系统仍然使用invalidate()和draw()来绘制view，但在处理绘制上有所不同。Android系统记录绘制命令到显示列表，而不是立即执行绘制命令。另一个优化就是Android系统只需记录和更新标记为脏（通过invalidate()）的view。新的绘制模型包含三个步骤：

1. Invalidate the hierarchy

2. 记录和更新显示列表

3. 绘制显示列表

## View的layer
view都有画到离屏缓冲的能力，包括使用view的绘制cache，或使用Canvas.saveLayer()。

https://blog.csdn.net/niu_gao/article/details/7464320

## At last
提升布局性能的关键点是：尽量保持布局层级的扁平化，避免出现重复的嵌套布局。

## 参考
https://developer.android.com/guide/topics/graphics/hardware-accel
http://hukai.me/android-performance-render/
