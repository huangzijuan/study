## 一、 加载因子默认0.75
加载因子默认0.75是“哈希冲突”和“空间利用率”矛盾的一个折中

## 二、底层数据结构
数组（也称哈希桶）加链表的形式，链表中的每个节点就是哈希表中的每个元素，在jdk8中，当链表长度达到8，会转化成红黑树，以提升它的查询、插入效率。

## 三、扩容resize、rehash过程
当元素数量大于阈值(threshold)对时候要进行扩容，hash桶的长度一定为2的次方（这样在根据key的hash值寻找对应的哈希桶时indexFor(hashvalue)，可以用位运算代替取余操作）
扩容操作时会new一个新的Node数组作为哈希桶，然后将原hash表中的数据全部移动到新的hash桶中，相当于对原hash表中的所有数据都做了一个put操作，性能消耗很大。所以哈希表容量越大，性能消耗越明显。
扩容是容量所以原链表上的每个节点，现在可能存放在原来的下标，即low位，或者扩容后的下标high位（high位=low位+原哈希桶容量），若追加节点后，链表数量>=8，则转化为红黑树。

## 四、特点
1. hashmap是线程不安全的，允许key为null，value为null。遍历时是无序的
2. hash桶的长度默认是16

## 五、与hashtable的区别
1. hashtable是线程安全的，不允许key、value是null
2. hashtable默认容量是11，扩容时，新容量是原来的2n+1倍，所以取哈希桶下标时使用的是模运算
3. hashtable直接使用key的hashcode作为hash值
4. hashtable是dictionary的子类同时也实现了map接口，hashmap是map接口的一个实现类

## 六、一些流程图
![hashmap_put](http://p5xecv7m0.bkt.clouddn.com/fc1a88acc7944fca3b590944770005fc.png)

## 七、1.8之后HashMap 中关于红黑树的三个关键参数

TREEIFY_THRESHOLD
一个桶的树化阈值
static final int TREEIFY_THRESHOLD = 8
当桶中元素个数超过这个值时
需要使用红黑树节点替换链表节点

UNTREEIFY_THRESHOLD
一个树的链表还原阈值
static final int UNTREEIFY_THRESHOLD = 6
当扩容时，桶中元素个数小于这个值
就会把树形的桶元素 还原（切分）为链表结构

MIN_TREEIFY_CAPACITY
哈希表的最小树形化容量
static final int MIN_TREEIFY_CAPACITY = 64
当哈希表中的容量大于这个值时，表中的桶才能进行树形化
否则桶内元素太多时会扩容，而不是树形化
为了避免进行扩容、树形化选择的冲突，这个值不能小于 4 * TREEIFY_THRESHOLD


## 其它
时间复杂度：最优情况为O(1)  最坏情况位O(N)

## 参考
https://mp.weixin.qq.com/s/zSpQEiaxSgGqirDMSeyMfQ
