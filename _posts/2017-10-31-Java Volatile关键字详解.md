---
layout: post
title:  "Java Volatile关键字详解"
date:   2017-10-31 17:07:01 +0800
categories: java
tag: java基础
---

* content
{:toc}


今天是17年十月份的最后一天，必须得写份博客来纪念一下！

1.volatile之可见性：
-------------------
对于可见性，Java提供了volatile关键字来保证可见性。
当一个共享变量被volatile修饰时，它会保证修改的值会立即被更新到主存，当有其他线程需要读取时，它会去内存中读取新值。

而普通的共享变量不能保证可见性，因为普通共享变量被修改之后，什么时候被写入主存是不确定的，当其他线程去读取时，此时内存中可能还是原来的旧值，因此无法保证可见性。

通过synchronized和Lock也能够保证可见性，synchronized和Lock能保证同一时刻只有一个线程获取锁然后执行同步代码，并且在释放锁之前会将对变量的修改刷新到主存当中。因此可以保证可见性。

2.volatile关键字的两层语义：
--------------------------
一旦一个共享变量（类的成员变量、类的静态成员变量）被volatile修饰之后，那么就具备了两层语义：

1. 保证了不同线程对这个变量进行操作时的可见性，即一个线程修改了某个变量的值，这新值对其他线程来说是立即可见的。
1. 禁止进行指令重排序。

**自增操作不是原子性操作，而且volatile也无法保证对变量的任何操作都是原子性的。**

**volatile关键字能禁止指令重排序，所以volatile能在一定程度上保证有序性。**

**volatile关键字禁止指令重排序有两层意思：**
1. 当程序执行到volatile变量的读操作或者写操作时，在其前面的操作的更改肯定全部已经进行，且结果已经对后面的操作可见；在其后面的操作肯定还没有进行；
1. 在进行指令优化时，不能将在对volatile变量访问的语句放在其后面执行，也不能把volatile变量后面的语句放到其前面执行。
2. 
eg：可能上面说的比较绕，举个简单的例子：

	`//x、y为非volatile变量
	//flag为volatile变量
	x = 2;        //语句1
	y = 0;        //语句2
	flag = true;  //语句3
	x = 4;         //语句4
	y = -1;       //语句5`

由于flag变量为volatile变量，那么在进行指令重排序的过程的时候，不会将语句3放到语句1、语句2前面，也不会讲语句3放到语句4、语句5后面。但是要注意语句1和语句2的顺序、语句4和语句5的顺序是不作任何保证的。
并且volatile关键字能保证，执行到语句3时，语句1和语句2必定是执行完毕了的，且语句1和语句2的执行结果对语句3、语句4、语句5是可见的。

3.使用volatile关键字的场景：
-----------------------
synchronized关键字是防止多个线程同时执行一段代码，那么就会很影响程序执行效率，而volatile关键字在某些情况下性能要优于synchronized，但是要注意volatile关键字是无法替代synchronized关键字的，因为volatile关键字无法保证操作的原子性。通常来说，使用volatile必须具备以下2个条件：
1. 对变量的写操作不依赖于当前值
1. 该变量没有包含在具有其他变量的不变式中
实际上，这些条件表明，可以被写入 volatile 变量的这些有效值独立于任何程序的状态，包括变量的当前状态。
事实上，我的理解就是上面的2个条件需要保证操作是原子性操作，才能保证使用volatile关键字的程序在并发时能够正确执行。

4.应用实例之双重检测同步延迟加载 
---------------------------
 为处理原版非延迟加载方式瓶颈问题，我们需要对 instance 进行第二次检查，目的是避开过多的同步（因为这里的同步只需在第一次创建实例时才同步，一旦创建成功，以后获取实例时就不需要同获取锁了），但在Java中行不通，因为同步块外面的if (instance == null)可能看到已存在，但不完整的实例。JDK5.0以后版本若instance为volatile则可行：

Java代码  

	`public class Singleton {  
			private volatile static Singleton instance = null;  
			private Singleton() {}  
			public static Singleton getInstance() {  
			if (instance == null) {  
				synchronized (Singleton.class) {// 1  
					if (instance == null) {// 2  
						instance = new Singleton();// 3  
						}  
				}  
			}  
			return instance;  
			}  
		 }  `

  
 双重检测锁定失败的问题并不归咎于 JVM 中的实现 bug，而是归咎于 Java 平台内存模型。内存模型允许所谓的“无序写入”，这也是失败的一个主要原因。

更多详情请点击：[http://www.importnew.com/18126.html](http://www.importnew.com/18126.html "http://www.importnew.com/18126.html")