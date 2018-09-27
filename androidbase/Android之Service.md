## Service的两种启动方式（对应Service的两种状态）
1. 启动状态
 1）调用startService()方法启动
 2）启动状态下的Service会在后台一直运行（即使主应用退出后依旧在运行），直至它自身通过stopSelf()结束工作，或者由另一组件通过stopService()来停止
 3）这种状态下的Service一般只负责执行任务，不会直接将结果返回给调用方（常用于：后台下载数据、处理文件）
 4）生命周期：onCreate()-->onStartCommand()-->Service running-->onDestroy()
2. 绑定状态
 1）调用bindService()启动
 2）绑定状态下的服务可以和调用组件交互（eg:发送请求、获取结果等）
 3）一个服务可以绑定多个组件，有绑定的组件才会运行，绑定的组件全部取消绑定后就会销毁（与组件是同生共死的关系）
 4）生命周期：onCreate()-->onBind()-->Service running-->onUnbind()-->onDestroy()

3. 先调用startService()，再调用bindService()方法
 1）如果结束只调用unbindService()，则只会执行到onUnbind，不会执行onDestroy()
 onCreate()-->onStartCommand()-->onBind()-->Service running-->onUnbind()
 2）如果在unbindService之后，再调用stopService()
 onCreate()-->onStartCommand()-->onBind()-->Service running-->onUnbind()-->onDestroy()

## 前台服务
1. 启动前台服务
// 参数一：唯一的通知标识；参数二：通知消息。
startForeground(110, notification);// 开始前台服务


## 开启服务还是新起线程？
影响的关键：这个任务是否在用户离开当前页面、应用后仍然在执行
1. 若希望异步任务在用户退出后就结束：选择使用 AsyncTask 或者 HandlerThread 等线程工作类，在onDestroy()时关闭线程
2. 若希望异步任务在用户推出后仍可以运行：选择 Service 或者 IntentService 等服务

## Thread与Service的区别
1. Thread的优先级低于Service的优先级，在资源紧张的情况下，会优先杀死Thread
2. Service可以跨进程访问，但Thread却不行
3. 如果任务占用CPU时间多，资源大的情况下，要使用Thread
4. 在Thread启动后，如果退出当前Activity，就无法对已启用的Thread进行操作了，但Service却可以

## 注意点
1. 默认情况下，服务在其调用组件所运行的线程中运行，它既不创建自己的线程，也不在单独的进程中运行（故：如果需要在Service中做耗时任务，需要新开启线程执行，避免ANR）
2. onCreate() 只在创建的时候调用一次，一旦服务启动后，就不会再调用了
3. onStartCommand() 必须返回整形数，表示服务停止时系统如何处理调，它有三个取值
 1）START_NOT_STICKY: 服务终止时不会重建，比较安全
 2）START_STICKY: 服务终止时会重建并调用 onStartCommand()，但传递的intent为空，适用于不需要传参数的服务
 3）START_REDELIVER_INTENT: 和START_STICKY类似，但会将之前的intent传递给重建的服务，适用于必须立即恢复的紧急任务
4. Android 5.0后，系统强制要求必须使用显式 Intent 来启动 Service
https://blog.csdn.net/pvpheroszw/article/details/77981553
5. 使用bindService方法不会调用onStartCommand()
6. 当手机屏幕发生旋转时，Activity会重新创建，之前通过bindService建立的连接便会断开（因之前的Context不存在了），服务也会被自动停止。
7. 如果bindService返回为false 解决方法：权限--后台管理——将智能后台改为允许后台管理

## 参考
http://blog.csdn.net/u011240877/article/details/72654743#android-50-%E5%90%8E%E9%9C%80%E8%A6%81%E6%98%BE%E5%BC%8F%E5%90%AF%E5%8A%A8-service
https://www.jianshu.com/p/1e49e93c3ec8

## intent的匹配规则
http://blog.csdn.net/u011240877/article/details/71305797
