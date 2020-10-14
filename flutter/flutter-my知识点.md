0. Android/flutter的一些区别
  编程范式不同：Android视图开发是命令式的；flutter视图开发是申明式的。

1. Widget和element和RenderObject之间的关系
  每个Widget都有三个关键方法：保证唯一的key、创建element的createElement、canUpdate
  对RenderObjectWidget还有一个方法：createRenderObject
  但并非每个Widget都有与之对应的RenderObjectWidget
  每个Widget都有一个对应的Element，但Element不一定会有对应的RenderObject
  Android的ViewTree为：PhoneWindow ——> DecorView ——> (TitleView、ContentView)
  flutter的ViewTree为：RenderObjectToWidgetAdapter ——> (MyApp、MyMeterialApp)

  ![35a9047a4b3cb83a957c65b9671fbf5](/assets/35a9047a4b3cb83a957c65b9671fbf5.png)

  首先要了解flutter中的三棵树：Widget树、Element树、RenderObject树

2. Future和microtask执行顺序
