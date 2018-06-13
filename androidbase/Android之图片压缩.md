## 图片存在的三种形式
1. 硬盘上时是file
2. 网络传输时是stream
3. 内存中是stream 或 bitmap

## 检测图片三种形式大小的方法:
文件形式: file.length()
流的形式: 讲图片文件读到内存输入流中,看它的byte数
Bitmap:    bitmap.getByteCount()

## bitmap所占内存大小计算方式：
图片长度 x 图片宽度 x 一个像素点占用的字节数

## tips
对于质量压缩，并不会改变图片的像素，所以就算质量被压缩了，但是bitmap在内存的占有率还是没变小

## 参考
https://blog.csdn.net/HarryWeasley/article/details/51955467
