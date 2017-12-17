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

## 三、引用传递和值传递
1. 基本类型（byte,short,int,long,double,float,char,boolean）为传值
2. 对象类型（Object,数组，容器）为传引用
3. String、Integer、Double等immutable类型因为类的变量设为final属性，无法被修改，只能重新赋值或生成对象。
当Integer作为方法参数传递时，对其赋值会导致原有的引用被指向了方法内的栈地址，失去原有的的地址指向，所以对赋值后的Integer做任何操作都不会影响原有值。

## 四、JAVA线程run与start方式的区别
