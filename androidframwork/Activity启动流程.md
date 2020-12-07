## 整体流程
![ead6e912a2664b26a40e6d1cfd4e264](/assets/ead6e912a2664b26a40e6d1cfd4e264.jpg)

![1606824520(1)](/assets/1606824520(1).png)

![1606825019(1)](/assets/1606825019(1).png)

1. startActivity内部会通过Instrumentation的execStartActivity方法来启动Activity，会远程调用到AMS中的startActivity中。
2. AMS将新启动的Activity以ActivityRecord的形式压入Activity栈中，使原进程的Activity处于paused状态，然后开始新Activity的启动工作
3. AMS会通过Zygote会fork一个新的进程，新进程启动后会调用ActivityThread的main函数（这个函数是应用程序的入口，在这里会开启主线程的消息循环队列，并通过attach函数将ApplicationThread与AMS进行关联）。
4. AMS完成启动Activity前的一些工作后，会通过ApplicationThread回调scheduleLaunchActivity到APP进程，因ApplicationThread回调逻辑是在binder线程池中完成的，需要通过Handler H将其切换到UI线程，然后会发送LAUNCH_ACTIVITY消息，会对应执行handleLaunchActivity方法，在这个方法中完成Activity的启动和创建，然后会通过Instrumentation回调Activity的生命周期方法

## 关键类作用
ActivityManagerService,简称AMS,系统服务，主要用于管理调度进程，Activity栈以及Activity启动销毁等操作
ActivityThread，简称AT，app运行环境的一部分，也被称为主进程，UI的绘制之类的都是在基于这个调度
Instrumentation，app运行组件监控类，主要用于管理Activity的启动，销毁以及监控activity运行
ApplicationThread, AMS服务与app进行进行通讯的类
ActivityRecord, 简称AR，主要用于在AMS中存储各个进程中Activity状态的信息类
ProcessRecord,简称PR，主要用于在AMS中存储各个进程的状态信息类


## ActivityStackSupervisor
是一个Activity栈的管理类，有许多不同类型的list来存放ActivityRecord，ActivityStackSupervisor只是用来管理Activity与任务栈的，它并不具备执行具体操作的能力。
ActivityRecord封装与Activity有关的一系列参数，（例如：我是谁、我从哪里来、我要到哪里去）


## 参考
https://blog.csdn.net/pgg_cold/article/details/79491791?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control

https://blog.csdn.net/q1183345443/article/details/79420901?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control

https://www.cnblogs.com/bastard/archive/2012/04/07/2436262.html
