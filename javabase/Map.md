map是键值对的集合接口，它的实现类主要包括

## HashMap 线程非同步
它根据key的HashCode值来存储数据
访问速度快
最多只允许一条记录的key值为null，允许多条记录的value值为null

## TreeMap 线程非同步
能够把保存的记录根据key排序，默认升序排序，也可以指定排序的比较器
当用Iterator遍历TreeMap时，得到的记录是排过序的
不允许key值为null

## HashTable 线程同步
key和value值均不允许为null
写入时比较慢

## LinkedHashMap 线程非同步
key和value值均允许为null
保存了记录的插入顺序，在用Iterator遍历时，先得到的记录是先插入的
遍历时候比HashMap慢
