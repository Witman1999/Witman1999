---
title: IO流
date: 2019-08-16 15:11:33
tags: IO
categories: java
copyright: true
---
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/E18D58A2FCC3400694C5B3F0A83CD572/16310)
> 我们对文件的操作，大多都是通过 IO 流来操作的，那什么是流呢？  

# 一 流
和水流类似，它只是变成了一组有顺序，连续字节的数据流，并且有开始和结束的位置，并且它的方向很重要。透明通常利用方向来区别它们的作用。
## 分类
- 根据流向分为：输入流和输出流
    - 输入流：数据源（磁盘）---> 内存
    - 输出流：内存---> 媒介 （磁盘等）
- 根据类型分为：字符流和字节流
    - 字节流：以字节为单位的进行读写，一次是8为二进制。
    - 字符流：以字符为单位进行读写。一次是16为二进制。
    - 关系
        - 底层还是使用了字节流
- 按功能分为：节点流和处理流
    - 节点流：可以直接从数据源或目的地读写数据
    - 处理流（包装流）：不直接连接到数据源或目的地，是其他流进行封装。目的主要是简化操作和提高性能。
    - 关系
        - 节点流处于 IO 操作的第一线，所有操作必须通过他们进行；
        - 处理流可以对其他流进行处理（提高效率或操作灵活性）

# 字节流
## 输入字节流 InputStream
- InputStream 是所有输入字节流的父类，他是一个抽象类
- ByteArrayInputStream、StringBufferInputStream、FileInputStream 是三种基本的介质流，它们分别从Byte 数组、StringBuffer、和本地文件中读取数据。

### FileInputStream
#### 概念
通过字节的
方式读取文件，适合读取所有
类型的文件(图像、视频等)，
全字符请考虑 FileReader
#### 构造方法
**第一种：**  
通过打开与File类对象代表的实际文件的链接来创建FileInputStream流对象
```java
public FileInputStream(File file) throws FileNotFoundException{}
```
**注意：**  
**若File类对象的所代表的文件不存在;不是文件是目录;或者其他原因不能打开的话，则会抛出 FileNotFoundException**  
**第二种：**   
通过指定的字符串参数来创建File类对象，而后再与File对象所代表的实际路径建立链接创建FileInputStream流对象,发现该构造方法等于是在第一个构造方法的基础上进行延伸的，因此规则也和第一个构造方法一致
```java
public FileInputStream(String name) throws FileNotFoundException
```
#### 常用方法 
##### read(byte[])
>读取数据到指定的字节数组，并且返回此时读取到的长度，如果达到文件的末尾返回 -1   

读取数据的时候我们分为 4 步骤
1. 创建源
2. 选择流
3. 操作
4. 释放资源

示例代码如下：  
```java
            //1. 创建源
            File file = new File("test.txt");
            //2. 选择流
            FileInputStream is= new FileInputStream(file);
            //3. 操作（读取数据）
			//建立一个字节数组来保存读取的内容
			byte[] flush=new byte[1024];
			//保存当前读取的长度
			int size= 0;
			while((size=is.read(flush))!=-1) {
			    //字节数组 -> 字符串（解码）
				System.out.println(new String(flush,0,size));
			}
			//4. 释放资源
			is.close();
```
### ByteArrayInputStream
#### 概念
字节数组输入流,在内存中创建了一个字节数组,将输入流中读取的数据保存到字节数组的缓存区中.也就是说字节数组输入流将读取数据放到字节数组缓冲区中
#### 构造方法
**第一种：**  
通过打开与File类对象代表的实际文件的链接来创建FileInputStream流对象
```java
public FileInputStream(File file) throws FileNotFoundException{}
```
**注意：**  
**若File类对象的所代表的文件不存在;不是文件是目录;或者其他原因不能打开的话，则会抛出 FileNotFoundException**  
**第二种：**   
通过指定的字符串参数来创建File类对象，而后再与File对象所代表的实际路径建立链接创建FileInputStream流对象,发现该构造方法等于是在第一个构造方法的基础上进行延伸的，因此规则也和第一个构造方法一致
```java
public FileInputStream(String name) throws FileNotFoundException
```
#### 常用方法 
##### read(byte[])
>读取数据到指定的字节数组，并且返回此时读取到的长度，如果达到文件的末尾返回 -1   

读取数据的时候我们分为 4 步骤
1. 创建源：字节数组，不要太大
2. 选择流
3. 操作
4. 释放资源：可以不用处理

示例代码如下：  
```java
            //1. 创建源
            File file = new File("test.txt");
            //2. 选择流
            FileInputStream is= new FileInputStream(file);
            //3. 操作（读取数据）
			//建立一个字节数组来保存读取的内容
			byte[] flush=new byte[1024];
			//保存当前读取的长度
			int size= 0;
			while((size=is.read(flush))!=-1) {
			    //字节数组 -> 字符串（解码）
				System.out.println(new String(flush,0,size));
			}
			//4. 释放资源
			is.close();
```
### DataInputStream
将基础的输入流，原始的数据类型w写入文件

