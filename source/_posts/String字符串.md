---
title: String字符串
date: 2019-11-18 15:43:00
tags: String
categories: java
keywords: String字符串
copyright: true
---
# 一、 String 简介


## String 不变原理（从源码上讲）
String 对象是不可改变的，String类中每一个==看起来会修改String对象值得方法，实际上都是创建了一个全新得String对象==，包含了修改后得字符串内容，最初得原始对象没有改变过
<!--more-->
### String 源码
####  String 属性值
```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];

    /** Cache the hash code for the string */
    private int hash; // Default to 0

    private static final long serialVersionUID = -6849794470754667710L;

   
    private static final ObjectStreamField[] serialPersistentFields =
        new ObjectStreamField[0];
     
    ......
    }
```
####  String 构造函数
```java
    /**
     ...
     */
    public String() {
        this.value = "".value;
    }
    /**
     ...
     */
    public String(String original) {
        this.value = original.value;
        this.hash = original.hash;
    }
    /**
     ...
     */
    public String(char value[]) {
        this.value = Arrays.copyOf(value, value.length);
    }
    /**
     ...
     */
    public String(char value[], int offset, int count) {
        if (offset < 0) {
            throw new StringIndexOutOfBoundsException(offset);
        }
        if (count <= 0) {
            if (count < 0) {
                throw new StringIndexOutOfBoundsException(count);
            }
            if (offset <= value.length) {
                this.value = "".value;
                return;
            }
        }
        if (offset > value.length - count) {
            throw new StringIndexOutOfBoundsException(offset + count);
        }
        this.value = Arrays.copyOfRange(value, offset, offset+count);
    }
    ......
```
#### 理由
从上面得源码可以知道，**String得value属性值是一个字符数组，字符串实际由字符串数组组成，并且被final修饰，所以不能被修改**。
# 二、 创建字符串的两种方式
##  通过构造方法创建字符串对象 
**通过构造函数创建**的字符串是**在堆内存**
```java
String str=new String("hello");
```
**++这里创建了多少对象++？**  
**2个。  
原因**：
- jvm 会在 String pool  中寻找是否存在 "hello" ,如果没有则创建，有则什么都不做
- 之后遇到了 new ，又在 Java head 中创建了一个对象用了存储 "hello"  

所以一共创建了两个
##  通过直接赋值创建字符串
```java
String str="hello";
```
通过**直接赋值创建**的对象是**在方法区的常量池**
##  两种实例化方法的比较
- **代码上的比较**
```java
public class TestString {
    public static void main(String[] args) {
        String str1 = "Lance";
        String str2 = new String("Lance");
        String str3 = str2; //引用传递，str3直接指向st2的堆内存地址
        String str4 = "Lance";
        /**
         *  ==:
         * 基本数据类型：比较的是基本数据类型的值是否相同
         * 引用数据类型：比较的是引用数据类型的地址值是否相同
         * 所以在这里的话：String类对象==比较，比较的是地址，而不是内容
         */
         System.out.println(str1==str2);//false
         System.out.println(str1==str3);//false
         System.out.println(str3==str2);//true
         System.out.println(str1==str4);//true
    }

}
```

- **内存图比较**  
如图  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/61B212D408E641FDAF30E5A20B725CEC/7585.jpg)
##  字符串常量池
在字符串中，如果采用**直接赋值的方法进行对象的实例化，则会将匿名对象放入字符串常量池**，每当**下一次对不同的对象进行直接赋值时，会直接利用池中的原有的匿名对象**。

## 总结
1. **直接赋值**：开辟一块堆内存空间，并且**自动入池**，**不会产生垃圾**
2. **构造函数**：会**开辟两块内存堆空间**，其中一块堆内存会变成垃圾被系统回收掉，而且不能够自动入池，要手动入池，另一块堆空间存储值。

