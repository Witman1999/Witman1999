---
title: Map集合
date: 2019-08-16 15:42:00
tags: Map
categories: java
copyright: true
---
# 概述
> 对比 Collection 中的集合，Map 集合中的元素是成对存在，每个元素由键与值两部分组成，通过键找到所对应的值。    

注意的是：<font color=red>Map 集合中不能包含重复的键，值可以重复；每个键对应一个值。</font>

# 常用集合
>Map 中常用的集合为 HashMap 集合，LinkedHashMap 集合。
<!-- more -->
## HashMap<K,V>
>存储数据采用的哈希表结构，所以是无序的，并且为了键的唯一性，不重复，需要重写键的 hashCode() 方法，equals() 方法
- 概述
    - 他是一个散列表，对比Collection 的单列集合，它是一个双列集合。存储内容是键值对（key-value）一对一的关系映射。 并且线程是不同步的，可以存入 null 键，null 值。
### HashMap 与 Hashtable 的区别
1. <font color=red> Hashtable 是一个线程安全的 Map 实现， 但是 HashMap 是线程不安全的实现（底层都是哈希表数据结构），所以 HashMap 比 Hashtable 的性能好一些</font>，但是多个线程访问同一个 Map 对象时，使用 Hashtable 会好一些
2. <font color=red>Hashtable 不也许使用 null 键作为 key 和 value </font>,如果把 null 值放入 Hashtabke 中，将会引发 NullPoiniterException 异常，但是<font color=red> HashMap 可以使用 null 作为 key 或 value</font>。
### 为什么 Key 值需要重写 hashCode() 和 equals()
在添加元素，HashMap 的判断步骤  
1. 首先会使用当前集合中的每个元素和新添加的元素进行 hash 值比较
2. 如果 hash 值不一样，则添加新的元素
3. 如果 hash 值一样，比较地址值或者使用 equals() 方法进行比较
4. 比较结果一样，则认为重复不添加
5. 所有的比较结果都不一样则添加
```java
        Student stu1= new Student("张三", "10000", 18, "男", "软件工程", 1000.00);
		Student stu2= new Student("张三", "10000", 18, "男", "软件工程", 1000.00);
		HashMap<Student, String> map= new HashMap<>();
		map.put(stu1, "我是第一个");
		map.put(stu2, "我是第二个");
		
		System.out.println(map.get(stu1));
		System.out.println(map.get(stu2));
```
以上代码结果为
```
我是第一个
我是第二个
```
明明是同样的数据，可是为什么添加进去了呢，因为，<font color=red>Object 的 hashcode() 方法是通过对象的地址计算出哈希值，所以不同的对象，地址不同也就添加进去了（equals()也是一样）</font>，为了区分不同所以得重写 hashCode() 和 equals() ,因为 equals() 在 hashCode() 相同的情况下（<font color=red>毕竟 hash 值也是会发生冲突的</font>）通过 equals() 判断 key 特有的 ID 值来区别不同。  
**<font color=blue>建议：</font>**  
- 尝试让 hashCode 方法的返回值和对象的成员变量有关
- 可以让 hashCode 方法返回所有成员变量之和。
- 让基本数据类型直接相加，然后引用数据类型获取 hashCode 方法返回值后再相加（boolean 不可参与运算）

### 遍历方式
1. **遍历 HashMap 的键值对**
    1. 根据entrySet()获取 HashMap 的“键值对”的 Set 的集合
    2. 通过 Iterator 迭代器遍历第一步得到的集合  
```java
		//Entry 相当于就是 Map 中的每个 key-value 只保存下来的单个记录点
		//每个 Entry 就保存一个 key 以及它所对应的 value 。Set是集合
		Set<Entry<String, Student>> keys = map.entrySet();
		Iterator<Entry<String, Student>> iterator= keys.iterator();
		//当下一个有值时
		while(iterator.hasNext()) {
			//读取单个的 Entry 对象
			Entry<String, Student> key=iterator.next();
			System.out.println(key.getKey());
			System.out.println(key.getValue().toString());
		}
```
2. **遍历 HashMap 的键**
    1. 根据keySet()获取HashMap的“键”的Set集合。
    2. 通过 Iterator 迭代器遍历第一步得到的集合
