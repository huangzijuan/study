
观察者模式：管理注册信息、调度方法
## 前言 常见的事件处理机制
1.Intent
2.Handler
3.BroadCastReceiver
4.Interface回调

## EventBus的优势
1.将事件发布者和订阅者之间充分解耦
2.简化了组件间的通信，使代码更简洁
3.避免了组件之间复杂的生命周期处理

## 如何使用
EventBus使用详解：https://www.jianshu.com/p/a040955194fc
(1)定义一个消息类，如：

public class MessageEvent {
    ......
}
(2)在需要订阅事件的地方注册事件

EventBus.getDefault().register(this);
(3)产生事件，即发送消息

EventBus.getDefault().post(messageEvent);
(4)处理消息

@Subscribe(threadMode = ThreadMode.MAIN)
public void XXX(MessageEvent messageEvent) {
    ...
}

## 一、注册过程
初始化EventBus
1.保存事件类型注册信息的map subscriptionsByEventType：key为事件类型，值为Subscription的列表
2.保存某个类注册的事件类型的map typesBySubscriber：key为注册的类，值为一个Event的事件列表
3.stickyEvents：记录sticky事件
4.负责线程调度的三个Poster：mainThreadPoster backgroundPoster asyncPoster

FindState:对订阅方法查找结果对封装

#### 两种生成订阅表方式
1. 运行期通过反射来生成订阅表
第一步：从池中拿出一个 FindState对象，FindState 中维护的就是我们对订阅方法查找结果的封装。
第二步：initForSubscriber() 就是将我们的订阅者传给FindState对象。
第三步：不断从订阅者和订阅者的父类去查找订阅方法
2. 利用APT技术再编译期通过事先生成的代码来构建订阅表
首先在 build.gradle 中声明编译期生成类的完整包名
android {
    defaultConfig {
        javaCompileOptions {
            annotationProcessorOptions {
                arguments = [ eventBusIndex : 'com.example.myapp.MyEventBusIndex' ]
            }
        }
    }
}

dependencies {
    compile 'org.greenrobot:eventbus:3.0.0'
    annotationProcessor 'org.greenrobot:eventbus-annotation-processor:3.0.1'
}
然后在初始化时把编译期生成的MyEventBusIndex实例插入到 DefaultBus 中

EventBus.builder().addIndex(new MyEventBusIndex()).installDefaultEventBus();

## 二、事件发送过程
第一步：遍历消息队列中的所有消息
第二步：遍历事件类型的所有父类
第三步：遍历事件类型的所有注册信息（订阅信息）
第四步：根据threadMode进行事件的分发

## 三、事件的调度
四种threadModed的情形：
1.POSTING：默认的 ThreadMode，直接再事件发送的线程中调用注册方法。
2.Main：在主线程中调用注册方法，如果事件发送线程不是主线程，则由mainThreadPoster将方法调用派送到主线程中调用。
3.Background：在后台线程中调用，如果事件发送不是在主线程，则注册方法则直接在该线程中被调用，如果在主线程发送事件，则注册方法由backgroundPoster派发到工作线程中调用；
4.Async：直接由asyncPoster派发到工作线程中调用

## 四、解注册
解注册主要是为了提高效率的，不然订阅的事件太多，会影响性能。