在<font color=red>开发过程中尽量不用采用构成函数来进行字符串实例化</font>
# 三、 String不可变的性质（从内存上讲）
意思是：<font color=red>String是个常量，从一出生就注定不可变</font>  
从第一点就看到，String 是被 final 所修饰的，不可变，以下是经典例子
```java
public class Apple {
    public static void main(String[] args) {
        String a = "abc";
        String b = "abc";
        String c = new String("abc");
        System.out.println(a==b);  //true
        System.out.println(a.equals(b));  //true
        System.out.println(a==c);  //false
        System.out.println(a.equals(c));  //true
    }
}
```
## 原因
因为有着字符串常量池的的缘故，**每次当直接赋值时，jvm 都会在池寻找是否已经存在该字符串，如果有，则使用同一个字符串,没有，则生成一个**,所以，这也就是为什么上面的例子 ``a==b`` 为 ``true`` , ``a==c`` 为 ``false`` ,因为变量只是保存地址值 ``==`` 比较的是地址，而，``equals()`` 比较的字符串的内容。  
以上的这种模式，叫做<font color=red>享元模式</font>
## 不变的好处
可以实现**多个变量引用堆内存中的同一个字符串实例，避免创建的开销。**

　　我们的程序中大量使用了String字符串，有可能是**出于安全性考虑**。

　　大家都知道**HashMap中key为String类型**，如果可变将变的多么可怕。

　　当我们在**传参的时候，使用不可变类不需要去考虑谁可能会修改其内部的值，如果使用可变类的话，可能需要每次记得重新拷贝出里面的值，性能会有一定的损失**。
　　
# 重载"+"与StringBuilder 构建字符串
```java
public class test{
    public static void main(String[] agrs){
        String mango="hello";
        String s="abc"+mango+"def"+47;
        System.out.println(s);
    }
}
```
上面的这段代码，我们会这样想，String可能有个 append() 方法，他会生成一个新的String对象，这个新生成的对象包好了“abc” 与 mango 连接后的字符串，以此类推。  
 
但是<font color=red>**这种工作方式，我们知道，他最终生成的String对象中途会产生一堆垃圾回收的中间对象**</font>。这样会发现性能相当糟糕  

通过反编译字节码我们看到  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/0E4F84B6F8EF405C9B751B175D634653/7697.jpg)  

<font color=red>**编译器自动使用了 StringBuilder 类来构造最终 String 对象**</font>，并且调用StringBuilder 的 append() 方法，总计四次，然后调用toString() 生成结果。  

现在可能**认为编译器会自动优化**，这里在使用**两种不同的方式**来生成 String 比较，**一种使用多个 String 对象，一种使用 StringBuilder，对应着下面的 implicit() 方法和 explicit() 方法**  
 ![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/16098DC71BF64A70BB30880F97993BFB/7721.jpg)  
 
 反编译之后，首先是 **implicit() 方法**   
 ![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/447D14294E6E4E2CB0B59E55155FA729/7726.jpg)  
 
 可以看出，<font color=red>**从第8行开始到第35行都在重复的生成 StringBuilder 对象**</font>  
 接下来是 **explicit() 方法**
 
 ![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/EFD46250018D410799521F4F67D17215/7728.jpg)  
 我们可以看的，<font color=red>**代码量进行了缩短，并且只生成了一个 StringBuilder 对象**</font>。  
 
 所以如果是**简单字符串**，可以**交给编译器来合理构造**，不然**使用 StringBuilder 对象的 append() 方**法一个个拼接起来
 
 # 附加（字符串常量+字符串常量=字符串常量？）
对于以下代码
```java
String test1="helloworld";
String test2="hello"+"world";
String test3="hello";
String test4=test3+"world";
String test5=new String("helloworld");

System.out.println(test1==test2);//true
System.out.println(test1==test4);//false
System.out.println(test1==test5);false
```
<font color=blue>从上面代码例子中看出，为什么 ``test1==test2`` 会 ``true`` ，而 ``test1==test4`` 会 ``false``。</font>  
-  对于 ``test1`` 为什么会等于 ``test2`` ,因为**两个都是字面字符串常量**，Java 在**编译期间**，就会**将两边拼接起来**，因为**编译器认为这个时候的值是不会发生改变**，这个**运算即使放在运行时不会变化**，所以**编译期就放到同一个常量**池中了。  
-  在 ``test4`` 中**有一变量**（严格意义上的变量，可以被改变的数据，可大可小可长可短能伸能缩，所有需要一次以上处理才能成为直接字面字符的     值存在时 java都一律将其视为变量），**无论这里几个变量**，因为  ``Java`` **并不知道这里 ``test3`` 到底是什么**，**只知道他是一个 String 变量（在编译期）**，**具体值是在运行时而去处理**，和多态很像。 

从前面的知识点得知，**Java 在处理字符串变量 + 时会生成一个 StringBuilder 的 append（） 方法，最后 toString() 方法来获得字符串，这是就 new 出来了一个新的堆空间，就不一样了**。

 
 