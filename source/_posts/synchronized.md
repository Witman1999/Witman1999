---
title: synchronized关键字
date: 2019-08-16 15:45:00
tags: 关键字
categories: java
keywords: synchronized关键字
copyright: true
---
# 一. 概念
（synchronized） java 中的关键字，是利用锁的机制来实现同步的。
## 特性
1. 互斥性：即在同一时间只也许一个线程持有某个对象锁，同一时间只有一个线程对需要同步的代码块进行访问。
2. 必须确保在锁被释放之前，对共享变量所做的修改，对于随后获得该锁的另一个线程是可见的（即在获得锁时应获得最新共享变量的值），否则另一个线程可能是在本地缓存的某个副本上继续操作从而引起不一致。
<!-- more -->
# 二. 对象锁和类锁
## 对象锁
在 Java 中，每个对象都会有一个 monitor 对象，这个对象其实就是 java 对象的锁（内置锁/对象锁），每个对象都有独立的对象锁，互不干扰。
## 类锁
在 Java 中，针对每个类也有一个锁，称为“类锁”，每一个类只有一个 class 对象锁。
# 三 synchronized 的用法
## 根据修饰的对象分类
synchronized 可以修饰方法和代码块
- 修饰代码块
    - synchronized(this.object){}
    - synchronized(类.class)
- 修饰方法
    - 修饰静态方法
    - 修饰非静态方法
## 根据获取的锁分类
- 获取对象锁
    - synchronized(this|object){}
    - 修饰非静态方法
- 获取类锁
    - synchronized(类.class)
    - 修饰非静态方法/静态方法

