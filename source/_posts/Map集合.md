---
title: Map集合
date: 2019-08-16 15:42:00
tags: Map
categories: java
copyright: true
---
# 概述
在现实生活中，我们要存储某些信息的时候，比如，我们使用的微信就是一个手机号对应一个微信账户，这是一种成对的存储关系。  
Map 就是用来存储“键（key） 值（value）”对的。通过键识别，所以键对象不能重复。
> 对比 Collection 中的集合，Map 集合中的元素是成对存在，每个元素由键与值两部分组成，通过键找到所对应的值。    

注意的是：**Map 集合中不能包含重复的键，值可以重复；每个键对应一个值。（如果重复了键将会覆盖旧的值，重复是根据 equals 方法判断）**
<!--more-->
# 常用类
Map 中常用的子类为 HashMap ，HashTable，TreeMap等。
## HashMap<K,V>
>存储数据采用的哈希表结构，所以是无序的，并且为了键的唯一性，不重复，需要重写键的 hashCode() 方法，equals() 方法
- 概述
    - 他是一个散列表，对比Collection 的单列集合，它是一个双列集合。存储内容是键值对（key-value）一对一的关系映射。 并且线程是不同步的，可以存入 null 键，null 值。
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
### 底层
**HashMap** 底层实现采用了哈希表，哈希表的基本结构就是数组加链表。我们打开 **HashMap** 源码，发现以下两个内容：  
```
public class HashMap<K,V> extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable {

    private static final long serialVersionUID = 362498820763181265L;

    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16

    static final int MAXIMUM_CAPACITY = 1 << 30;

    static final float DEFAULT_LOAD_FACTOR = 0.75f;

    static final int TREEIFY_THRESHOLD = 8;

    static final int UNTREEIFY_THRESHOLD = 6;

    static final int MIN_TREEIFY_CAPACITY = 64;

    transient Node<K,V>[] table;
    ......
}
```
其中 **Node[ ] table** 就是 **HashMap** 的核心数组结构，也称为 “**位桶数组**” ，我们在看看 **Node** 的源码看看  
```
 static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;//哈希值
        final K key;
        V value;
        Node<K,V> next;//下一个结点

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
**一个 Node 对象存储了：**  
- **key**：键对象 
- **value**：值对象
- **next**：下一个结点
- **hash**：键对象的哈希值

显然每个 **Node** 对象，代表一条单向链表，示意图如下：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/16FFDA56C5324B2B8DC4DD2D72F732EC/15045)   
因此我们也得出，整个 **Node[ ]** 数组的结构（也就是 **HashMap** ）结构如图：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/0BA3D89403444419A8C12760E9A5F291/15052)   
#### 存储数据过程 put(key,value)
此处的核心就是产生 hash 值，该值对应数组的存储位置。如下图：（其中数组默认大小为 16）  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/E9FFB6C80A64400699E6817B4E4725B1/15062)  
**步骤如下：**  
1. **获得 key 对象的 hashcode**
    - 首先调用 key 对象的 hashcode（） 方法，获得 hashcode 
2. **根据 hashcode 计算出 hash 值（要求在[0,数组长度-1]区间）**
    - hashcode 是一个整数，我们需要把他转化为 [0,数组长度-1] 之间，我们要求转换后的 hash 值尽量的均匀分布在 [0,数组长度-1] 这个区间，减少 “hash” 冲突
    
3. **简单的 hash 算法**
    - 一种是 hash = hash % 数组长度 ，但是由于除法低效，还有以下算法
    - 还有一种是 hash = hash & （数组长度 - 1） 前提是数组的长度是 2 的整数幂
    - 示例代码
    ```
    public class TestMap {
	public static void main(String[] args) {
		int h = 25860399;
		int length = 16;//length 为 2 的整数幂，h & （length-1）相当于对 length 取模
		myHash(h,length);
	}

	private static int myHash(int h,int length) {
		// TODO Auto-generated method stub
		System.out.println(h&(length-1));
		System.out.println(h%length);
		return h&(length-1);
	}

    ```

在上述程序，其实发现取余和位运算结果都是一样的，事实是为了获得更好的散列效果。JDK 对 hashcode 进行了两次散列处理  
4. **生产 Node 对象**
5. **将 Node 对象放到 table 数组中** 
    - 如果本 Node 对象的数组索引还没有 Node 对象，则直接将 Node 对象放进数组，否则，则将已有的 Node 对象的 next 指向本 Node 对象，形成链表。
##### 总结上述过程
 当添加一个元素 (key-value) 时，首先计算 key 的 hash 值,以此确定插入数组中的位置,但是可能存在同一 hash 值的元素已经被放在数同一位置了,这时就添加到同一 hash 值的元素的后面,他们在数组的同一位置,就形成了链表,同-一个链表上的Hash值是相同的,所以说数组存放的是链表。**注意：（JDK8中,当链表长度大于8时,链表就转换为红黑树,这样又大大提高了查找的效率。）**
#### 取数据的过程 get（key）
从存储的过程，我们很容易的退出取数据的过程，如下：
1. **获得 key 的 hashcode ，通过 hash() 散列算法得到 hash 值，进而定位到数组的位置**
2. **在链表上挨个比较 key 对象，调用 equals（） 方法**，将 key 对象与链表上的所有结点 key 对象比较，直到碰到返回 true 结点对象的 value 的值。
3. **返回 equals（）为 true 的结点的 value 对象**
4. 明白了存取过程，在看一下 **hashcode 和 equals 的关系：**
    - **java 规定，两个内容相同的（equals 为 true）必须具有相等的 hashcode** 
    - 因为如果 equals 为 true 而两个对象的 hashcode 不同，那再整个存储过程会发生二义性。因为 hashcode 是用来寻找 在数组中的位置，如果内容相同，数组下标不同，那将会乱套。


##### 为什么 Key 值需要重写 hashCode() 和 equals()
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
明明是同样的数据，可是为什么添加进去了呢，因为，**Object 的 hashcode() 方法是通过对象的地址计算出哈希值，所以不同的对象，地址不同也就添加进去了（equals()也是一样）**，为了区分不同所以得重写 hashCode() 和 equals() ,因为 equals() 在 hashCode() 相同的情况下（**毕竟 hash 值也是会发生冲突的**）通过 equals() 判断 key 特有的 ID 值来区别不同。  
**建议：**  
- 尝试让 hashCode 方法的返回值和对象的成员变量有关
- 可以让 hashCode 方法返回所有成员变量之和。
- 让基本数据类型直接相加，然后引用数据类型获取 hashCode 方法返回值后再相加（boolean 不可参与运算
### 扩容问题
**HashMap** 的位桶数组，初始大小为16。实际使用时,显然大小是可变的。如果位桶数组中的元素达到(0.75*数组length),就重新调整数组大小变为原来 2 倍大小。    

扩容很耗时。扩容的本质是定义新的更大的数组,并将旧数组内容挨个拷贝到新数组中。
### JDK8 将链表在大于8 情况下变为红黑二叉树
JDK8 中, HashMap 在存储一个元素时 ,当对应链表长度大于 8 时,链表就转换为红黑树,这样又大大提高了查找的效率。

## HashTable
HashTable 和 HashMap 用法几乎一样，底层实现也几乎一样，**只不过 HashTable 的方法添加了 synchronized 关键字确保线程同步检查**，效率较低。
## HashTable 和 HasbMap 的区别
1. HashTable：线程安全，效率低，不也许 key 或 value 为 null。
2. hashMap：线程不安全，效率高，也许 key 或 value 为 null。
## TreeMap
TreeMap 是红黑二叉树的典型实现，我们打开 TreeMap 的源码，发现有一行核心代码：
```
private transient Entry<k,v> root = null
```
root 用来存储整个树的根节点，继续查看 Entry （TreeMap 的内部类） 代码：  
```
 static final class Entry<K,V> implements Map.Entry<K,V> {
        K key;
        V value;
        Entry<K,V> left;
        Entry<K,V> right;
        Entry<K,V> parent;
        boolean color = BLACK;
        ......
        ......
        ......
}
```
明显的看到，存储了本身数据，左节点，右节点，父节点，以及结点颜色。在内部的方法 put() 和 remove() 方法大量采用了红黑树的理论，对于红黑二叉树，这里就不进行深入的讨论，有需要的可以参考数据结构的书籍。  

TreeMap 和 HashMap 都实现了同样的接口 Map ，因此对于调用者来说使用没有区别，HashMap 效率高于 TreeMap ,只是在需要对排序的 Map 才使用 TreeMap 。  

### Comparable 接口
然而在 TreeMap 是怎样进行排序的呢？对于个人自定义的类是 TreeMap 是依照什么依据排序的呢？  

在对于已经定义好的 Integer ，String 等系统类， 他们都有实现 Comparable<E> 接口，然后是实现里面的 ``compareTo(Emp o)``  方法，而对于自定义类，要使得 TreeMap 进行排序，也要实现这个  Comparable<E> 接口。   

假设，我们要对一个 Employee 类排序，先依照里面的 salary 大小，在依照 id 排序，代码如下：  
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

