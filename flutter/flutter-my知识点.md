##0. Android/flutter的一些区别
  编程范式不同：Android视图开发是命令式的；flutter视图开发是申明式的。

##1. Widget和element和RenderObject之间的关系
  每一个Widget都有一个对应的Element，但Element不一定会有对应的RenderObject。
  每个Widget都有三个关键方法：保证唯一的key、创建element的createElement、canUpdate
  对RenderObjectWidget还有一个方法：createRenderObject
  但并非每个Widget都有与之对应的RenderObjectWidget

  Android的ViewTree为：PhoneWindow ——> DecorView ——> (TitleView、ContentView)
  flutter的ViewTree为：RenderObjectToWidgetAdapter ——> (MyApp、MyMeterialApp)

  ![1602750317(1)](/assets/1602750317(1).png)
  ![1602750335(1)](/assets/1602750335(1).png)
  ![1602750362(1)](/assets/1602750362(1).png)

  StatefulElement中有对Widget的引用，也有对StatefulWidget的State的引用，在构造函数里将widget赋值给_state里面的_widget。
  RenderObjectElement中持有对Widget和RenderObject的引用
  Element中有一个关键mount方法：ComponentElement的mount方法主要作用是执行build，而RenderObjectElement的mount方法主要作用是生产RenderObject。

  总结：首先要了解flutter中的三棵树：Widget树（配置信息的树，是Element的配置）、Element树（作为中间层，管理着将Widget生成RenderObject和一些更新的操作）、RenderObject树（渲染树，负责计算、布局和绘制）。写好Widget树后，flutter会在遍历widget树时调用Widget里面的createElement方法生成对应节点的Element对象，Element创建好后flutter会执行mount方法，对应非渲染的ComponentElement来说mount主要执行widget里的build方法，而对于渲染的RenderObjectElement来说mount里会调用widget里的createRenderObject方法生成RenderObject。当widget树发生变化时，持有该widget的Element节点会被标记为dirty，在下一个绘制周期，flutter会出发Element树的更新，会通过canUpdate方法来判断是否可以使用新的widget来更新Element里的配置，还是重新生成Element，并使用最新的Widget数据更新自身及关联的RenderObject对象。布局和绘制完成后，合成和渲染会交给skia引擎来做

2. Root的创建过程

  ![35a9047a4b3cb83a957c65b9671fbf5](/assets/35a9047a4b3cb83a957c65b9671fbf5.png)

  a. attachRootWidget(app)方法创建Root[Widget]（也就是RenderObjectToWidgetAdapter）
  b. 调用attachToRenderTree方法创建Root[Element]
  c. Root[Element]尝试调用mount方法将自己挂载到父Element上，因为自己就是root了，所以没有父Element，挂空了
  d. mount的过程中会调用Widget的createRenderObject,创建了 Root[RenderObject]
  至此，root创建完成，app作为RenderObjectToWidgetAdapter的子Widget依次往父控件挂载。
  e. 调用owner.buildScope，执行子Tree的创建和挂载
  f. 调用createElement方法创建出Child[Element]
  g. 调用Element的mount方法,将自己挂载到Root[Element]上，形成一棵树
  h. 挂载的同时，如果是需要渲染的widget则调用widget.createRenderObject,创建Child[RenderObject]
  i. 创建完成后，调用attachRenderObject,完成和Root[RenderObject]的链接

##3. flutter的刷新流程
  a. 调用setState时，Element将自身标记为dirty，并调用owner.scheduleBuildFor(this)，通知buildOwner进行处理
  b. buildOwner将element添加到集合_dirtyElements中，等待下一帧绘制时集中处理，并通知ui.window安排新的一帧
  c. 底层引擎最终回到dart层，执行buildOwner的buildScope方法：（_dirtyElement.sort ——> _dirtyElement[i].rebuild ——> _dirtyElement.clear）
  d. 执行performRebuild()
     ComponentElement的performRebuild()：执行element的build() ——> updateChild
     RenderObjectElement的performRebuild()：调用了widget.updateRenderObject方法更新RenderObject

##4. Future和microtask执行顺序


## 参考
https://www.jianshu.com/p/71bb118517b1
https://lizhaoxuan.github.io/2019/01/02/%E5%B8%9D%E5%9B%BD%E7%9A%84%E7%BA%B7%E4%BA%89-FlutterUI%E7%BB%98%E5%88%B6%E8%A7%A3%E6%9E%90/
