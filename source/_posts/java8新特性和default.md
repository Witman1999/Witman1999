---
title: java8新特性和default
date: 2019-08-16 15:29:49
tags: 基础知识
categories: java
copyright: true
---
# 新特性
> JDK1.8 为了加强接口的实用能力，使得接口可以存在具体的方法，前提是方法需要被 default 和 static 修饰
```java
public interface  D {
	default void method1() {
		System.out.println("我是接口的默认方法");
	}
	static void method2() {
		System.out.println("我是接口的静态方法");
	}
}
```
<!-- more -->
**<font color=red>注意：</font>**  
- 用 default <font color=red>修饰的方法必须是用方法体，不能方法体为空，不能用以下形式声明在接口</font>
```java
default void method1();
```
- 如果一个<font color=red> A 类继承 B,C 两个接口，此时接口中用同名的 default 修饰的方法，那么此时编译器会报错</font>，编译器不知道调用哪一个。
- <font color=red>default 方法不能通过类名调用（对象级），static 方法可以通过类名调用（类级）。</font>
- 一个接口可以有多个default方法, 也可以有多个static方法
## defautl另一种使用方法
>以上是 default 的一种使用方法，另外一种则是在 switch 语句中，在 switch 中如果没有与 case 匹配的就与 default 匹配，这里就不多介绍了。
# 总结
- default 可以使得接口有具体的默认方法
- default 修饰的方法，被继承的子类也同时具有该默认方法，并且可以被重写
- 主要是解决继承该接口的类有些具有同样的方法功能，每个类都要写这段重复的代码，显然费时，这也是新特性的意义。
### <font color=green>附</font>
注意这里的 default 与类中的 default 的修饰词是不一样的，两者意义不同，而且类中 default 是不能显示写出来，而是默认如果你没有写修饰符，默认就是 default ，所以不能写出来。

