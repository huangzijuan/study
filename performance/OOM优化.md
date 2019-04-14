## OOM发生的条件
Android 2.x系统GC LOG中的dalvik allocated + external allocated + 新分配的大小 >= getMemoryClass()值的时候就会发生OOM

Android 4.x的系统废除了external的计数器，类似Bitmap的分配改到Dalvik的Java Heap中申请。只要allocated + 新分配的内存 >= getMemoryClass()的时候就会发生OOM

## 如何避免OOM
1. 减小对象的内存占用
  1）使用更加轻量的数据结构
  2）避免在Android里面使用Enum
  3）减小Bitmap对象的内存占用
  4）使用更小的图片
2. 内存对象的重复利用
  1）复用系统自带的资源
  2）注意在ListView/GridView等出现大量重复子组件的视图里对ConvertView的复用
  3）Bitmap对象的复用
  4）避免在onDraw方法里面执行对象的创建
  5）StringBuilder
3. 避免对象的内存泄露
  1）注意Activity的泄漏(它占用的内存多，影响面广)
     内部类引用导致Activity的泄漏(在UI退出之前，执行remove Handler消息队列中的消息与runnable对象。或者是使用Static + WeakReference的方式来达到断开Handler与Activity之间存在引用关系的目的)
     Activity Context被传递到其他实例中，这可能导致自身被引用而发生泄漏。
  2）考虑使用Application Context而不是Activity Context
     Dialog的Context就必须是Activity Context
  3）注意临时Bitmap对象的及时回收
  4）注意监听器的注销
  5）注意缓存容器中的对象泄漏
  6）注意WebView的泄漏
  7）注意Cursor对象是否及时关闭
4. 内存使用策略优化
  1）谨慎使用large heap
  2）综合考虑设备内存阈值与其他因素设计合适的缓存大小
  3）onLowMemory()与onTrimMemory()
  4）资源文件需要选择合适的文件夹进行存放
  5）Try catch某些大内存分配的操作
  6）谨慎使用static对象
  7）特别留意单例对象中不合理的持有
  8）珍惜Services资源:建议使用IntentService
  9）优化布局层次，减少内存消耗
  10）谨慎使用“抽象”编程
  11）使用nano protobufs序列化数据
  12）谨慎使用依赖注入框架
  13）谨慎使用多进程
  14）使用ProGuard来剔除不需要的代码
  15）谨慎使用第三方libraries


## 参考：
https://blog.csdn.net/jdsjlzx/article/details/49107183
