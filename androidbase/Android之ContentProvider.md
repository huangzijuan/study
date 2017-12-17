## 实现进程间共享内存的原理
它是通过Binder进程间通信机制以及匿名共享内存机制来实现的

## ContentObserver
#### 使用ContentObserver的情况主要有一下两者情况：
1、需要频繁检测的数据库或者某个数据是否发生改变，如果使用线程去操作，很不经济而且很耗时 ；
2、在用户不知晓的情况下对数据库做一些事件，比如：悄悄发送信息、拒绝接受短信黑名单等；

## 参考
http://blog.csdn.net/luoshengyang/article/details/6985171
