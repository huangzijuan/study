## 获取屏幕大小
```
MediaQuery.of(context).size
```
## 获取状态栏高度
```
MediaQueryData.fromWindow(WidgetsBinding.instance.window).padding.top
```

## 设置字体不允许缩放
```
MediaQuery(
      data: MediaQueryData.fromWindow(WidgetsBinding.instance.window).copyWith(textScaleFactor: 1),
      child: new Container(),
    );
```

## Padding设为负数
```
Transform(
      transform: Matrix4.translationValues(10, -10, 0),
      child: new Container(),
    );
```

## 参考
https://zhuanlan.zhihu.com/p/60849813
