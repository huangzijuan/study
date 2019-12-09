![dart_event](/assets/dart_event.png)

## dart中代码执行优先级分三个级别
1. 在 Main 中的代码将最先执行
2. 执行完 Main 中的代码，然后会检查并执行 Microtask Queue 中的任务， 通常使用 scheduleMicrotask 将事件添加到 MicroTask Queue 中
3. 最后执行 EventQueue 队列中的代码，通常使用 Future 向 EventQueue加入事件，也可以使用 async 和 await 向 EventQueue 加入事件。

## 多个Future的执行顺序
1. Future 的执行顺序为Future的在 EventQueue 的排列顺序。类似于 JAVA 中的队列，先来先执行
2. 当任务需要延迟执行时，可以使用 new Future.delay() 来将任务延迟执行。
3. Future 如果执行完才添加 then ，该任务会被放入 microTask，当前 Future 执行完会执行 microTask，microTask 为空后才会执行下一个Future。
4. Future 是链式调用，意味着Future 的 then 未执行完，下一个then 不会执行。

## 注意点
1. Future中的 then 并没有创建新的Event丢到Event Queue中，而只是一个普通的Function，在一个 Future 所有的 Function 执行完后，下一个 Future 才会开始执行
