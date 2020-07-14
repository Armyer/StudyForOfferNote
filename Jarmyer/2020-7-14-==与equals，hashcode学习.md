
==:
判断两个**对象的地址**是不是相等的。即。判断两个对象是不是同一个对象（基本数据类型==比较的是值，引用数据类型==比较的是内存地址）

equals( )：
判断两个对象是否相等。但它一般有两种使用情况：
1. 类没有覆盖equals（）方法。则通过equals（）比较该类的两个对象时，等价于通过“==”比较这两个对象。
2. 类覆盖了equals（）方法。一般，我们覆盖equals（）方法来比较两个对象的内容是否相等；若他们的内容相等，则返回true。

`String a = new String("ab");`
`String b = new String("ab");`
`String aa="ab"`
`String bb = "ab"`
`if(a==b) false`
`if(a.equals(b) true`
`if(42==42.0) true`
说明“

* String中的equals方法是被重写的，因为object的equals方法是比较的对象的内存地址，而String的equals方法比较的是对象的值。
* 当创建String类型的对象时，虚拟机会在常量池中查找有没有已经存在的值和要创建的值相同的对象，如果有就把它赋值给当前引用。如果没有就在常量池中重新创建一个String对象。

hashcode()与equals（）的相关规定
1.如果两个对象相等，则hashcode一定也是相同的
2.两个对象相等，对两个对象分别调用equals方法都返回true
3.两个对象有相同的hashcode值，它们也不一定是相等的
4.因此，equals方法被覆盖过，则hashcode方法也必须被覆盖。否则会出现hashcode相等，但是实际的值不相等，造成没有正确插入。
5.hashcode的默认行文是对堆上的对象产生独特值。如果没有重写hashcode，则该class的两个对象无论如何都不会相等。 


**String类中的hashcode函数源码**
public int hashCode() {   
int h = hash;   
if (h == 0 && value.length > 0) 
{       
char val[] = value;       
    for (int i = 0; i < value.length; i++)
    {           
       **h = 31 * h + val[i];**
    }        
    hash = h;   
}    
return h;
}
**源码中，为什么选择31这个数字？**

原因有两个：
1. 31是一个不大不小的质数，是作为hashcode乘子的优选质数之一。
2. 31可以被JVM优化，31 * i == (i<<5) - i。假设有50000个英文单词进行hashcode运算，使用31，33，37，39，41作为乘子，每个常数算出的哈希值冲突数都小于7个。

