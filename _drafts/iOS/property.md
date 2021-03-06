---
layout: post
title: "Property"
date: 2016-05-29 23:00:00 +0800
categories: iOS
---
## Property
@property 是 Objective-c 在 2.0 之后加入的一个用于声明属性的指令，它可以快速方便的为实例变量创建存取器，并允许我们通过点语法使用存取器。与 @property 相关联的还有 @synthesize 和 @dynamic，@synthesize 的作用是用于自动生成 getter 和 setter，不过在 Xcode 4.4 之后，@synthesize 已经淡出了我们的视线，所有的工作都由 @property 完成。@dynamc 是告诉编译器，属性的 setter 和 getter 方法由用户自己实现，不自动生成。

#### 作用

* 生成成员变量的 getter / setter 方法的声明；
* 生成私有的（以下划线开头）成员变量；
* 生成了 getter / setter 方法的实现；


#### Accessor (存取器)
用于获取和设置实例变量的方法，即 getter 和 setter。getter 用于获取实例变量的值，setter 用于设置实例变量的值。


在使用 @property 声明一个属性的时候，我们还会用到很多的关键字，它们都是有特殊作用的，根据它们的用途我们将其划分为三类：原子性、访问器控器、内存管理和方法名。

### 原子性

##### atomic
默认特性，意思为操作是原子的，即在同一时刻，只能有一个线程访问的实例变量，所以 atomic 是线程安全的。但是出于效率方面的原因，其很少被使用。

##### nonatomic
与 atomic 刚好相反，非原子性的，即在同一时刻，可以被多个线程访问。效率比 atomic 快，但是不能保证其在多线程环境下的安全性。

### 访问器控制

##### readwrite
默认特性，表示该属性同时拥有 getter 和 setter 方法。

##### readonly
表示该属性是只读的，只拥有 getter 方法。

### 内存管理

##### assign
常用于基本值类型，如 int, float, double, CGFloat, NSInteger 等等，表示简单的赋值，不会修改引用计数。

##### retain
会对传入对象的引用计数器进行+1的操作，以拥有该对象的所有权。

##### strong
ARC 引入的新关键字，retian 的可选替代者。顾名思义，其会对传入的对象进行强引用，即拥有原对象的所有权，会将原对象的引用计数+1。

##### weak
不会对传入对象的引用计数进行+1操作，只是对该对象的一个弱引用，当原对象的引用计数为0时，该对象被释放之后，用 weak 声明的实例变量即会指向 nil。

##### copy
与 strong 类似，但是区别在于实例变量拥有的是传入对象副本的所有权，而非对象本身。

### 方法名

#### getter
用于指定该属性的 getter 方法。

#### setter
用于指定该属性的 setter 方法。

### 默认

在 ARC 环境下，在使用 @property 声明属性的时候，如果不指定任何修饰关键字，默认的情况如下：

* 基本数据类型: atomic, readwrite, assign

* Objective-c 对象: atomic, readwrite, strong
