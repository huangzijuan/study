## flutter编译
![WechatIMG13](/assets/WechatIMG13.png)

flutter下的iOS/Android工程本质上依然是一个标准的iOS/Android的工程，flutter只是通过在BuildPhase中添加shell来生成和嵌入App.framework和Flutter.framework(iOS),通过gradle来添加flutter.jar和vm/isolate_snapshot_data/instr(Android)来将Flutter相关代码编译和嵌入原生App而已。

不同于AOT模式下的App.framework是Dart代码对应的本地机器代码，JIT模式下，App.framework只有几个简单的API，其Dart代码存在于snapshot_blob.bin文件里。这部分的snapshot是脚本快照，里面是简单的标记化的源代码。所有的注释，空白字符都被移除，常量也被规范化，也没有机器码，tree shaking或者是混淆。

Debug模式：对应dart的JIT(just in time)模式
Release模式：对应dart的AOT(ahead of time)模式
Profile模式：类似Release模式，只是多了对于Profile模式的服务扩展的支持，支持跟踪，以及最小化使用跟踪信息需要的依赖

## flutter运行
![WechatIMG14](/assets/WechatIMG14.png)

## 参考
https://juejin.im/post/5b6d59476fb9a04fe91aa778

https://segmentfault.com/a/1190000015452970
