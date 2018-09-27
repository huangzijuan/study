## 编译不同版本的apk

## productFlavor可以实现什么
 1.多包名 （applicationId "zuul.com.android.devel"）
 2.不同的变量配置 （buildConfigField 'String', 'HOST', '"http://api.devel.com"'）
 3.不同的res
 4.为不同flavors提供不同的图标
 5.不同的source code

## productFlavor如何配置
android {

  productFlavors {  
     ...
     ad {
         ...
     }
     preview {
         ...
     }
  }
}

## 组合多个productFlavor
flavorDimensions 表示维度的概念，Gradle 不会组合属于相同flavorDimensions的productFlavor。
flavorDimensions "api", "mode"
在 Gradle 为每个构建变体或对应 APK 命名时，属于较高优先级风味维度的产品风味首先显示，之后是较低优先级维度的产品风味，再之后是构建类型

src/fullDebug/（构建变体源集）
src/debug/（构建类型源集）
src/full/（产品风味源集）
src/main/（主源集）

构建变体 > 构建类型 > 产品风味 > 主源集 > 库依赖项

## 过滤变体



## 在library中使用productFlavors
publishNonDefault 这个变量的配置来使得依赖库在编译的时候默认生成所有变种的包，而不是仅仅生成 release 一种。
publishNonDefault true //注意，这里的配置是为了去除gradle对library module默认只编译release buildType的限制

## 参考
https://blog.csdn.net/yulyu/article/details/70257015

https://developer.android.com/studio/build/build-variants?



##——————————————————————————————————————————————————————————————————————————
gradle的工作流程分三个阶段：
Initialization ： 这个阶段，主要是会分析哪些module将被构建。这个时候又一个很明显的操作就是这个阶段会解析settings.gradle，并创建project对象。
Configuration ：这个阶段，主要是执行当前项目所有需要构建的module以及root project的build.gradle脚本；这个过程会形成每个项目的task依赖图。
Execution ：这个阶段，执行我们指定的task任务，以及其依赖的任务