## 输出字节流 OutputStream
- OutputStream 是所有的输出字节流的父类，它是一个抽象类。
- ByteArrayOutputStream、FileOutputStream 是两种基本的介质流，它们分别从 Byte 数组、和本地文件中读取数据。
### FileOutputStream
通过字节的方式写出或追加数据到文件，适合所有类型的文件(图像、视频等),全字符请考虑 FileWriter
```java
public class FileOutputStream extends OutputStream{}
```
#### 构造函数
**第一种：**   
创建FileOutputStream流以写入数据到File对象所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)
```java
public FileOutputStream(File file) throws FileNotFoundException{}
```
**第二种：**   
创建FileOutputStream流以写入数据到File对象表示的文件。 如果第二个参数为true，则字节将写入文件的末尾而不是开头。创建一个新的FileDescriptor对象来表示此文件连接。其抛异常的规则与第一个构造函数一致
```java
public FileOutputStream(File file,boolean append) throws FileNotFoundException{}
```
若第二个参数为真，则意味着会写入字节到文件的末尾，意味着追加内容，若为假，则是写入字节到文件的开头，意味着是覆盖。（默认是覆盖）  
**第三种：**   
创建FileOutputStream流以写入数据到指定路径所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)
```java
public FileOutputStream(String name) throws FileNotFoundException{}
```
**第四种：**  
创建FileOutputStream流以写入数据到指定路径所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)， 如果第二个参数为true，则字节将写入文件的末尾而不是开头
```java
public FileOutputStream(String name,boolean append) throws FileNotFoundException
```
**注意：**  
1. <font color=red> **若文件存在，但是是目录而不是文件，则会抛出FileNotFoundException异常**</font>
2. <font color=red> **若文件不存在则创建**</font>
3.  <font color=red> **若不存在且无法创建，则会抛出FileNotFoundException异常**</font>
#### 常用方法
##### write(byte b[], int off, int len)
> 指定一个字节数组 b，然后写入指定的长度  

写入数据的时候我们分为 4 步骤
1. 创建源
2. 选择流
3. 操作
4. 释放资源
```java
        //1、创建源
		File dest = new File("dest.txt");
		//2、选择流
		OutputStream os =null;
		try {
			os = new FileOutputStream(dest,true);
			//3、操作(写出)
			String msg ="IO is so easy";
			byte[] datas =msg.getBytes(); // 字符串-->字节数组(编码)
			os.write(datas,0,datas.length);
			os.flush();
		}catch(FileNotFoundException e) {		
			e.printStackTrace();
		}catch (IOException e) {
			e.printStackTrace();
		}finally{
			//4、释放资源
			try {
				if (null != os) {
					os.close();
				} 
			} catch (Exception e) {
			}
		}
```
### FileOutputStream
通过字节的方式写出或追加数据到文件，适合所有类型的文件(图像、视频等),全字符请考虑 FileWriter
```java
public class FileOutputStream extends OutputStream{}
```
#### 构造函数
**第一种：**   
创建FileOutputStream流以写入数据到File对象所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)
```java
public FileOutputStream(File file) throws FileNotFoundException{}
```
**第二种：**   
创建FileOutputStream流以写入数据到File对象表示的文件。 如果第二个参数为true，则字节将写入文件的末尾而不是开头。创建一个新的FileDescriptor对象来表示此文件连接。其抛异常的规则与第一个构造函数一致
```java
public FileOutputStream(File file,boolean append) throws FileNotFoundException{}
```
若第二个参数为真，则意味着会写入字节到文件的末尾，意味着追加内容，若为假，则是写入字节到文件的开头，意味着是覆盖。（默认是覆盖）  
**第三种：**   
创建FileOutputStream流以写入数据到指定路径所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)
```java
public FileOutputStream(String name) throws FileNotFoundException{}
```
**第四种：**  
创建FileOutputStream流以写入数据到指定路径所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)， 如果第二个参数为true，则字节将写入文件的末尾而不是开头
```java
public FileOutputStream(String name,boolean append) throws FileNotFoundException
```
**注意：**  
1. <font color=red> **若文件存在，但是是目录而不是文件，则会抛出FileNotFoundException异常**</font>
2. <font color=red> **若文件不存在则创建**</font>
3.  <font color=red> **若不存在且无法创建，则会抛出FileNotFoundException异常**</font>
#### 常用方法
##### write(byte b[], int off, int len)
> 指定一个字节数组 b，然后写入指定的长度  

