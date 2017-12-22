##  一、Loader
主要完成单线程耗时数据异步装载功能，并在数据有更新自动通知UI刷新的作用。loader自带数据结果监听机制，可以方便优雅的进行UI更新。

Loader以及LoaderManager是Android Framework中异步加载各种数据（不限于Cursor）的标准机制

Loader的生命周期是 started <-> stopped -> abandoned -> reseted

#### 作用和优点
1. 提供异步加载数据功能
2. 对数据源变化进行监听，实时更新数据
3. 在Activity配置发生变化（如横竖屏切换）时可避免数据的重复加载
4. 适用于任何Activity和Fragment


## 二、相关的类
#### LoaderManager
一个Activity/Fragment只有一个单例的LoaderManager对象，LoaderManager可以管理一个或多个Loader，能够维护Loader的生命周期。

常用的两个方法有：initLoader(loaderId, bundle, LoaderCallbacks)方法、restartLoader()方法

#### LoaderManager.LoaderCallbacks
LoaderCallbacks有三个回调方法需要实现：onCreateLoader()、onLoadFinished()以及onLoaderReset()
1. onCreateLoader:返回一个Loader的实例。
2. onLoadFinished:当onCreateLoader中创建的Loader完成数据加载的时候，会在onLoadFinished回调函数中得到加载的数据。
3. onLoaderReset:当之前创建的Loader（该Loader向客户端发送过数据）被销毁的时候，就会触发onLoaderReset回调，表明之前获取的数据已被重置处于无效状态了，客户端应该释放对该无效数据的引用。

#### Loader
具体的数据加载器，Loader类本身并不支持异步加载机制。
Loader有许多public的方法，比如startLoading()、stopLoading()等，但是客户端不应该直接调用这些方法，这些方法由LoaderManager调用的，如果客户端调用了这些public的方法，就很有可能导致Loader生命周期出现混乱，进而影响到LoaderManager对Loader的管理。

#### AnyncTaskLoader
AnyncTaskLoader继承自Loader。AnyncTaskLoader具有异步加载的机制

#### CursorLoader
CursorLoader继承自AnyncTaskLoader。其实现了AsyncTaskLoader的loadInBackground()方法，在该方法中会执行ContentResolver的query()方法，从而实现对ContentProvider的数据查询，其得到的数据是Cursor对象。

## 参考：
http://blog.csdn.net/iispring/article/details/48834767
http://blog.csdn.net/iispring/article/details/48958117
