## 输入法生命周期
![life_cycle](/assets/life_cycle.png)

## 关键类及作用
1. LatinIME：核心方法，继承InputMethodService，用来调配业务层、逻辑层与视图层
2. InutLogic：输入事件的逻辑层，是LatinIME与RichInputConnection连接的关键
3. RichInputConnection：通过组合的方式引入InputConnection，InputConnection是输入法向调用应用传递字符、键盘事件、文本等的关键方法
4. KeyboardSwitcher：视图层枢纽，用来控制视图层的显示、切换等
5. input_view.xml：整体键盘布局
6. main_keyboard_frame.xml：字母键盘布局（包括候选词显示栏）
7. MainKeyboardView：字母键盘布局（不包括候选词显示栏）
8. Key：键盘上的按键
9. KeyboardBuilder：解析键盘配置的信息（LatinIME中键盘的信息都是配置在各个xml文件中的，然后通过KeyboardBuilder方法解析出来）
10. KeyboardView：主键盘控件，负责键盘、按键的绘制
11. SubtypeSwitcher：控制输入法语言切换

## 一些方法
1. loadKeyboard:解析布局文件
2. LatinKeyboard.createKeyFromXml，Keyboard.createKeyFromXml：从XML文件创建一个按键。
3. getDimensionOrFraction：获取某一个属性的值。这个属性值的格式必须规定为Dimen(dip,px,sp,in等)或者Fraction（百分比）的。
4. LatinKeyboardBase.onBufferDraw：把所有的Key绘制在一张Bitmap上，再由继承自ViewonDraw方法把这张Bitmap渲染到onDraw传递过来的Canvas上。

绘制Key的时候，主要绘制两个东西，label和icon。对于a,b,c,1,2,&等这样可以用字符来表示的键，就绘制它的label属性。对于Shift,Alt等这样无法用字符表示的键，就绘制它的icon属性。
