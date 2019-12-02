1. android异常 More than one file was found with OS independent path 'META-INF/XXX'
修改：在app.gradle文件里面android节点如下代码
packagingOptions {
     exclude 'META-INF/XXX'
 exclude 'META-INF/XXX'
 exclude 'META-INF/XXX'
 exclude 'META-INF/XXX'
 }
