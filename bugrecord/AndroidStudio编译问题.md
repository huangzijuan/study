1. IDE提示：Connection timed out: connect. If you are behind an HTTP proxy, please configure the proxy settings either in IDE or Gradle.
解决方式：
在build.gradle文件里面，分别在buildscript中的repositories和allprojects中的repositories添加如下代码
````
maven() {
        url 'https://maven.aliyun.com/repository/jcenter'
    }
    maven(){
        url 'https://maven.aliyun.com/repository/google'
    }
    maven {
        url 'https://maven.aliyun.com/repository/public'
    }
    maven {
        url 'https://maven.aliyun.com/repository/mapr-public'
    }


````
这串代码的意思是国内镜像可以让速度变快
