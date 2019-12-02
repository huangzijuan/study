## 是什么？
一款高性能的开源RPC框架

## 特点
1. 简单的服务定义：使用Protocol Buffers（做序列化的工具）来定义服务
2. 跨语言跨平台
3. 简单、可扩展
4. 双向数据流

## gRPC中定义了四种类型的服务方法
1. 一元 RPC（Unary RPCs），客户端发送简单请求，得到简单响应，类似于一个函数调用：
```
rpc SayHello(HelloRequest) returns (HelloResponse){
}
```

2. 服务端流式 RPC（Server streaming RPCs），客户端发送请求，得到一个流 Stream，然后从 Stream 读取内容：
```
rpc LotsOfReplies(HelloRequest) returns (stream HelloResponse){
}
```

3. 客户端流式 RPC（Client streaming RPCs），客户端通过流 Stream 来写入内容，然后发送给服务端，最后得到响应：
```
rpc LotsOfGreetings(stream HelloRequest) returns (HelloResponse) {
}
```

4. 双向流式 RPC（Bidirectional streaming RPCs），上面两种方式的结合体：
```
rpc BidiHello(stream HelloRequest) returns (stream HelloResponse){
}
```
