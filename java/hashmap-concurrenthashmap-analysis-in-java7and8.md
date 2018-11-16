# HashMap和ConcurrentHashMap

需要看解析就读这篇原作[《Java7/8 中的 HashMap 和 ConcurrentHashMap 全解析》](https://javadoop.com/post/hashmap)。

## A1：

HashMap不支持并发操作。底层是一个数组。在JDK1.7前，数组每个元素是一个单向链表；1.8中，当链表的元素达到8个时，会将链表转换成红黑树；查找的时间复杂度从原先的_O\(n\)_降低到_O\(logN\)_。

1.7使用Entry表示HashMap的数据节点，1.8用Node（Node用于链表，TreeNode用于红黑树，这样根据第一个节点数据类型是Node还是TreeNode来判断该位置下是否是红黑树），两者基本无区别，都是key、value、hash、next四个属性。

1.7先扩容再插值，1.8反之。扩容倍数为2。

三个参数：

* capacity：当前数组容量，始终保持 2^n，可以扩容，扩容后数组大小为当前的 2 倍。
* loadFactor：负载因子，默认为 0.75。
* threshold：扩容的阈值，等于 capacity \* loadFactor。

## A2：

这一段可以看下[《为并发而生的 ConcurrentHashMap（Java 8）》](https://www.cnblogs.com/yangming1996/p/8031199.html)。

ConcurrentHashMap支持并发。

1.7中使用分段锁（简单理解：ConcurrentHashMap是一个Segment数组），整个Hash表被分成多个段，每个段中会对应一个Segment段锁，段与段之间可以并发访问，但是多线程想要操作同一个段是需要获取锁的。所有的put、get、remove等方法都是根据键的hash值对应到相应的段中，然后尝试获取锁进行访问。

1.8改用`CAS`+`synchronized`控制并发操作，在某些方面提升了性能。并且追随1.8的HashMap底层实现，使用数组+链表+红黑树进行数据存储。