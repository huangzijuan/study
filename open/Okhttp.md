## 主要类作用
1. OkHttpClient对象：为网络请求执行的一个中心，它会管理连接池，缓存，SocketFactory，代理，各种超时时间，DNS，请求执行结果的分发。
2. Request对象：用于描述一个HTTP请求，比如：请求的方法是GET还是POST，请求的URL，请求的header，请求的body，请求的缓存策略等。

## 几个Interceptor的职责
1. RetryAndFollowUpInterceptor（重试、重定向拦截器） --->创建StreamAllocation对象，处理http的redirect，出错重试。对后续Interceptor的执行的影响：修改request及StreamAllocation。
2. BridgeInterceptor（桥拦截器）-------------->补全缺失的一些http header。对后续Interceptor的执行的影响：修改request。
3. CacheInterceptor（缓存拦截器）-------------->处理http缓存。对后续Interceptor的执行的影响：若缓存中有所需请求的响应，则后续Interceptor不再执行。
4. ConnectInterceptor（连接拦截器）------------>借助于前面分配的StreamAllocation对象建立与服务器之间的连接，并选定交互所用的协议是HTTP 1.1还是HTTP 2。对后续Interceptor的执行的影响：创建了httpStream和connection。
5. CallServerInterceptor（向服务器发起网络请求）----------->处理IO，与服务器进行数据交换。对后续Interceptor的执行的影响：为Interceptor链中的最后一个Interceptor，没有后续Interceptor。
![okhttp](/assets/okhttp.png)

## 主流程分析
1. 请求发送到哪里？
请求发送到框架中的两个队列中：运行时队列、等待中队列
如果运行中队列总数小于64，并且访问同一目标及其请求小于5，就放在运行时队列中；否则放入等待队列中
2. 请求被谁处理？
请求提交到运行中队列后，交给线程池直接处理请求
3. 请求是怎么被维护的？
每次请求被处理完之后，都会对运行中队列和等待中队列进行数据处理（在符合条件的情况下，将等待中队列放入运行中队列中去）

## 建造者模式
又称构建者模式，允许使用多个简单的对象一步一步构建成一个复杂的对象
优点：不需要关注细节，因为提供了默认值，
