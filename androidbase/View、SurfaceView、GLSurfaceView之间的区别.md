## 区别
1. View：(必须在UI的主线程中更新画面)
显示视图，内置画布，提供图形绘制函数、触屏事件、按键事件函数等；必须在UI主线程内更新画面，速度较慢。

2. SurfaceView(UI线程和子线程中都可以。在一个新启动的线程中重新绘制画面，主动更新画面)：
基于view视图进行拓展的视图类，更适合2D游戏的开发；是view的子类，类似使用双缓机制，在新的线程中更新画面所以刷新界面速度比view快。

3. GLSurfaceView：
基于SurfaceView视图再次进行拓展的视图类，专用于3D游戏开发的视图；是SurfaceView的子类，openGL专用。

## SurfaceView实现原理
https://blog.csdn.net/luoshengyang/article/details/8661317

## 参考
https://blog.csdn.net/zcmain/article/details/14454953
