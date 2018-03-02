## 指定进程
1. android:process=":remote"
以‘:’开头的进程属于当前应用的私有进程，其它应用的组件不可以和它跑在同一个进程中
2. android:process="com.example.zijuan.remote"
不以‘:’开头的进程属于全局进程，其它应用通过ShareUID方式可以和它跑在同一进程中

## 其他
1. android:exported=“true|false”  组件是否可以被其它应用组件启动
'true'：该组件可以由其它应用的组件启动
'false'：该组件只能由同一应用的组件或者使用同一用户ID的不同应用启动
2. android:enabled=“true|false”  组件是否可以被实例化
‘true’：系统可以将组件实例化
‘false’：系统不可以将组件实例化
