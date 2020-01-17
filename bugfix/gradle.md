1. 问题： Note: the configuration keeps the entry point 'XXX', but not the descriptor class 'XXX'
解决：在 proguard-rules.pro 文件中添加 -ignorewarnings

2. 问题：安装提示Failure [INSTALL_FAILED_OLDER_SDK]
解决：修改build.gradble中的minSdkVersion 版本号，降低对于Android最低版本的限制
```
defaultConfig {
    applicationId "com.example.mooreliu.androidl"
    minSdkVersion 13
    targetSdkVersion 22
    versionCode 1
    versionName "1.0"
}
```
