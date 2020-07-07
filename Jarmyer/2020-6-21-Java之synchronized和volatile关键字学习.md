### **synchronized :**
英文解释如下：
英 ['sɪŋkrənaɪzd]  美 ['sɪŋkrənaɪzd] 
**adj**. 同步的；同步化的
**v**. 使协调（synchronize的过去分词）；同时发生；校准

作为Java其中的关键字之一，用于解决多个线程之间访问资源的同步性。在实际代码中修饰方法或是代码块，使其在任意时刻智能有一个线程执行。

Java早期版本，synchronized属于重量级锁、效率很低，主要原因在于其**依赖底层操作系统**实现的，而底层操作系统实现线程之间的切换时需要从用户态转为内核态，这个转换状态需要相对较长的时间，因而时间成本相对较高。后来在Java1.6之后官方对JVM层面对synchronized进行较大优化。现在的其锁效率优化得不错了。JDK1.6对锁的实现引入大量的优化，如**自旋锁、适应性自旋锁、锁消除、锁粗化、偏向锁、轻量锁**等技术来减少锁操作的开销。

### 如何使用synchronized？

| 名称 |说明  |
| --- | --- |
|修饰实例方法  |  对当前对象实例加锁，进入同步代码前要获得当前对象实例的锁|
|修饰静态方法  |给当前类加锁，作用于类的所有对象实例，因为静态成员不属于任何一个实例对象，是类成员。  |
|修饰代码块  |指定加锁对象，对给定对象加锁，进入同步代码库前要获得给定对象的锁  |

总结：无论该关键字加到static静态方法还是代码块上都是给Class类上锁。加到实例方法上则是给该对象实例上锁。尽量不要使用synchronized（String s)，因为JVM中，字符串常量池具有缓存功能！缓存了就不好上锁了！

### **Volatile:**

volatile英 [ˈvɒlətaɪl]  美 [ˈvɑːlətl] 
**adj**. [化学] 挥发性的；不稳定的；爆炸性的；反复无常的
**n**. 挥发物；有翅的动物n. (Volatile)人名；(意)沃拉蒂莱

在Java中主要想表达的意思应该是形容词，不稳定等意思。主要作用就是保证变量的可见性，并且还有一个作用是防止指令重排序。
在实际线程程序运行时会出现如下图所示情况，在工作内存中，变量可能和主内存不同，因而会导致出错。
![image](https://github.com/awqcs/Study-for-Offer/blob/master/Jarmyer/image/volatile-1.JPG)
使用volatile关键字之后工作原理就如下图所示：
![image](https://github.com/awqcs/Study-for-Offer/blob/master/Jarmyer/image/volatile-1.JPG)


### **synchronized和volatile区别？**


| 名称 |说明  |
| --- | --- |
| 使用体验上 |volatile关键字是线程同步的轻量级实现，性能更好，但只能用于变量，而synchronized关键字可修饰方法以及代码块。经过后期优化，现在实际开发中synchronized使用较多  |
| 阻塞 |volatile不会发生阻塞，synchronized会发生阻塞  |
| 可见性 | volatile可保证数据的可见性，不保证数据的原子性，synchronized两者都能保证。 |
|补充  |volatile用于解决多个线程之间的可见性，而synchronized解决的是多个线程之间访问资源的同步性 |