---
title: Set 集合
date: 2020-01-16 15:50:00
tags: 
categories: java
copyright: true
---
# 概述
Set 接口继承自 Collection 。Set 接口中没有新增方法,方法和 Collection 保持完全一致。 在 List 学习的方法,在 Set 中仍然适用。
<!--more-->
# 特点
无序、不可重复。无序指 Set 中的元素没有索引。我们只能遍历查找；不可重复指不允许加入重复的元素，更确切地讲,新元素如果和 Set 中某个元素通过 equals() 方法对比为 true , 则不能加入;甚至，Set 中也只能放入一个 null 元素,不能多个。  

Set 常用的实现类有: HashSet. TreeSet等 。我们一般使用 HashSet .
# HashSet
## 使用
```
        Set<String> s = new HashSet<>();
		s.add("hello");
		s.add("world");
		System.out.println(s);
		s.add("hello");//相同的元素不会加入
		System.out.println(s);
		s.add(null);
		System.out.println(s);
		s.add(null);
		System.out.println(s);
```
结果
```
[world, hello]
[world, hello]
[null, world, hello]
[null, world, hello]
```
## 底层
HashSet 是采用哈希算法实现，底层实际用来 HashMap 实现的，其实 HashSet 本质就是一个简化版的 HashMap，因此查询和增删效率都比较高，我们看看源码：  
```
public class HashSet<E>
    extends AbstractSet<E>
    implements Set<E>, Cloneable, java.io.Serializable{
    ......
    private transient HashMap<E,Object> map;

    private static final Object PRESENT = new Object();

    public HashSet() {
        map = new HashMap<>();
    }
    public boolean add(E e) {
        return map.put(e, PRESENT)==null;
    }
    ......
}
```
可以发现里面有个 map 属性，再看看 add() 方法，发现说白了就是在 map 中增加一个键值对，键就是这个元素，值对象是名为 PRESENT 的 Object 对象固定好的。
# TreeSet
用法和 HashSet 差不多。只是这个有排序。
## 底层
**TreeSet 底层实际是用 TreeMap 实现的，内部维持了一个简化版的 TreeMap ，通过 key 来存儲 Set 的元素**。TreeSet内部需要対存儲的元素迸行排序，因此,我們对应的类需要实现 Comparable 接口。这样，オ能根据 compareTo() 方法比較対象之同的大小。オ能迸行内排序。  

源码如下：  
```
public class TreeSet<E> extends AbstractSet<E>
    implements NavigableSet<E>, Cloneable, java.io.Serializable
{
    private transient NavigableMap<E,Object> m;

    private static final Object PRESENT = new Object();

    TreeSet(NavigableMap<E,Object> m) {
        this.m = m;
    }

    public TreeSet() {
        this(new TreeMap<E,Object>());
    }
    ......    
}
```
里面其中一个成员 m 类型是 NavigableMap ，这是一个接口，其中 TreeMap 实现了这个接口，从构造函数可以看出它在生成的时候，马上 new 了 TreeMap 。
## Comparable 的使用
和 TreeMap 的用法一样，通过实现 Comparable 接口进行排序。  

假设我们要对一个 Employee 类排序，先依照里面的 salary 大小，在依照 id 排序，代码如下：  
```
// 这里接口中的泛型就是自定义的类，比较要跟自己同类比较
class Employee  implements Comparable<Employee>  {
	int id;
	String name;
	double salary;
	
	public Employee(int id, String name, double salary) {
		super();
		this.id = id;
		this.name = name;
		this.salary = salary;
	}

	@Override
	public String toString() {
		return  "id:"+id+",name:"+name+",salary:"+salary;
	}
	//这里就实现了用于比较自定义类大小的方法
	@Override
	public int compareTo(Employee o) {		//负数：小于，0：等于，正数：大于
		
		if(this.salary>o.salary){
			return 1;
		}else if(this.salary<o.salary){
			return -1;
		}else{
			if(this.id>o.id){
				return 1;
			}else if(this.id<o.id){
				return -1;
			}else{
				return 0;
			}
		}
		
	}
}
```
