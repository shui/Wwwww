# ConcurrentHashMap

这一段可以看下[《为并发而生的 ConcurrentHashMap（Java 8）》](https://www.cnblogs.com/yangming1996/p/8031199.html)。

## A：

ConcurrentHashMap支持并发。

1.7中使用分段锁（简单理解：ConcurrentHashMap是一个Segment数组），整个Hash表被分成多个段，每个段中会对应一个Segment段锁，段与段之间可以并发访问，但是多线程想要操作同一个段是需要获取锁的。所有的put、get、remove等方法都是根据键的hash值对应到相应的段中，然后尝试获取锁进行访问。

1.8改用`CAS`+`synchronized`控制并发操作，在某些方面提升了性能。并且追随1.8的HashMap底层实现，使用数组+链表+红黑树进行数据存储。
