## 查看apk包的签名信息
1. 解压apk包找到签名文件（\META-INF\CERT.RSA）
2. 执行以下命令
keytool -printcert -file D:\Users\……\META-INF\CERT.RSA

## 生成签名证书
https://www.jianshu.com/p/c419e54e7492

## 查看安装包版本号等信息
https://www.jianshu.com/p/ee04f2dcb8cf
adb shell
dumpsys package com.aaa.bbb
