## PMS(PackageManagerService)
主要用来管理安装包、提前加载Activity的。安装apk 管理apk

是被SystemServer启动，运行在SystemServer进程中

## 为什么需要PMS
如果没有PMS
1. 每次打开一个APP 遍历/data/app 定位到要跳转的app
2. IO操作获取到AndroidManifest.xml
3. dom解析 Activity
4. 加载入口Activity
