# HashMap

需要看解析就读这篇原作[《Java7/8 中的 HashMap 和 ConcurrentHashMap 全解析》](https://javadoop.com/post/hashmap)。

## A：

HashMap不支持并发操作。底层是一个数组。在JDK1.7前，数组每个元素是一个单向链表；1.8中，当链表的元素达到8个时，会将链表转换成红黑树；查找的时间复杂度从原先的_O\(n\)_降低到_O\(logN\)_。

1.7使用Entry表示HashMap的数据节点，1.8用Node（Node用于链表，TreeNode用于红黑树，这样根据第一个节点数据类型是Node还是TreeNode来判断该位置下是否是红黑树），两者基本无区别，都是key、value、hash、next四个属性。

1.7先扩容再插值，1.8反之。扩容倍数为2。

三个参数：

* capacity：当前数组容量，始终保持 2^n，可以扩容，扩容后数组大小为当前的 2 倍。
* loadFactor：负载因子，默认为 0.75。
* threshold：扩容的阈值，等于 capacity \* loadFactor。
