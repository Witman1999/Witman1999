---
title: 迭代器 Iterator
date: 2020-01-16 15:49:00
tags: 
categories: java
copyright: true
---
# 概述
- 所有集合类均未提供相应的遍历方法，而是把把遍历交给迭代器完成。迭代器为集 合而生，专门实现集合遍历
- Iterator是迭代器设计模式的具体实现
- Iterator方法 
    - boolean hasNext(): 判断是否存在另一个可访问的元素 
    -  Object next(): 返回要访问的下一个元素 
    -  void remove(): 删除上次访问返回的对象。
- 遍历的本质
    - 实现 Iterable 接口
	  
  
<!--more-->
# For-each 循环
## 优点
- 增强的for循环，遍历array 或 Collection的时候相当简便 
- 无需获得集合和数组长度，无需使用索引访问元素，无需循环条件 
- 遍历集合时底层调用Iterator完成操作
- 数组：
    -  不能方便的访问下标值 
    -  不要在for-each中尝试对变量赋值，只是一个临时变量 
- 集合：
    - 与使用Iterator相比，不能方便的删除集合中的内容
  
## 缺点
# 遍历集合用法
## 遍历 List
```
        List list = new ArrayList<>();
		list.add("de");
		list.add("dddd");
		list.add("dfjiow");
		list.add("pp");
		
		Iterator<String> iterator = list.iterator();
		while(iterator.hasNext()) {//判断是否有下一个
			String o =iterator.next();//获取对象
			System.out.println(o);
		}
```
## 遍历 Set
```
        Set list = new HashSet<>();
		list.add("de");
		list.add("dddd");
		list.add("dfjiow");
		list.add("pp");
		
		Iterator<String> iterator = list.iterator();
		while(iterator.hasNext()) {//判断是否有下一个
			String o =iterator.next();//获取对象
			System.out.println(o);
		}
```
## 遍历 Map
- 方法一：使用 entrySet() 方法
```
        Map<Integer,String> map1 = new HashMap<>();
		map1.put(100, "aa");
		map1.put(200, "bb");
		map1.put(300, "cc");
		
		Set<Entry<Integer,String>> s = map1.entrySet();
		Iterator<Entry<Integer,String>> iterator = s.iterator();
		while(iterator.hasNext()) {
			Entry<Integer, String> temp = iterator.next();
			System.out.println(temp.getKey()+"------"+temp.getValue());
		}
```
- 方法二：使用 keySet() 方法
```
        Map<Integer,String> map1 = new HashMap<>();
		map1.put(100, "aa");
		map1.put(200, "bb");
		map1.put(300, "cc");
		
		Set<Integer> s = map1.keySet();
		Iterator<Integer> iterator = s.iterator();
		while(iterator.hasNext()) {
			Integer temp = iterator.next();
			System.out.println(temp+"----------"+map1.get(temp));
		}
```
