## ProGuard如何工作的
ProGuard使用字典来定义要重命名包，类或方法的内容。有一个默认字典只包含字母a-z。

## 常用到的不混淆
1. JNI方法不混淆
2. 反射不混淆
3. AndroidMainfest中的类不混淆
AndroidMainfest中的类不混淆，所以四大组件和Application的子类和Framework层下所有的类默认不会进行混淆。
4. JSON对象类不混淆
5. 第三方开源或SDK包
6. WebView的JS调用的接口方法不混淆
7. Parcelable的子类和Creator静态成员变量不混淆
8. enum类型
9. 注解不混淆
10. 泛型不混淆
11. 内部类不混淆


## 参考
https://www.cnblogs.com/zhangmiao14/p/7098168.html

https://blog.csdn.net/lihenair/article/details/79879144
