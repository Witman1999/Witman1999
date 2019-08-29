---
title: java中的引用
date: 2019-08-16 15:32:17
tags: 
	- 引用
	- 基础知识
categories: java
copyright: true
---
>  参考来源  点击[这里](https://www.cnblogs.com/czx1/p/10665327.html)
# 值类型与引用类型
```java
    int num=10;
    String str="hello";
```
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/ED36801302CB4FC99BD307A99771EEE9/7419)
从上图中可以看出基本数据类型保存的是值，而引用数据类型保存的是指向对象的地址信息，不是值
<!-- more -->
# 变量赋值
```java
    num=20;
    str="java";
```
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/6CDFFFA7D06D4EDEB7B53FE4CD00290D/7433 )
对于基本数据类型，如果赋值会覆盖掉原来的数，而对于引用数据类型，重新赋值的话，会覆盖原本保存的地址信息，而去指向新的对象，原来对象没有改变过，此时原来的对象则会因没有引用来关联找不到它，就会被垃圾回收器回收。
# 函数传参
```java
    StringBuilder sb1 = new StringBuilder("test");
    StringBuilder sb2 = new StringBuilder("test");

    // 对于提供修改自身的成员方法引用类型，原始的sBuilder会被更改
    public void func(StringBuilder sBuilder) {
        sBuilder.append("aa");
    }

    // 原始的sBuilder不会被更改
    public void test(StringBuilder sBuilder) {
       
        sBuilder = new StringBuilder("111");
    }
    public static void main(String s){
        func(sb1);
        test(sb2);
    }
```
在执行 main 里面的 &ensp;func(sb1)&ensp;之后
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/F485D582DB9B40D2A9FBC6429C38459D/7467)
执行 main 里面的 test(sb2) 后
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/BC24DEA624EC4DE181C7BF860BB1C82E/7483)
