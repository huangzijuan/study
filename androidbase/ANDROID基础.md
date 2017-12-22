## 一、RecycleView与ListView相比的优势是什么？

## 二、常用的MaterialDesign组件用到了哪些？

## 三、AsyncTaskLoader与AsyncTask的区别
1. AsyncTaskLoader 主要用来开启异步任务加载数据库数据或者URI数据
   优势：会自动刷新数据变化；会自动处理Activity配置变化造成的影响；适合处理纯数据加载
   劣势：
2. AsyncTask 主要用来请求网络或者耗时操作（IO流操作、复杂数据解析）
   优势：可以与UI实时交互及replace操作
   劣势：不会自动处理Activity配置变化造成的影响

参考：http://blog.csdn.net/chenshengfa/article/details/50485162

## 四、Activity与Fragment传递数据的方式
1. 将要传的值放在Bundle对象里；

## 五、Http Client与HttpURLConnection的区别
