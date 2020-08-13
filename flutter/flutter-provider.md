## InheritedWidget
InheritedWidget提供了数据在widget树中从上到下传递、共享的方式。


## Provider原理图
![截屏2020-07-30下午3.40.24](/assets/截屏2020-07-30下午3.40.24.png)

### 说明：
Model变化后会自动通知ChangeNotifierProvider（订阅者），ChangeNotifierProvider内部会重新构建InheritedWidget，而依赖该InheritedWidget的子孙Widget就会更新。
### Provider的好处：
1. 我们的业务代码更关注数据了，只要更新Model，则UI会自动更新，而不用在状态改变后再去手动调用setState()来显式更新页面。
2. 数据改变的消息传递被屏蔽了，我们无需手动去处理状态改变事件的发布和订阅了，这一切都被封装在Provider中了。这真的很棒，帮我们省掉了大量的工作！
3. 在大型复杂应用中，尤其是需要全局共享的状态非常多时，使用Provider将会大大简化我们的代码逻辑，降低出错的概率，提高开发效率。


## 参考文档
https://book.flutterchina.club/chapter7/provider.html
