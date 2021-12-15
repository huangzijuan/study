## Android/Flutter编程范式
声明式编程关注于发生了啥，而命令式则同时关注于咋发生的。（在命令式场景下，机器是不“智能”的，只是很机械的完成你交代的事情；而申明式是你告诉计算机你想要什么，由计算机自己去设计执行路径（最常见的申明式语言是SQL））
Android:命令式  （每个view都得听developer的指挥）
Flutter:申明式  （developer维护一整套数据集，设定好布军计划WidgetTree，为Widget绑定数据集中的某个数据，根据数据渲染）

## 概念
Flutter UI有三大元素：Widget、Element、RenderObject。对应这三者也有三个owner负责管理他们，分别是WidgetOwner(将军&Developer)、BuildOwner、PipelineOwner。

Widget，Widget 并不是真正的士兵，它只是将军手中的棋子，是一些廉价的纯对象，持有一些渲染需要的配置信息，棋子在不断被替换着。

RenderObject，RenderObject 是真正和我们作战的士兵，在概念上和我们Android的View一样，渲染引擎会根据RenderObject来进行真正的绘制，它是相对稳定且昂贵的。

Element，使得不断变化Widget转变为相对稳定的RenderObject的功臣是Element


## Widget、Element、RenderObject 的第一次创建与关联
1. 最底层rootWidget是RenderObjectToWidgetAdapter
