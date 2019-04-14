## Bitmap内存占用
Bitmap内存占用 ≈ 像素数据总大小 = 横向像素数量 × 纵向像素数量 × 每个像素的字节大小
单个像素的字节大小由Bitmap的一个可配置的参数Config来决定
![bitmap_config](/assets/bitmap_config.png)
细化：Bitmap内存占用 ≈ 像素数据总大小 = 图片宽 × 图片高× (设备分辨率/资源目录分辨率)^2 × 每个像素的字节大小

## Bitmap优化
从Bitmap占用内存的计算公式来看，减少内存主要可以通过以下几种方式：
1. 使用低色彩的解析模式，如RGB565，减少单个像素的字节大小
2. 资源文件合理放置，高分辨率图片可以放到高分辨率目录下
3. 图片缩小，减少尺寸

Bitmap内存占用的优化还有一个方式是复用和缓存

## 不同Android版本时的Bitmap内存模型
![bitmap_store](/assets/bitmap_store.png)

可以看到，最新的Android O之后，谷歌又把像素存放的位置，从java 堆改回到了 native堆。API 11的那次改动，是源于native的内存释放不及时，会导致OOM，因此才将像素数据保存到Java堆，从而保证Bitmap对象释放时，能够同时把像素数据内存也释放掉。8.0由于GC算法的优化，使得Bitmap占用的大内存区域，在GC后也能够比较快速的回收、压缩，重新使用。

## 参数
Options的基本属性：
1. inJustDecodeBounds：是否只加载图片的轮廓
2. inSampleSize：加载图片时加载原来的1/inSampleSize倍

1、当inJustDecodeBounds为true的时候，Android系统并不会去加载图片的具体数据，只会提取图片的轮廓信息。在这里我们就可以防止加载大图片进来的时候把内存给挤爆。
2、上面获取了宽高有怎样？？？？这样我们就可以根据比例去挑中inSampleSize的值，inSampleSize可以告诉系统加载Bitmap的时候按照怎样的比例去加载（按照1/inSampleSize去加载），这样在加载进来系统之前就已经处理好了，就不会挤爆内存了。


## 參考
https://juejin.im/entry/5ad0213f6fb9a028df2306cd
