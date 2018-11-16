# final

final在Java中是一个保留的关键字，可以声明成员变量、方法、类以及本地变量。  
一旦你将引用声明作final，你将不能改变这个引用了，编译器会检查代码，如果你试图将变量再次初始化的话，编译器会报编译错误。

## final变量

final变量是只读的，不能对final变量再次赋值。

final变量经常和static关键字一起使用，作为常量。

* final成员变量必须在声明的时候初始化或者在构造器中初始化，否则就会报编译错误。
* final本地变量必须在声明时赋值。
* 在匿名类中所有变量都必须是final变量。
* 接口中声明的所有变量本身是final的。

## final方法

表示方法不可以被子类的方法重写。

final方法比非final方法要快，因为在编译的时候已经静态绑定了，不需要在运行时再动态绑定。

## final类

表示类不能被继承。

*final类不可能被abstract修饰。*

## final的好处

* final关键字提高了性能。JVM和Java应用都会缓存final变量。
* final变量可以安全的在多线程环境下进行共享，而不需要额外的同步开销。
* 使用final关键字，JVM会对方法、变量及类进行优化。

## 不可变类

不可变类是指它的对象一旦被创建了就不能被更改了。  
不可变类有很多好处，譬如它们的对象是只读的，可以在多线程环境下安全的共享，不用额外的同步开销等等。

Java中有许多类是final的，譬如String, Interger以及其他包装类。  

可以看下[《如何写一个不可变类？》](http://www.importnew.com/7535.html)。


---

Ref:  
原文链接：[Javarevisited](http://javarevisited.blogspot.hk/2011/12/final-variable-method-class-java.html)
翻译：[ImportNew.com](http://www.importnew.com/) - [唐小娟](http://www.importnew.com/author/tangxiaojuan)
译文链接：<http://www.importnew.com/7553.html>