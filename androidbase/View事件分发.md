## 事件分发顺序
Activity->Window->View

## 事件优先级
OnTouchListen>onTouchEvent>OnClickListen

## 滑动冲突
主要有以下两种形式
#### 一、外部滑动方向与内部方向不一致
主要判断滑动方向是竖直的还是横向的。（判断方法：1.竖直距离与横向距离的大小比较 2.滑动路径与水平形成的夹角）
#### 二、外部滑动方向与内部方向一致
根据具体业务逻辑做相应的处理

## 事件传递的结论
1. 同一个事件序列是指手机接触屏幕那一刻起，到离开屏幕那一刻结束，有一个down事件，若干个move事件，一个up事件构成。

2. 某个View一旦决定拦截事件，那么这个事件序列之后的事件都会由它来处理，并且不会再调用onInterceptTouchEvent。

3. 正常情况下，一个事件序列只能被一个View拦截并消耗。这个原因可以参考第2条，因为一旦拦截了某个事件，那么这个事件序列里的其他事件都会交给这个View来处理，所以同一事件序列中的事件不能分别由两个View同时处理，但是我们可以通过特殊手段做到，比如一个View将本该自己处理的事件通过onTouchEvent强行传递给其他View处理。

4. 一个View如果开始处理事件，如果它不处理down事件（onTouchEvent里面返回了false）,那么这个事件序列的其他事件就不会交给它来继续处理了，而是会交给它的父元素去处理。

5. 如果一个View处理了down事件，却没有处理其他事件，那么这些事件不会交给父元素处理，并且这个View还能继续受到后续的事件。而这些未处理的事件，最终会交给Activity来处理。

6. ViewGroup的onInterceptToucheEvent默认返回false,也就是默认不拦截事件。

7. View没有InterceptTouchEvent方法，如果有事件传过来，就会直接调用onTouchEvent方法。

8. View的onTouchEvent方法默认都会消耗事件，也就是默认返回true,除非他是不可点击的（longClickable和clickable同时为false）。

9. View的enable属性不会影响onTouchEvent的默认返回值。就算一个View是不可见的，只要他是可点击的（clickable或者longClickable有一个为true）,它的onTouchEvent默认返回值也是true。

10. onClick方法会执行的前提是当前View是可点击的，并且它收到了down和up事件。

11. 事件传递过程是由外向内的，也就是事件会先传给父元素在向下传递给子元素。但是子元素可以通过requestDisallowInterceptTouchEvent来干预父元素的分发过程，但是down事件除外（因为down事件方法里，会清除所有的标志位）。

## 参考
http://www.jianshu.com/p/057832528bdd
