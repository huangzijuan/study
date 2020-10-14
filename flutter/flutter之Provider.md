## Provider类别
1. Provider
  优点：（数据共享方面：）可以在以Provider为根节点的子树中获取到T的对象
  缺点：在共享数据发生改变时，不能通知它的监听者
2. ListenableProvider
  数据模型model如果没有定义成ChangeNotifier的子类，则需要自己进行监听者的管理。
3. ChangeNotifierProvider
 ChangeNotifierProvider继承自ListenableProvider；限制数据model必须是ChangeNotifier的子类；通过重写ChangeNotifier.dispose()来完成资源的释放，构造函数中不需要传入dispose。
  数据改变的触发者：对于只需要获取到数据model，不需要监听变化的，使用Provider.of<T>(context, listen: false)
  数据改变的监听者：使用Consumer
4. ValueListenableProvider
  builder返回的对象必须是ValueNotifier<T>的子类，T是需要共享的数据类型（ValueNotifier是ChangeNotifier的子类）
5. StreamProvider
6. FutureProvider
   与FutureBuilder的区别：
   FutureBuilder的数据请求和展示都是在一个组件中的，而FutureProvider是数据的请求者，Consumer是展示者
   FutureBuilder的请求者和展示者是一对一的关系，而FutureProvider可以是一对多的关系

## Provider官方示例
https://github.com/rrousselGit/provider

## 参考文档
https://juejin.im/post/6844903903432032263
