---
title: List集合
date: 2019-08-16 15:38:00
tags: List
categories: java
copyright: true
---
>有序集合，可以存放重复的元素；
# 实现类
## ArrayList
>数组实现，查询块，增删慢，轻量级。（线程不安全）  

底层是 Object 数组，动态的，通过判断大小是否超过来 copy 数组，并且重新赋予新的空间。能够拥有数组的查找速度快的特点，但是，也造成了增删慢的缺点。
<!-- more -->
### 遍历方式
**（01）第一种，迭代器**
```java
Integer value = null;
Iterator iter = list.iterator();
while (iter.hasNext()) {
    value = (Integer)iter.next();
}
```
**（02）第二种，索引值访问**
```java
Integer value = null;
int size = list.size();
for (int i=0; i<size; i++) {
    value = (Integer)list.get(i);        
}
```
**（03）增强 for 遍历**
```java
Integer value = null;
for (Integer integ:list) {
    value = integ;
}
```
**<font color=red>注意：</font>**  
使用索引值访问效率最高，而迭代器最低
## LinkedList
>双向链表实现，增删块，查询慢（线程不安全）
底层是一个双向循环链表，所以在插入和删除上会更好，但是对比 ArrayList ,随机访问也就是查询性能差。
### 遍历方式
1. 通过迭代器
2. 随机访问
3. 增强 for 循环
4. 通过 pollFirst() 
5. 通过 pollLast()
6. 通过 removeFirst()
7. 通过 removeLast()

**<font color=red>注意：</font>**    
逐个遍历，效率最高，随机访问效率最低。    
LinkedList() 可以用来实现栈（stack），队列（queue），双向队列，因为它具有 addFirst(), getFirst(),getLast(),removeFirst(),removeLast()等。
## Vector
>数组实现，重量级（线程安全，使用少）

和 ArrayList   相似在考虑的清空下使用 Vector ( 保证线程安全 )
## 总结 
对于“单线程环境”或者“多线程环境，但 List 仅仅只会被单个线程操作“，此时应该使用非同步类（如 ArrayList ）,对于多线程环境，且 list 可能同时被多个线程操作，此时应该使用同步的类（如 Vector ）

