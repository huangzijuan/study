## XCode证书配置
// 证书和签名必须对应起来
1. 证书创建
![certificate_create](/assets/certificate_create.jpg)
2. 签名文件创建
![profiles_create](/assets/profiles_create.jpg)

3. XCode关联
XCode里面证书和provisioning一定要匹配，否则会出现“Provisoning profile XXX doesn't include signing certificate XXX”问题
![xcode_sign_general](/assets/xcode_sign_general.jpg)

![xcode_sign](/assets/xcode_sign.jpg)

## fastlane自动管理证书
// fastlane初始化
fastlane init
命令：fastlane match init
fastlane match appstore
fastlane match adhoc
fastlane match development

// 参考文档
https://chenjunzhi.com/2018/09/10/ios-continuous-build-2/
