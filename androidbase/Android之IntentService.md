## 概述
IntentService继承自Service，在IntentService的onCreate()方法中会创建一个工作线程ServiceHandler，工作线程ServiceHandler的Looper是由HandlerThread获得的。当工作线程中的任务处理完毕后，IntentService会调用stopSelf()自动停止。

## 启动IntentService为什么不需要新建线程？
在IntentService的onCreate()方法中会自己创建一个工作线程ServiceHandler

## 为什么不建议使用onBind()方式启动IntentService
IntentService的onBind()方法返回是null，且用onBind()方式启动回调不到ServiceHandler中的handleMessage中，从而也回调不到onHandleIntent中

## 多次启动IntentService会顺序执行，停止服务后，后续事件得不到执行
如果服务停止，会清除掉消息队列中的消息，使后续事件得不到执行

## 参考
https://www.jianshu.com/p/332b6daf91f0
