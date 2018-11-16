# Transient

用来表示所修饰的域不是改对象串行化的一部分。

---

序列化的使用场景：Java内存中的对象是无法进行IO操作或网络通信，必须将这些对象以某种方式表示出来，即存储对象中的状态。  
Java提供序列化的方式来表示对象。

* 序列化：将一个对象转换成一串二进制表示的字节数组，通过保存或转移这些字节数据来达到持久化的目的。
* 反序列化：将字节数组重新构造成对象。

序列化只需要实现`java.io.Serializable`接口。

序列化的时候有一个`serialVersionUID`参数，Java序列化机制是通过在运行时判断类的serialVersionUID来验证版本一致性的。在进行反序列化，Java虚拟机会把传过来的字节流中的serialVersionUID和本地相应实体类的serialVersionUID进行比较， 如果相同就认为是一致的实体类，可以进行反序列化，否则Java虚拟机会拒绝对这个实体类进行反序列化并抛出异常。  
**如果实现 java.io.Serializable接口的实体类没有显式定义一个名为serialVersionUID、类型为long的变量时，Java序列化机制会根据编译的.class文件自动生成一个serialVersionUID，如果.class文件没有变化，那么就算编译再多 次，serialVersionUID也不会变化。**换言之，Java为用户定义了默认的序列化、反序列化方法，其实就是`ObjectOutputStream`的`defaultWriteObject`方法和`ObjectInputStream`的`efaultReadObject`方法。

---

Ref：[《Java对象表示方式1：序列化、反序列化和transient关键字的作用》](https://www.cnblogs.com/szlbm/p/5504166.html)
