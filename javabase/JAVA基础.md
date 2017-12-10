## 一、 JAVA中提供的8种原始数据类型
1. int 长度数据类型：byte(8 bit)  short(16 bit)  int(32 bit)  long(64 bit)
2. float 长度数据类型：float(32 bit)  double(64 bit)
3. boolean 长度数据类型：boolean
4. char 数据类型：char(16 bit)

## 二、synchronized 相关知识点
1. synchronized(this) 以及 非static的synchronized方法，只能防止多个线程同时执行同一个对象的同步代码块

注：a. 用synchronized关键字的时候，应尽量减小锁的粒度，使代码更大程度的并发（能在代码段上加同步就不要在整个方法上加同步）
b. synchronized(XX.class)实现了全局锁的效果
  static synchronized方法也相当于锁住了代码段
