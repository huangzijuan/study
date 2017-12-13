## HandlerThread
HandlerThread是安卓API提供的一个便捷的类，能使得我们快速创建一个带有Looper的线程。（提供了一个线程专门来处理handler的消息）

#### HandlerThread的使用场景
HandlerThread比较适用于 单线程+异步队列 的场景，比如IO读写操作数据库、文件等，耗时不多也不会产生较大的阻塞。（对网络操作并不适用，因为它只有一个线程）

使用场景举例：
1. 应用刚启动时的数据初始化操作，如果开启多个线程同时执行，有可能争夺UI线程的CPU执行时间，造成卡顿，而使用该模型，通过设置优先级就可以将同步工作顺序的执行，而又不影响UI的初始化；
2. 从数据库中读取数据展现在ListView中，通过Handler的postAtFrontOfQueue方法，快速将读取操作加入队列前端执行，必要时返回给主线程更新UI；
3. HandlerThread应用在IntentService中，IntentService是一个需要长时间执行任务Service，优先级要比线程高。

参考：http://blog.csdn.net/isee361820238/article/details/52589731

## IntentService
IntentService用于执行后台耗时任务，当任务执行后它会自动停止。（由于IntentService是服务的原因，他的优先级比单纯的线程要高很多）它里面封装了HandlerThread和Handler
