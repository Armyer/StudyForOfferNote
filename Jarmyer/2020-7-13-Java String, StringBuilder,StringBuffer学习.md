### String, StringBuffer, StringBuilder区别
**可变性**
String类中使用final关键字修饰字符数组来保存字符串，private final value[]，所以String对象是不可变的。在Java9之后，string类的实现改用byte数组存储字符串private final byte[ ] value

StringBuilder和StringBuffer都继承AbstractStringBuilder类，在AbstractStringBuilder中也是使用字符数组保存字符串char[] value，但是没有用final关键字修饰，所以这两种对象都是可变的。

**线程安全性**
String中的对象是不可变的，可以理解为常量，**线程安全**。
AbstractStringBuilder是Stringbuffer和StringBuilder的公共父类，定义了一些字符串的基本操作，如expandCapacity, append, insert, indexOf等公共方法。StringBuffer对方法加了同步锁或者对调用方法加了同步锁，所以是**线程安全**。StringBuilder没有对方法进行加同步锁，所以是**线程不安全**。

**性能**
每次对String类型进行改变时候，都会生成一个新的String对象，然后将指针指向新的String对象。
StringBuffer每次都会对StringBuffer对象本身进行操作，而不是生成新的对象并改变对象引用。
相同情况下，StringBuilder相比使用StringBuffer仅能获得10%-15%左右性能提升，但却要冒多线程不安全的风险。

**总结**
1. 操作少量的数据：使用String
2. 单线程操作字符串缓冲区下操作大量数据：使用StringBuilder
3. 多线程操作字符串缓冲区下操作大量数据：使用StringBuffer

