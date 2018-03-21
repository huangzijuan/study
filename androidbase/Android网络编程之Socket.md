## Socket：
是一个调用接口（API），可对TCP/IP协议进行封装和应用。可视为TCP/IP的编程接口
通信的基石，是支持TCP／IP协议的网络通信的基本操作单元

套接字之间的连接分为三个步骤：服务器监听、客户端请求、连接确认

## 常用类
#### 位于服务端的ServerSocket
1. accept()方法
调用此方法时，会阻塞当前的侦听，等待客户端的连接。创建成功之后会返回一个Socket实例，与客户端进行通信
2. getInetAddress()
返回服务端的本地地址
3. getLocalPort()
返回此服务端侦听的端口号

#### 位于客户端的Socket
1. getInputStream()
获取当前套接字的输入流
2. getOutputStream()
获取当前套接字的输出流
