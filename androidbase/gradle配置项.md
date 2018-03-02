## zipAlignEnabled
对打包完成的apk文件进行优化
在Android中，每个应用程序中存储的数据文件都会被多个进程访问，当资源文件通过内存映射对齐到四字节边界时，访问资源文件的代码才是最有效率的。但如果资源本身没有进行对齐处理，就必须显式地读取它们（这个过程比较缓慢且会花费额外的内存）

## minifyEnabled
开启混淆、代码压缩
与proguardFiles配合使用，proguardFiles取值有：
1. getDefaultProguardFile('proguard-android.txt')
在Android SDK tools/proguard/ 文件夹下可以获取到默认的ProGuard设置。（若使用同一位置的 proguard-android-optimize.txt 文件，它包括相同的ProGuard规则，但还包括其它字节码一级执行分析的优化，进一步减小APK大小和帮助提高运行效率）
2. proguard-rules-debug.pro
用于添加自定义的ProGuard规则（一般需要解析的model类、第三方类库等，需要添加到自定义ProGuard规则里）

## shrinkResources
资源压缩
资源压缩与代码压缩协同工作。首先代码压缩器移除未使用的代码后，使库资源变为未引用资源，然后资源压缩器将其移除。
