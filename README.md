文件

采用ActiveAndroid作为主要数据库

图片上传模块使用ContentProvider + AsyncTaskLoader的
方式，将照片回调更新到db里，然后监听db的变化，更新UI列表

上传任务采用Service + 线程池的方式


车辆详情的图片流采用ViewPager + Fragment的典型架构
项目引入RxJava，链式的编程风格使代码更易读
使用模版设计模式抽取基类代码
利用RecycleView将臃肿的代码模块化