写入数据的时候我们分为 4 步骤
1. 创建源
2. 选择流
3. 操作
4. 释放资源
```java
        //1、创建源
		File dest = new File("dest.txt");
		//2、选择流
		OutputStream os =null;
		try {
			os = new FileOutputStream(dest,true);
			//3、操作(写出)
			String msg ="IO is so easy";
			byte[] datas =msg.getBytes(); // 字符串-->字节数组(编码)
			os.write(datas,0,datas.length);
			os.flush();
		}catch(FileNotFoundException e) {		
			e.printStackTrace();
		}catch (IOException e) {
			e.printStackTrace();
		}finally{
			//4、释放资源
			try {
				if (null != os) {
					os.close();
				} 
			} catch (Exception e) {
			}
		}
```
### ByteArrayOutputStream
对byte类型数据进行写入的类 相当于一个中间缓冲层，将类写入到文件等其他outputStream。它是对字节进行操作，属于内存操作流
```java
public class FileOutputStream extends OutputStream{}
```
#### 构造函数
**第一种：**   
创建FileOutputStream流以写入数据到File对象所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)
```java
public FileOutputStream(File file) throws FileNotFoundException{}
```
**第二种：**   
创建FileOutputStream流以写入数据到File对象表示的文件。 如果第二个参数为true，则字节将写入文件的末尾而不是开头。创建一个新的FileDescriptor对象来表示此文件连接。其抛异常的规则与第一个构造函数一致
```java
public FileOutputStream(File file,boolean append) throws FileNotFoundException{}
```
若第二个参数为真，则意味着会写入字节到文件的末尾，意味着追加内容，若为假，则是写入字节到文件的开头，意味着是覆盖。（默认是覆盖）  
**第三种：**   
创建FileOutputStream流以写入数据到指定路径所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)
```java
public FileOutputStream(String name) throws FileNotFoundException{}
```
**第四种：**  
创建FileOutputStream流以写入数据到指定路径所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)， 如果第二个参数为true，则字节将写入文件的末尾而不是开头
```java
public FileOutputStream(String name,boolean append) throws FileNotFoundException
```
**注意：**  
1. <font color=red> **若文件存在，但是是目录而不是文件，则会抛出FileNotFoundException异常**</font>
2. <font color=red> **若文件不存在则创建**</font>
3.  <font color=red> **若不存在且无法创建，则会抛出FileNotFoundException异常**</font>
#### 常用方法
##### write(byte b[], int off, int len)
> 指定一个字节数组 b，然后写入指定的长度  

写入数据的时候我们分为 4 步骤
1. 创建源：内部维护
2. 选择流：不关联源
3. 操作：
4. 释放资源：可以不用
5. 获取数据 toByteArray();

```java
        //1、创建源
		File dest = new File("dest.txt");
		//2、选择流
		OutputStream os =null;
		try {
			os = new FileOutputStream(dest,true);
			//3、操作(写出)
			String msg ="IO is so easy";
			byte[] datas =msg.getBytes(); // 字符串-->字节数组(编码)
			os.write(datas,0,datas.length);
			os.flush();
		}catch(FileNotFoundException e) {		
			e.printStackTrace();
		}catch (IOException e) {
			e.printStackTrace();
		}finally{
			//4、释放资源
			try {
				if (null != os) {
					os.close();
				} 
			} catch (Exception e) {
			}
		}
```


## try - catch - resource
## DataOutputStream

# 字符流
## 输入字符流 Reader
- <font color=red>Reader 是所有输入字符流的父类，他是一个抽象类</font>
### BufferedReader
BufferedReader类从字符输入流中读取文本并缓冲字符，以便有效地读取字符，数组和行
可以通过构造函数指定缓冲区大小也可以使用默认大小。对于大多数用途，默认值足够大
#### 构造函数
```java
BufferedReader(Reader in) 
```
和上面的输入流类似，new出新对象的时候需要传入Reader的子类流，如下
```java
bufferRead = new BufferedReader(new InputStreamReader(new FileInputStream(path)));
```
#### 常用的方法
##### readLine()
```java
        bufferRead = new BufferedReader(new InputStreamReader(new FileInputStream(path)));
        String result;
		while ((result = bufferRead.readLine()) != null) {
				System.out.println(result);
			}
		}
```
### InputStreamReader
InputStreamReader类是从字节流到字符流的桥接器：它使用指定的字符集读取字节并将它们解码为字符。 它使用的字符集可以通过名称指定，也可以明确指定，或者可以接受平台的默认字符集。每次调用一个InputStreamReader的read（）方法都可能导致从底层字节输入流中读取一个或多个字节。 为了实现字节到字符的有效转换，可以从基础流中提取比满足当前读取操作所需的更多字节。
## 输出字 符流 Writer
- <font color=red>Writer 是所有输出字符流的父类，他是一个抽象类</font>
### BufferedWriter
字符缓冲输出流
#### 构造函数
```java
            BufferedWriter(Wtiert in) ;
```
和上面的输入流类似，new出新对象的时候需要传入Writer的子类流，如下
```java
		bufferWriter = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(path, true)));
```
#### 常用方法
##### writer()
```java
        bufferWriter = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(path, true)));
        String result="hello world";
        bufferWriter.write(result);
		}
```
##### nextLine()
> public void newLine() throws IOException
写入一个行分隔符。


