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

## 三、注意事项
#### demo1
handler.post(runnable);
view.post(runnable);
activity.postOnUIThread(runnable)
上述三个runnable都是在主线程执行的，不能进行耗时操作。

#### demo2
handler.postDelay(runnable);
runnable中存在潜在的内存泄漏