```java
        Set<String> keys=map.keySet();
		Iterator<String> iterator= keys.iterator();
		//当下一个有值时
		while(iterator.hasNext()) {
			String key=iterator.next();
			Student value=map.get(key);
			System.out.println(value);
		}
```
3. **遍历 HashMap 的值**
    1. 根据value()获取HashMap的“值”的集合。
    2. 通过 Iterator 迭代器遍历第一步得到的集合
```java
        //只能获取值，不能获取键
        Collection<Student> values = map.values();
		 Iterator<Student> iterator = values.iterator();
		//当下一个有值时
		 while(iterator.hasNext()) {
			 Student value = iterator.next();
			System.out.println(value.toString());
		}
```
### 内部结构
#### HashMap 构造函数
```java
// 默认构造函数。
HashMap()

// 指定“容量大小”的构造函数
HashMap(int capacity)

// 指定“容量大小”和“加载因子”的构造函数
HashMap(int capacity, float loadFactor)

// 包含“子Map”的构造函数
HashMap(Map<? extends K, ? extends V> map)
```
#### 概括
> HashMap 是通过“拉链法”实现的哈希表。它包括 table,size,threshold,loadFactor
1. **table**
    - 是一个 Node[] 数组类型，而 Node 实际就是一个单项链表。数组用来存放 一个Node的头节点（理解为key 的 hashCode() ）的值，以便插入先利用 hashCode 寻址。
2. **size**
    - HashMap的大小，它是HashMap保存的键值对的数量。
3. **threshold**
    - threshold是HashMap的阈值，用于判断是否需要调整HashMap的容量。threshold的值="容量*加载因子"，当HashMap中存储数据的数量达到threshold时，就需要将HashMap的容量加倍。
4. **loadFactor**
    - 加载因子  
    

Node 节点源代码
```java
static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;
        final K key;
        V value;
        // 指向下一个节点
        Node<K,V> next;
        //构造函数。
      // 输入参数包括"哈希值(hash)", "键(key)", "值(value)", "下一节点(next)"
        Node(int hash, K key, V value, Node<K,V> next) {
            this.hash = hash;
            this.key = key;
            this.value = value;
            this.next = next;
        }

        public final K getKey()        { return key; }
        public final V getValue()      { return value; }
        public final String toString() { return key + "=" + value; }

        public final int hashCode() {
            return Objects.hashCode(key) ^ Objects.hashCode(value);
        }

        public final V setValue(V newValue) {
            V oldValue = value;
            value = newValue;
            return oldValue;
        }
         // 判断两个Node是否相等
        // 若两个Node的“key”和“value”都相等，则返回true。
        // 否则，返回false
        public final boolean equals(Object o) {
            if (o == this)
                return true;
            if (o instanceof Map.Entry) {
                Map.Entry<?,?> e = (Map.Entry<?,?>)o;
                if (Objects.equals(key, e.getKey()) &&
                    Objects.equals(value, e.getValue()))
                    return true;
            }
            return false;
        }
    }
```

HashMap 的哈希表，就是存储这数组和链表两种结构。数组的特点就是连续空间，寻址速度，但是删除或增加困难，链表则是正好相反，由于空间的不连续，查找速度慢，但增加删除只需要改指针，速度块。这种叫做“拉链法”。
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/306A1E3FD5554C3BB5340FF6DCC45F28/8644)  
图中，我们可以发现哈希表是由数组+链表組成的，一个长度为16的数组中，每個元素存储的是一个链表的头结点。
一般情況是通过hash(key)获得，也就是元素的key的哈希值。如果hash(key)值相等，则都存入该hash值所对应的链表中。它的內部其实是用一個Node数组來实现。
## LinkedHashMap
>LinkedHashMap使用双向链表来维护key-value对的次序。
LinkedHashMap 的性能略低于HashMap的性能，因为要拍顺序；但由于它以链表，所以在迭代访问Map里的全部元素时有较好速度。迭代输出LinkedHashMap的元素时，将会按照添加key-value对的顺序输出。

**本质上来讲，LinkedHashMap=散列表+循环双向链表**

## TreeMap

>TreeMap是SortedMap接口的实现类。TreeMap 是一个有序的key-value集合，它是通过红黑树实现的，每个key-value对即作为红黑树的一个节点。

