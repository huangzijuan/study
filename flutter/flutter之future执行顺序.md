## future执行顺序
![1612343635(1)](/assets/1612343635(1).png)

Dart事件循环执行如上图所示

先查看MicroTask队列是否为空，不是则先执行MicroTask队列
一个MicroTask执行完后，检查有没有下一个MicroTask，直到MicroTask队列为空，才去执行Event队列
在Evnet 队列取出一个事件处理完后，再次返回第一步，去检查MicroTask队列是否为空
注意：我们可以看出，将任务加入到MicroTask中可以被尽快执行，但也需要注意，当事件循环在处理MicroTask队列时，Event队列会被卡住，应用程序无法处理鼠标单击、I/O消息等等事件。

## 延时任务
延时任务需要等待X秒之后才会将任务加入Event任务队列。
【若在X秒之间有耗时任务加入到了Event队列，会导致写在前面的delayed任务在X秒之后才能被加入到耗时任务之后，只有当前面耗时任务完成后，它才有机会得到执行。（这种机制会使延迟任务无法确定在延迟多久后能被执行）】

## async和await
将 async 关键字作为方法声明的后缀时，具有如下意义:
1. 被修饰的方法会将一个 Future 对象作为返回值
2. 该方法会同步执行其中的方法的代码直到第一个 await 关键字，然后它暂停该方法其他部分的执行；
3. 一旦由 await 关键字引用的 Future 任务执行完成，await的下一行代码将立即执行。

## 示例

![f9742e9534ef6539506d0fcca380e32](/assets/f9742e9534ef6539506d0fcca380e32.png)

![edc4873255bdeee19fd1d14c6254644](/assets/edc4873255bdeee19fd1d14c6254644.png)

## 总结
1. Future中的then并没有创建新的Event丢到Event Queue中，而只是一个普通的Function Call，在FutureTask执行完后，立即开始执行
2. 当Future在then函数先已经执行完成了，则会创建一个task，将该task的添加到microtask queue中，并且该任务将会执行通过then传入的函数
3. Future只是创建了一个Event，将Event插入到了Event Queue的队尾
4. 使用Future.value构造函数的时候，就会和第二条一样，创建Task丢到microtask Queue中执行then传入的函数
5. Future.sync构造函数执行了它传入的函数之后，也会立即创建Task丢到microtask Queue中执行

## Dart中的Isolate
两对Isolate是通过两对Port对象通信，一对Port分别由用于接收消息的ReceivePort对象，和用于发送消息的SendPort对象构成。其中SendPort对象不用单独创建，它已经包含在ReceivePort对象之中。
（一对Port对象只能单向发消息，这就如同一根自来水管，ReceivePort和SendPort分别位于水管的两头，水流只能从SendPort这头流向ReceivePort这头。因此，两个Isolate之间的消息通信肯定是需要两根这样的水管的，这就需要两对Port对象。）

无论是spawn还是spawnUri，运行后都会创建两个进程，一个是主Isolate的进程，一个是新Isolate的进程，两个进程都双向绑定了消息通信的通道，即使新的Isolate中的任务完成了，它的进程也不会立刻退出，因此，当使用完自己创建的Isolate后，最好调用newIsolate.kill(priority: Isolate.immediate);将Isolate立即杀死。

## Flutter中的Isolate

## 使用场景
一个最简单的判断方法是根据某些任务的平均时间来选择：

　　方法执行在几毫秒或十几毫秒左右的，应使用Future，如果一个任务需要几百毫秒或之上的，则建议创建单独的Isolate
除此之外，还有一些可以参考的场景

JSON 解码
加密
图像处理：比如剪裁
网络请求：加载资源、图片
