
![fda927a912553cf9ea67fd377225022](/assets/fda927a912553cf9ea67fd377225022.png)
## 生命周期绑定：
  传入ApplicationContext，不会对生命周期进行管理
  传入Activity、FragmentActivity、Fragment、View，会创建一个不可见的Fragment，Fragment中持有一个lifecycle，当fragment生命周期变化时会回调lifecycle相关生命周期函数，从而实现生命周期绑定。

![f28c9140a0dfa79df480bb7f8f17014](/assets/f28c9140a0dfa79df480bb7f8f17014.png)

## 缓存机制：
  1. ActiveResources  WeakReference<EngineResource>弱引用缓存
         EngineResource用acquired变量来记录图片被引用的次数，其中acquire()会让变量加1，release()会让变量减1。当acquired为0时，说明图片已经不再被使用了，此时会回调onResourceRelease()方法，此方法会将该图片从activeResources中移除，并将其放入LruResourceCache中。（正在使用的图片用弱引用来缓存，不在使用中的图片使用LruCache来缓存）
  2. MemoryCache
      当LruResourceCache中图片被使用时，会从LruResourceCache中移除，并加入ActiveResources  中
  3. decodeResultFromCache      对应DiskCacheStrategy.RESULT
  4. decodeSourceFromCache      对应DiskCacheStrategy.SOURCE（是从网络、文件获得的原始数据）
####内存缓存（防止重复将图片数据读取到内存中）
      会先从内存缓存中找，（找到加载，并从内存缓存中移除加入activeResources中去）找不到再到activeResources中去找，找不到回到磁盘缓存中找（先找Result图，再找原图），找不到从网络下载
####磁盘缓存（防止重复将图片数据读取到磁盘中）
      DiskCacheStrategy.NONE 不缓存文件
      DiskCacheStrategy.SOURCE 只缓存原图
      DiskCacheStrategy.RESULT 只缓存最终加载的图（默认的缓存略）
      DiskCacheStrategy.ALL 同时缓存原图和结果图
![08066cb96d492896b0edb57e8fc695b](/assets/08066cb96d492896b0edb57e8fc695b.png)

![aabb8c5d16e5e65fd3822c4be0ce55a](/assets/aabb8c5d16e5e65fd3822c4be0ce55a.png)


## 复用机制
  如果缓存中不存在，就要从源地址来获取图片，在解析图片的时候会使用BitmapPool（复用池），来达到频繁申请内存而引起的性能（抖动、碎片）问题。
  每次解析一张图片为Bitmap(磁盘缓存、网络/文件)时会从BitmapPool中查找一个可被复用的Bitmap；当一个Bitmap从内存缓存中被动的被移除（内存紧张、达到maxSize）时并不会被recycle，而是加入BitmapPool，只有从BitmapPool中被动的被移除时，Bitmap内存才会真正被释放。
Glide的优点：
1. 可以监听Activity生命周期管理，更合理地管理图片加载和释放
2. 可以加载Gif图
3. 加载质量，Picasso默认采用的是ARGB-8888，Glide默认采用的是RGB-565，内存占用会减小一半
4. 缓存策略和加载速度。Picasso缓存的是全尺寸，而Glide缓存的图片和ImageView的尺寸相同。Glide的这个特点，让加载显得特别快，而Picasso则因为显示前需要重新调整大小而导致一些延迟
5. Glide可以通过自定义GlideModule来完成特殊加载需求（如加载加密图片）



图片加载框架一般包含以下步骤：
封装参数、解析路径、下载、解码、变换、缓存、显示
