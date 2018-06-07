## 当一个线程进入到一个对象的synchronized方法后，其它线程可以进入此对象其它方法吗？
1）其它方法是否加了synchronized关键字，如果没加，则可以进入
2）如果这个方法内部调用了wait，则可以进入其它synchronized方法
3）如果其他个方法都加了synchronized关键字，并且内部没有调用wait，则不能。
4）如果其他方法是static，它用的同步锁是当前类的字节码，与非静态的方法不能同步，因为非静态的方法用的是this。

## synchronized 与 static synchronized的区别
synchronized是对类的当前实例（当前对象）进行加锁，防止其他线程同时访问该类的该实例的所有synchronized块。（类的两个不同实例就没有这种约束了）
static synchronized是限制多线程中，该类的所有实例同时访问jvm中该类所对应的代码块

## 结论（synchronized锁住的是一个对象或者类（其实也是对象），而不是方法或者代码段）
1）synchronized static是某个类的范围，synchronized static 方法防止多个线程同时访问这个类中的synchronized static 方法。它可以对类的所有对象实例起作用。
2）synchronized 是某实例的范围，synchronized isSync(){}防止多个线程同时访问这个实例中的synchronized 方法。
3）synchronizedmethods(){} 与synchronized（this）{}之间没有什么区别，只是 synchronized methods(){} 便于阅读理解，而synchronized（this）{}可以更精确的控制冲突限制访问区域，有时候表现更高效率。
4）也就是说，基类的方法synchronized f(){} 在继承类中并不自动是synchronized f(){}，而是变成了f(){}。继承类需要你显式的指定它的某个方法为synchronized方法；