## 附
```java
//修饰非静态方法
public synchronized void test1() {}
//修饰静态方法
public synchronized static void test() {}
```
# 四. synchronized 例子
### 1. 对象锁
```java
public class SynchorizedThread extends Thread {
    @Override
	public void run() {
		syn5();
	}
	public void syn5() {
		 System.out.println(Thread.currentThread().getName() + "_Sync5: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
		 
	        synchronized (new SynchorizedThread()) {
	            try {
	                System.out.println(Thread.currentThread().getName() + "_Sync5_Start: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	                Thread.sleep(2000);
	                System.out.println(Thread.currentThread().getName() + "_Sync5_End: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	            } catch (InterruptedException e) {
	                e.printStackTrace();
	            }
	        }
	}
}
```
后面所有的例子都是采用这四个线程，只是对方法进行修改
```java
public static void main(String args[]) {
		SynchorizedThread syncThread = new SynchorizedThread();
        Thread F_thread1 = new Thread(new SynchorizedThread(), "F_thread1");
        Thread F_thread2 = new Thread(new SynchorizedThread(), "F_thread2");
        Thread F_thread3 = new Thread(syncThread, "F_thread3");
        Thread F_thread4 = new Thread(syncThread, "F_thread4");
        F_thread1.start();
        F_thread2.start();
        F_thread3.start();
        F_thread4.start();
	}
```
运行结果如下：
```java
F_thread2_Sync5: 08:49:36
F_thread1_Sync5: 08:49:36
F_thread4_Sync5: 08:49:36
F_thread2_Sync5_Start: 08:49:36
F_thread3_Sync5: 08:49:36
F_thread4_Sync5_Start: 08:49:36
F_thread1_Sync5_Start: 08:49:36
F_thread3_Sync5_Start: 08:49:36
F_thread1_Sync5_End: 08:49:38
F_thread3_Sync5_End: 08:49:38
F_thread4_Sync5_End: 08:49:38
F_thread2_Sync5_End: 08:49:38
```
<font color=red>四个线程同时开始，同时结束，因为作为锁的对象与线程是属于不同的实例</font>
### 2. 采用类锁，无论哪个类都会被拦截
```java
public class SynchorizedThread extends Thread {
    @Override
	public void run() {
		syn5();
	}
	public void syn5() {
		 System.out.println(Thread.currentThread().getName() + "_Sync5: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
		 
	        synchronized (test.class) {
	            try {
	                System.out.println(Thread.currentThread().getName() + "_Sync5_Start: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	                Thread.sleep(2000);
	                System.out.println(Thread.currentThread().getName() + "_Sync5_End: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	            } catch (InterruptedException e) {
	                e.printStackTrace();
	            }
	        }
	}
}
```
运行结果如下：
```java
F_thread2_Sync5: 09:26:25
F_thread3_Sync5: 09:26:25
F_thread4_Sync5: 09:26:25
F_thread1_Sync5: 09:26:25
F_thread2_Sync5_Start: 09:26:25
F_thread2_Sync5_End: 09:26:27
F_thread3_Sync5_Start: 09:26:27
F_thread3_Sync5_End: 09:26:29
F_thread4_Sync5_Start: 09:26:29
F_thread4_Sync5_End: 09:26:31
F_thread1_Sync5_Start: 09:26:31
F_thread1_Sync5_End: 09:26:33
```
可以发现，采用类锁一次只能通过一个，即使是不同的类，也只能通过一个。
### 3. 采用 this 对象锁
```java
public class SynchorizedThread extends Thread {
    @Override
	public void run() {
		syn5();
	}
	public void syn5() {
		 System.out.println(Thread.currentThread().getName() + "_Sync5: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
		 
	        synchronized (this) {
	            try {
	                System.out.println(Thread.currentThread().getName() + "_Sync5_Start: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	                Thread.sleep(2000);
	                System.out.println(Thread.currentThread().getName() + "_Sync5_End: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	            } catch (InterruptedException e) {
	                e.printStackTrace();
	            }
	        }
	}
}
```
结果如下：
```java
F_thread2_Sync5: 09:40:29
F_thread1_Sync5: 09:40:29
F_thread4_Sync5: 09:40:29
F_thread1_Sync5_Start: 09:40:29
F_thread3_Sync5: 09:40:29
F_thread2_Sync5_Start: 09:40:29
F_thread4_Sync5_Start: 09:40:29
F_thread1_Sync5_End: 09:40:31
F_thread2_Sync5_End: 09:40:31
F_thread4_Sync5_End: 09:40:31
F_thread3_Sync5_Start: 09:40:31
F_thread3_Sync5_End: 09:40:33
```
<font color=red>可以发现1，2同时结束，3是等4结束后才开始，它们是同一对象</font>
### 4. 修饰方法
作用范围是整个方法
1. 非静态方法
```java
public class SynchorizedThread extends Thread {
    @Override
	public void run() {
		syn5();
	}
	public synchronized void syn5() {
		 System.out.println(Thread.currentThread().getName() + "_Sync5: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	            try {
	                System.out.println(Thread.currentThread().getName() + "_Sync5_Start: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	                Thread.sleep(2000);
	                System.out.println(Thread.currentThread().getName() + "_Sync5_End: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	            } catch (InterruptedException e) {
	                e.printStackTrace();
	            }
	        
	}
}
```
结果为：
```java
F_thread2_Sync5: 09:44:45
F_thread3_Sync5: 09:44:45
F_thread1_Sync5: 09:44:45
F_thread2_Sync5_Start: 09:44:45
F_thread1_Sync5_Start: 09:44:45
F_thread3_Sync5_Start: 09:44:45
F_thread3_Sync5_End: 09:44:47
F_thread1_Sync5_End: 09:44:47
F_thread2_Sync5_End: 09:44:47
F_thread4_Sync5: 09:44:47
F_thread4_Sync5_Start: 09:44:47
F_thread4_Sync5_End: 09:44:49
```
<font colro=red>可以发现和this对象锁很像，同一个实例的线程访问会被拦截，非同一实例可以同时访问</font>
2. 修饰静态方法
```java
public class SynchorizedThread extends Thread {
    @Override
	public void run() {
		syn5();
	}
	public static synchronized void syn5() {
		 System.out.println(Thread.currentThread().getName() + "_Sync5: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	            try {
	                System.out.println(Thread.currentThread().getName() + "_Sync5_Start: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	                Thread.sleep(2000);
                    System.out.println(Thread.currentThread().getName() + "_Sync5_End: " + new SimpleDateFormat("HH:mm:ss").format(new Date()));
	            } catch (InterruptedException e) {
	                e.printStackTrace();
	            }
	}
}
```
结果为：
```java
F_thread1_Sync5: 09:47:50
F_thread1_Sync5_Start: 09:47:50
F_thread1_Sync5_End: 09:47:52
F_thread4_Sync5: 09:47:52
F_thread4_Sync5_Start: 09:47:52
F_thread4_Sync5_End: 09:47:54
F_thread3_Sync5: 09:47:54
F_thread3_Sync5_Start: 09:47:54
F_thread3_Sync5_End: 09:47:56
F_thread2_Sync5: 09:47:56
F_thread2_Sync5_Start: 09:47:56
F_thread2_Sync5_End: 09:47:58
```
<font color=red>可以发现是和类锁一样</font>
# 总结
1. 对于静态方法，由于此时对象还未生成，采用类锁。
2. 只要是类锁，就会拦截所有的线程，只能让一个线程访问。
3. 对于对象锁（this/Object）,如果是同一个实例，就会按照顺序进行访问，但是如果是不同的实例，就能同时访问
4. 如果对象锁跟访问的对象没有关系，那么就都会同时访问。
5. synchronized 关键字不能被继承。对于父类中的 synchronized 修饰的方法，子类覆盖的时候，默认情况是不同步的，必须使用 synchronized 关键字修饰才行。
6. 定义接口时候不能使用 synchronized 关键字
7. 构造方法不能使用 synchronized 关键字，但可以使用 synchronized 代码块同步。
