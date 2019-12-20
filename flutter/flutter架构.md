## Flutter架构
1. flutter framework层
可构建Widget控件以及实现UI布局
2. flutter engine层
实现了Flutter的核心库，包括Dart虚拟机、动画和图形、文字渲染、通信通道、事件通知、插件架构等。
引擎渲染采用的是2D图形渲染库Skia，虚拟机采用的是面向对象语言Dart VM，并将它们托管到Flutter的嵌入层。shell实现了平台相关的代码

## 引擎启动
APP启动过程，会执行Application和Activity的onCreate()方法，FlutterApplication和FlutterActivity的onCreate()方法正是连接Native和Flutter的枢纽。
1. FlutterApplication.java的onCreate过程主要完成初始化配置、加载引擎libflutter.so、注册JNI方法；
2. FlutterActivity.java的onCreate过程，通过FlutterJNI的AttachJNI()方法来初始化引擎Engine、Dart虚拟机、Isolate、taskRunner等对象。再经过层层处理最终调用main.dart中main()方法，执行runApp(Widget app)来处理整个Dart业务代码

#### flutter引擎启动过程
每一个FlutterActivity都有相对应的FlutterView、AndroidShellHolder、Shell、Engine、Animator、PlatformViewAndroid、RuntimeController、Window等对象。但每一个进程DartVM独有一份；

## taskRunner工作原理
Flutter引擎启动过程，会创建UI/GPU/IO这3个线程，会为这些线程依次创建MessageLoop对象，启动后处于epoll_wait等待状态。

![屏幕快照 2019-12-04 下午4.11.42](/assets/屏幕快照%202019-12-04%20下午4.11.42.png)

Flutter分为Task和MicroTask两种类型，引擎和Dart虚拟机的事件以及Future都属于Task，Dart层执行scheduleMicrotask()所产生的属于Microtask。

简单理解为先处理完所有的Microtask，然后再处理Task。因为scheduleMicrotask()方法的调用自身就处于一个Task，执行完当前的task，也就意味着马上执行该Microtask。

为了能访问GPU，IO Runner跟GPU Runner的Context在同一个ShareGroup

## dart虚拟机工作
Flutter引擎启动会创建Dart虚拟机以及Root Isolate。DartVM自身也拥有自己的Isolate，完全由虚拟机自己管理的，Flutter引擎也无法直接访问。Dart的UI相关操作，是由Root Isolate通过Dart的C++调用，或者是发送消息通知的方式，将UI渲染相关的任务提交到UIRunner执行，这样就可以跟Flutter引擎相关模块进行交互。

对于Dart程序的并发则需要依赖多个isolate来实现。

1. isolate堆是运该isolate中代码分配的所有对象的GC管理的内存存储；
2. vm isolate是一个伪isolate，里面包含不可变对象，比如null，true，false；
3. isolate堆能引用vm isolate堆中的对象，但vm isolate不能引用isolate堆；
4. isolate彼此之间不能相互引用；
5. 每个isolate都有一个执行dart代码的Mutator thread，一个处理虚拟机内部任务(比如GC, JIT等)的helper thread； 可见，isolate是拥有内存堆和控制线程，虚拟机中可以有很多isolate，但彼此之间内存不共享，无法直接访问，只能通过dart特有的Port端口通信；isolate除了拥有一个mutator控制线程，还有一些其他辅助线程，比如后台JIT编译线程、GC清理/并发标记线程；

## widget架构
1. Widget是为Element描述需要的配置， 负责创建Element，决定Element是否需要更新。Flutter Framework通过差分算法比对Widget树前后的变化，决定Element的State是否改变。当重建Widget树后并未发生改变， 则Element不会触发重绘，则就是Widget树的重建并不一定会触发Element树的重建。
2. Element表示Widget配置树的特定位置的一个实例，同时持有Widget和RenderObject，负责管理Widget配置和RenderObject渲染。Element状态由Flutter Framework管理， 开发人员只需更改Widget即可。
3. RenderObject表示渲染树的一个对象，负责真正的渲染工作，比如测量大小、位置、绘制等都由RenderObject完成

## 渲染过程
渲染过程，UI线程完成布局、绘制操作，生成Layer Tree；GPU线程执行合成并光栅化后交给GPU来处理，其中几个关键步骤：

1. Animate: 遍历_transientCallbacks，执行动画回调方法；
2. Build: 对于dirty的元素会执行build构造，没有dirty元素则不会执行，对应于buildScope()
3. Layout: 计算渲染对象的大小和位置，对应于flushLayout()，这个过程可能会嵌套再调用build操作；
4. Compositing bits: 更新具有脏合成位的任何渲染对象， 对应于flushCompositingBits()；
5. Paint: 将绘制命令记录到Layer， 对应于flushPaint()；
6. Compositing: 将Compositing bits发送给GPU， 对应于compositeFrame()；

## 参考
http://gityuan.com/flutter/
