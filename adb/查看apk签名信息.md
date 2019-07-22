## 查看apk包的签名信息
1. 解压apk包找到签名文件（\META-INF\CERT.RSA）
2. 执行以下命令
keytool -printcert -file D:\Users\……\META-INF\CERT.RSA
