---
title: Collections 工具类
date: 2020-01-16 15:49:00
tags: 
categories: java
copyright: true
---
# 概述
- 专门用来操作集合的工具类
    - 构造方法私有，禁止创建对象
    -  提供一系列静态方法实现对各种集合的操作
    -   具体操作：搜索、复制、排序、线程安全化等
<!--more-->
   
# 常用方法
> 以下方法都是静态方法。
- void sort(List) //对 List 容器内的元素排序，排序的规则是按照升序进行排序。
- void shuffle(List) //对 List 容器内的元素进行随机排列。
- void reverse(List) //对 List 容器内的元素进行逆序排列.
- void fill(List, Object) //用一个特定的对象重写整个 List 容器。
- int binarySearch(List, Obect)//对于顺序的 List 容器。采用折半直找的方法查找特定对象。

示例代码：  
```
        List<String>  list  = new ArrayList<>();
		for(int i=0;i<10;i++){
			list.add("wang:"+i);
		}
		System.out.println(list);
		
		Collections.shuffle(list);	//随机排列list中的元素
		System.out.println(list);
		
		Collections.reverse(list); //逆序排列
		System.out.println(list);
		
		Collections.sort(list);		//按照递增的方式排序。自定义的类使用：Comparable接口。
		System.out.println(list);
		
		System.out.println(Collections.binarySearch(list, "wang:1")); 	//二分法查找，或者：折半查找，查到返回下标索引，否则返回负数
		
```
结果：  
```
[wang:0, wang:1, wang:2, wang:3, wang:4, wang:5, wang:6, wang:7, wang:8, wang:9]
[wang:5, wang:2, wang:6, wang:7, wang:4, wang:9, wang:0, wang:3, wang:1, wang:8]
[wang:8, wang:1, wang:3, wang:0, wang:9, wang:4, wang:7, wang:6, wang:2, wang:5]
[wang:0, wang:1, wang:2, wang:3, wang:4, wang:5, wang:6, wang:7, wang:8, wang:9]
1
```
