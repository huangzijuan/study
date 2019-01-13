## 一、 设计目的
因为android中更新UI只能在主线程中执行，而UI线程中确不能执行耗时任务，Handler为了进行异步执行耗时任务提供了方便。

## 二、工作机制
Thread  负责业务逻辑
Handler  负责发送消息和处理消息
MessageQueue  负责保存消息
Looper  负责轮询消息队列

#### Handler构造方法
1. 创建looper
2. 创建MassageQueue

#### ThreadLocal
实现不同线程的数据副本

#### Looper.prepare()
在Looper类中申明一个 static final类型的 ThreadLocal<Looper>
1. 创建了一个looper（一个looper对应一个消息队列，对应一个线程）
   创建了消息队列
   创建线程
2. 将这个looper放在ThreadLocal中

#### 消息入队
1. 为msg设置了target，target代表了消息的来源是哪一个handler
2. 判断消息在消息队列中的位置是 根据时间uptimeMilllis来判断的，时间越小排在队列越前面，时间越大排到队列越后面
#### 消息出队
由Looper.loop()从ThreadLocal中取出looper中消息队列中的msg
#### 消息处理
由handler的dispatchMassge()处理消息
优先msg的callback；其次handler构造方法传入的callback；最后handleMessage();

#### Message.obtain()方法
直接从MessagePool中拿已经存在的message，省去了创建对象、申请内存的开销。

## 三、注意事项
#### demo1
handler.post(runnable);
view.post(runnable);
activity.postOnUIThread(runnable)
上述三个runnable都是在主线程执行的，不能进行耗时操作。

#### demo2
handler.postDelay(runnable);
runnable中存在潜在的内存泄漏

## 四、细节点
1. 为什么主线程不会因为Looper.loop()方法而造成阻塞
activity 的生命周期都是对应的 ActivityThread 的 Handler 的 handleMessage 方法。主线程确实必须是阻塞的，如果不加入looper作死循环，当run()方法走完之后，系统就会回收线程所占用的资源。
2. msg有哪些属性
public Messenger replyTo;
public int what;
public Object obj;

Bundle data;
Handler target;
Runnable callback;
3. 阻塞操作的地方
public static void loop() {
        ......
        for (;;) {
            Message msg = queue.next(); // might block  在这儿队列阻塞了
            ......
            msg.target.dispatchMessage(msg);//里面调用了handler.handleMessage()
        }
    }


## 解决内存泄漏
1、声明一个继承Runnable类的静态内部类，并弱引用要操作的控件

2、在onDestroy()中调用removeCallbacksAndMessages()

3、调用Badoo团队的WeakHandler来替代os.Handler

666、WeakHandler只能替代postDelay(New Runnable())方法造成的内存泄漏，没办法替代os.Handler中接收消息的操作，所以正常情况下需要调用方法(2)



参考：https://blog.csdn.net/jbb0403/article/details/75109890
