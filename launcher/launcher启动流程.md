# 几个重要的类：
1. ActivityManagerService：主要负责系统中四大组件的启动、切换、调度及应用进程的管理和调度等工作。
2. Instrumentation：监控应用程序和系统的交互
3. ActivityThread：应用的入口类，系统通过调用main函数，开启消息循环队列。ActivityThread所在线程被称为应用的主线程（UI线程）
4. ApplicationThread：ApplicationThread提供Binder通讯接口，AMS则通过代理调用此App进程的本地方法。
5. ActivityManagerProxy：AMS服务在当前进程的代理类，负责与AMS通信。
6. ApplicationThreadProxy：ApplicationThread在AMS服务中的代理类，负责与ApplicationThread通信。

# 流程概述图
![屏幕快照 2019-09-18 下午3.30.41](/assets/屏幕快照%202019-09-18%20下午3.30.41.png)

# 
