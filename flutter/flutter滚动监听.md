## ScrollController

## NotificationListener

## 两者的区别
1. ScrollController可以控制滚动控件的滚动，NotificationListener不可以
2. 通过NotificationListener可以在从可滚动组件到widget树根之间任意位置都能监听，而ScrollController只能和具体的可滚动组件关联后才可以
3. 收到滚动事件后获得的信息不同：NotificationListener在收到滚动事件时，通知中会携带当前滚动位置和ViewPort的一些信息，而ScrollController只能获取当前滚动位置

## 参考
https://juejin.im/post/5d8f0ad6e51d45780f0604c8
