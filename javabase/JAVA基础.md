## 一、 JAVA中提供的8种原始数据类型
1. int 长度数据类型：byte(8 bit)  short(16 bit)  int(32 bit)  long(64 bit)
2. float 长度数据类型：float(32 bit)  double(64 bit)
3. boolean 长度数据类型：boolean
4. char 数据类型：char(16 bit)

## 二、synchronized 相关知识点
synchronized既可以锁类又可以锁对象，故synchronized分为类锁和对象锁
1. synchronized(this) 以及 非static的synchronized方法，只能防止多个线程同时执行同一个对象的同步代码块

注：a. 用synchronized关键字的时候，应尽量减小锁的粒度，使代码更大程度的并发（能在代码段上加同步就不要在整个方法上加同步）
b. synchronized(XX.class)实现了全局锁的效果
  static synchronized方法也相当于锁住了代码段
c. 因wait()、notify()、notifyAll()会对对象的“锁标志”进行操作，所以他们必须在synchronized函数或synchronized block中进行调用，否则会抛出异常IllegalMonitorStateException的异常

结论：1.不同对象实例的对象锁是互不干扰的，但每个类只有一个类锁
     2.类锁和对象锁互不干扰

## 三、引用传递和值传递
1. 基本类型（byte,short,int,long,double,float,char,boolean）为传值
2. 对象类型（Object,数组，容器）为传引用
3. String、Integer、Double等immutable类型因为类的变量设为final属性，无法被修改，只能重新赋值或生成对象。
当Integer作为方法参数传递时，对其赋值会导致原有的引用被指向了方法内的栈地址，失去原有的的地址指向，所以对赋值后的Integer做任何操作都不会影响原有值。

## 四、JAVA线程run与start方式的区别
1. start() 通过该方法启动线程的同时也创建了一个线程，真正实现了多线程。run()方法称为线程体，包含线程要执行的内容，run()方法运行结束，则线程随即停止。无需等待run()方法中的代码执行完毕就可以执行线程外面的代码。
2. run() 在当前线程开启（如果当前线程是主线程则运行在主线程，如果当前线程是自线程则运行在自线程），没有达到写线程的目的。要顺序执行，要等待run方法体执行完毕后才可以继续执行下面的代码。

## 五、JAVA停止线程
使用Thread.interrupt()方法
判断线程是否停止状态
1. thread.interrupted()：作用于当前线程是否已经中断；（清除中断标志，并返回原来的状态）
2. thread.isInterrupted()：作用于调用该方法的线程对象所对应的的线程；
停止线程方式：
1. 将方法interrupt()与return结合使用，可以实现停止线程的效果
2. 建议使用“抛异常”的方法来实现线程的停止，因为在cache块中还可以将异常向上抛，使线程停止事件得以传播

参考：http://www.cnblogs.com/greta/p/5624839.html
http://www.cnblogs.com/w-wfy/p/6414801.html

## 六、compareTo和compare方法的比较
1. compareTo 是java.lang.Comparable接口中的方法，当需要对某个类的对象进行排序时，该类必须要实现Comparable接口，且须重写compareTo方法
2. compare 是java.util.Comparator接口中的方法，实际上用的是待比较对象的compareTo方法
参考：http://blog.csdn.net/pange1991/article/details/53954043
## 七、聚合与组合的区别

## 八、equals与==的区别
1. ==
对于基本数据类型，比较的是值是否相同
对于复合数据类型，比较的是他们在内存中存放的地址（只对于同一个new出来的对象，比较结果为true，否则为false）
2. equals
是Object基类中的方法，该方法是用==实现的（所以在没有复写equals的情况下，比较的还是内存中存放的地址）

equals方法可以被重写，但是==不可以被重写

## 九、运行时注解和编译时注解的区别

## 十、堆和栈的区别
堆主要是用来存放对象的，栈主要是用来执行程序的
