## Android四大组件
1. Activity 通过intent使用Bundle传递extra
在Bundle中附加需要传输给远程进程的信息数据（数据必须是能够被序列化的），并通过Intent发送出去
2. BroadCastReceiver
3. Service
4. ContentProvider

## 共享文件，通过对文件进行读写，传递数据
Android系统基于Linux，其并发读写文件可以没有限制地进行，两个线程可以同时对同一线程进行读写
适用于：对数据同步不高的进程之间通信

## AIDL、Messanger

## Socket
