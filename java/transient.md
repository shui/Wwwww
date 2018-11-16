# Transient

用来表示所修饰的域不是改对象串行化的一部分。

---

序列化的使用场景：Java内存中的对象是无法进行IO操作或网络通信，必须将这些对象以某种方式表示出来，即存储对象中的状态。  
Java提供序列化的方式来表示对象。

* 序列化：将一个对象转换成一串二进制表示的字节数组，通过保存或转移这些字节数据来达到持久化的目的。
* 反序列化：将字节数组重新构造成对象。

序列化只需要实现`java.io.Serializable`接口。

序列化的时候有一个`serialVersionUID`参数，Java序列化机制是通过在运行时判断类的serialVersionUID来验证版本一致性的。在进行反序列化，Java虚拟机会把传过来的字节流中的serialVersionUID和本地相应实体类的serialVersionUID进行比较， 如果相同就认为是一致的实体类，可以进行反序列化，否则Java虚拟机会拒绝对这个实体类进行反序列化并抛出异常。  
**如果实现 java.io.Serializable接口的实体类没有显式定义一个名为serialVersionUID、类型为long的变量时，Java序列化机制会根据编译的.class文件自动生成一个serialVersionUID，如果.class文件没有变化，那么就算编译再多 次，serialVersionUID也不会变化。**

Java为用户提供默认的序列化、反序列化方法，其实就是`ObjectOutputStream`的`defaultWriteObject`方法和`ObjectInputStream`的`efaultReadObject`方法。  
可以重写这两个方法来自定义序列化/反序列化的过程。（使用场景举例：某些敏感字段在序列化前需要加密，在反序列化后解密；某些字段不需要序列化，可以将这些字段声明为transient再进行操作。）

虽然Java的序列化能够保证对象状态的持久保存，但是遇到一些对象结构复杂的情况还是比较难处理的，最后对一些复杂的对象情况作一个总结：  
1. 当父类继承Serializable接口时，所有子类都可以被序列化。
2. 子类实现了Serializable接口，父类没有，父类中的属性不能序列化（不报错，数据丢失），但是在子类中属性仍能正确序列化。
3. 如果序列化的属性是对象，则这个对象也必须实现Serializable接口，否则会报错。
4. 反序列化时，如果对象的属性有修改或删减，则修改的部分属性会丢失，但不会报错。
5. 反序列化时，如果serialVersionUID被修改，则反序列化时会失败。

---

Ref：[《Java对象表示方式1：序列化、反序列化和transient关键字的作用》](https://www.cnblogs.com/szlbm/p/5504166.html)
