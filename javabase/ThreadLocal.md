## 常用方法
1. void set(Object value)
2. public Object get()
3. public void remove() 将当前线程局部变量的值删除
当线程结束后，该线程对应的局部变量将自动被垃圾回收。故显式调用该方法不是必须的操作，但它可以加快内存回收的速度
4. protected Object initialValue() 返回该线程局部变量的初始值
这是一个延迟调用方法，在线程第一次调用get()或是set(Object)时才执行。

## ThreadLocal与线程同步机制的比较
ThreadLocal：一个线程对应一个实例
Synchronize：多个线程共享一个实例
