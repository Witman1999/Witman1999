---
title: IO流
date: 2019-08-16 15:11:33
tags: IO
categories: java
copyright: true
---
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/15BBC074A3674B2DA00E438C8B2209D0/8686.jpeg)
> 我们对文件的操作，大多都是通过 IO 流来操作的，那什么是流呢？  
<!-- more -->
# 一 流
和水流类似，它只是变成了一组有顺序，连续字节的数据流，并且有开始和结束的位置，并且它的方向很重要。透明通常利用方向来区别它们的作用。
## 分类
- 根据流向分为：输入流和输出流
    - 输入流：数据源（磁盘）---> 内存
    - 输出流：内存---> 媒介 （磁盘等）
- 根据类型分为：字符流和字节流
    - 字节流：以字节为单位的进行读写，一次是8为二进制。
    - 字符流：以字符为单位进行读写。一次是16为二进制。
## 使用环境

# 字节流
## 输入字节流 InputStream
- <font color=red>InputStream 是所有输入字节流的父类，他是一个抽象类</font>
- <font color=red>ByteArrayInputStream、StringBufferInputStream、FileInputStream</font> 是三种基本的介质流，它们分别从<font color=red>Byte 数组、StringBuffer、和本地文件中读取数据</font>。

### FileInputStream
#### 概念
FileInputStream流被称为文件字节输入流，意思指对文件数据以字节的形式进行读取操作如读取图片视频等
#### 构造方法
**<font color=blue>第一种：</font>**  
通过打开与File类对象代表的实际文件的链接来创建FileInputStream流对象
```java
public FileInputStream(File file) throws FileNotFoundException{}
```
**<font color=red>注意：</font>**  
**<font color=red>若File类对象的所代表的文件不存在;不是文件是目录;或者其他原因不能打开的话，则会抛出FileNotFoundException</font>**  
**<font color=blue>第二种：</font>**   
通过指定的字符串参数来创建File类对象，而后再与File对象所代表的实际路径建立链接创建FileInputStream流对象,发现该构造方法等于是在第一个构造方法的基础上进行延伸的，因此规则也和第一个构造方法一致
```java
public FileInputStream(String name) throws FileNotFoundException
```
#### 常用方法 
##### read()
>数据的下一个字节（或者指定的长度），如果达到文件的末尾， -1 
```java
            FileInputStream fin= new FileInputStream(file);
			//建立一个字节数组来保存读取的内容
			byte[] by=new byte[1024];
			//保存当前读取的长度
			int size= 0;
			while((size=fin.read(by))!=-1) {
				System.out.println(new String(by,0,size));
			}
			fin.close();
```
## 输出字节流 OutputStream
- <font color=red>OutputStream 是所有的输出字节流的父类，它是一个抽象类。</font>
- <font color=red>ByteArrayOutputStream、FileOutputStream</font> 是两种基本的介质流，它们分别从<font color=red>Byte 数组、和本地文件中读取数据</font>。
### FileOutputStream
FileOutputStream流是指文件字节输出流，专用于输出原始字节流如图像数据等，其继承OutputStream类，拥有输出流的基本特性
```java
public class FileOutputStream extends OutputStream{}
```
#### 构造函数
**<font color=blue>第一种：</font>**   
创建FileOutputStream流以写入数据到File对象所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)
```java
public FileOutputStream(File file) throws FileNotFoundException{}
```
**<font color=blue>第二种：</font>**   
创建FileOutputStream流以写入数据到File对象表示的文件。 <font color=red>如果第二个参数为true，则字节将写入文件的末尾而不是开头。</font> 创建一个新的FileDescriptor对象来表示此文件连接。其抛异常的规则与第一个构造函数一致
```java
public FileOutputStream(File file,boolean append) throws FileNotFoundException{}
```
若第二个参数为真，则意味着会写入字节到文件的末尾，意味着追加内容，若为假，则是写入字节到文件的开头，意味着是覆盖。（默认是覆盖）  
**<font color=blue>第三种：</font>**   
创建FileOutputStream流以写入数据到指定路径所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)
```java
public FileOutputStream(String name) throws FileNotFoundException{}
```
**<font color=blue>第四种：</font>**  
创建FileOutputStream流以写入数据到指定路径所代表的文件，同时创建一个新的FileDescriptor对象来表示与该文件的关联(源码中会new一个该对象)， 如果第二个参数为true，则字节将写入文件的末尾而不是开头
```java
public FileOutputStream(String name,boolean append) throws FileNotFoundException
```
**<font color=red>注意：</font>**  
1. <font color=red> **若文件存在，但是是目录而不是文件，则会抛出FileNotFoundException异常**</font>
2. <font color=red> **若文件不存在则创建**</font>
3.  <font color=red> **若不存在且无法创建，则会抛出FileNotFoundException异常**</font>
#### 常用方法
##### write()
```java
            FileInputStream fin= new FileInputStream(file);
			FileOutputStream fout=new FileOutputStream("picture2.png");
			//建立一个字节数组来保存读取的内容
			byte[] by=new byte[1024];
			//保存当前读取的长度
			int size= 0;
			while((size=fin.read(by))!=-1) {
				fout.write(by, 0, size);
				fout.flush();//刷流
			}
			fout.close();
			fin.close();
```
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
## 输出字符流 Writer
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

