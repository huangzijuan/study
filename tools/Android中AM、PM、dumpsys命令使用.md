## am命令
![am_command](/assets/am_command.png)

原理分析：am命令实的实现方式在Am.java，最终几乎都是调用ActivityManagerService相应的方法来完成的，am monitor除外。比如前面概述中介绍的命令am start -a android.intent.action.VIEW -d https://amberweather.com， 启动Acitivty最终调用的是ActivityManagerService类的startActivityAsUser()方法来完成的。再比如am kill-all命令，最终的实现工作是由ActivityManagerService的killBackgroundProcesses()方法完成的

## pm命令
![pm_command](/assets/pm_command.png)

原理分析：pm命令实的实现方式在Pm.java，最后大多数都是调用PackageManagerService相应的方法来完成的。disbale之后，在桌面和应用程序列表里边都看到不该app。

## dumpsys
通过命令查看当前手机所支持的dump服务：先进入adb shell，再执行如下命令：dumpsys -l


## 参考
https://www.jianshu.com/p/2802683923e0
adb常用命令：https://juejin.im/post/5b5683bcf265da0f9b4dea96
