---
layout: post
title: "CoreData"
date: 2016-05-28 09:00:00 +0800
categories: iOS
---
## CoreData

CoreData 是一个模型层的技术，它能够帮助开发者快速建立描述应用程序状态的模型层。同时，它也是一种持久化技术，能够将模型对象的状态技术化到磁盘。最重要的是，CoreData 不仅仅是一个存储、获取数据的框架，它还能很好地和内存中的数据共事。

#### NSManagedObjectModel
用于描述应用程序的数据模型，这个模型包括实体（Entity）、特性(Property)、读取请求(FetchRequest)等信息。其维护着实体对象和 NSManagedObject 类之间的映射表。

#### NSPersistentStoreCoordinator
持久化存储协调器，用于指定对象的存储方式和存储位置。

#### NSManagedObjectContext
对象管理上下文，负责数据的实际操作。

#### NSManagedObject
被管理的数据对象。

## 堆栈
CoreData 有很多组件，当把这些组件都捆绑到一起的时候，我们把它称作 CoreData 堆栈，这个堆栈有两个主要部分：一是对象图管理；二是持久化，保存模型对象的状态或者恢复模型对象的状态。

在这两个部分之间，是持久化存储协调器，它将对象图管理部分和持久化部分捆绑在一起，当它们两者中的任何一部分需要和另一部分进行交流时，就需要持久化存储协调器来进行调节了。

对象图管理是应用程序模型层的逻辑存在的地方，模型层的对象存在于一个 context 内。在大多数情况下，存在一个 context，并且所有的对象存在于那个 context 中。CoreData 支持多 contexts, 每个 context 与其它的 context 都是完全独立的。context 中的对象与其是相关联的，每个被管理的对象都知道自己属于那个 context，每个 context 都知道自己管理着那些对象。

堆栈的另一部分就是持久了，即 CoreData 从文件系统中读取或者写入数据。每个持久化存储协调器都有一个属于自己的持久化存储，并且这个持久化存储在文件系统中与 SQLite 数据库进行交互。


---
参考文献：

* [Core Data Overview](https://www.objc.io/issues/4-core-data/core-data-overview/)
* [Core Data 概述
](http://objccn.io/issue-4-1/)