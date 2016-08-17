---
layout: post
title: "MongoDB 集群 - Sharding"
date: 2016-08-16 19:00:00 +0800
categories: MongoDB
---

前面所说的 Master - Slave 和 Replica Set 最主要的应用场景是数据备份和故障恢复，如果想要真正体会到 MongoDB 集群的强大，那还得上分片 - Sharding。关于分片的概念，网上已经有很多，比如这里[搭建高可用mongodb集群（四）—— 分片](http://www.lanceyan.com/tech/arch/mongodb_shard1.html)，本文不作过多介绍。只是搭建方式大多都停留在较老的版本，如果是从零开始搭建一个新的 MongoDB 服务集群，未免有些过时。所以本文将对使用 MongoDB 3.2.8 搭建一个分片服务进行简单介绍。

对于较小的数据操作，单机可能问题不大，但是如果数据量大了，这时候就要考验硬件设备及网络的性能了。纵向扩展代价太大，或者已经到了不可扩展的地步，就只有横向扩展了。幸好，MongoDB 在横向扩展方面确实做的很好很强大。

对于分片的配置，会涉及到 Replica Set 相关的知识，如果对于这方面还不了解，建议先查看如何配置 Replica Set。


### 什么是 Sharding?

将数据库拆分，将其分散到不同机器上的过程。将数据分散到不同的机器上，因此不需要强大的服务器就可以存储更多的数据和运行更强大的计算。

MongoDB 分片的基本思想就是将集合分成小块，然后将这些小块分散到若干片里，每个片只负责总数据的一部分，最后通过一个均衡器来对各个分片进行均衡。

MongoDB 的分片主要包含: mongos、config server、shard 和 replica set。

### 准备工作

自行从官网下载最新的 MongoDB 软件，本文采用的版本是 3.2.8。

由于只是测试，所以所有的操作都在一台电脑上完成，但是方法适用于任何环境。

从 MongoDB 分片的概念中可以得知，主要需要三个组件： mongos、config server、shard。

本机IP：192.168.192.105

### Shard 搭建

分片是最终存储数据的地方，可以是一个独立的服务，也可以是一个副本集。从可持续发展的角度来看，本人不推荐使用独立服务，所以下面的搭建也将采用副本集的形式。

为了更加详细的介绍分片的搭建，在此将部署两个副本集，每个副本集有三个节点：一个主节点、一个备份节点和一个仲裁节点。

我们规定第一个副本集名字为 s1，主节点端口为 30001、备份节点端口为 30002、仲裁节点端口为 30003。

第二个副本集名字为 s2，主节点端口为 40001、备份节点端口为 40002、仲裁节点端口为 40003。

首先配置副本集 s1，可以打开三个终端窗口，分别执行下面的命令启动服务（注意自行创建数据存放目录）：

```
./bin/mongod --shardsvr --port 30001 --dbpath ./s130001 --replSet s1
./bin/mongod --shardsvr --port 30002 --dbpath ./s130002 --replSet s1
./bin/mongod --shardsvr --port 30003 --dbpath ./s130003 --replSet s1
```

成功启动服务之后，连接上 30001 进行配置：

```
> var config = {_id:"s1", members:[{_id:0, host:"192.168.192.105:30001"}, {_id:1, host:"192.168.192.105:30002"}, {_id:2, host:"192.168.192.105:30003", arbiterOnly: true}]}
> rs.initiate(config)
```

不出意外，这时候已经配置好第一个副本集了，并且主节点为 30001。


用同样的方式配置好副本集 s2：

```
./bin/mongod --shardsvr --port 40001 --dbpath ./s240001 --replSet s2
./bin/mongod --shardsvr --port 40002 --dbpath ./s240002 --replSet s2
./bin/mongod --shardsvr --port 40003 --dbpath ./s240003 --replSet s2
```

```
> var config = {_id:"s2", members:[{_id:0, host:"192.168.192.105:40001"}, {_id:2, host:"192.168.192.105:40002"}, {_id:3, host:"192.168.192.105:40003", arbiterOnly: true}]}
> rs.initiate(config)
```

到此，Shard 就配置完成。


### Config Server 搭建

Config Server 也需要搭建为副本集的形式(我用的 3.2.8 是必须这样做，以前老版本也是建议搭建三台服务器作为 Config Server)。

我们规定端口分别为 50001、50002 和 50003，副本集名字为 cs：


```
./bin/mongod --configsvr --port 50001 --dbpath ./cs50001 --replSet cs
./bin/mongod --configsvr --port 50002 --dbpath ./cs50002 --replSet cs
./bin/mongod --configsvr --port 50003 --dbpath ./cs50003 --replSet cs
```

连接上 50001 进行副本集配置：

```
> var config = {_id:"cs", members:[{_id:0, host:"192.168.192.105:50001"}, {_id:1, host:"192.168.192.105:50002"}, {_id:2, host:"192.168.192.105:50003"}]}
> rs.initiate(config)
```

**特别注意：Config Server 的副本集不能有仲裁节点。**

### Mongos 搭建

接下来就需要进行 Mongos 配置了，我们规定端口为 50005，启动服务：

```
./bin/mongos --port 50005 --configdb cs/192.168.192.105:50001,192.168.192.105:50002,192.168.192.105:50003
```

注意 --configdb 参数的格式为: 副本集名字/ip:port[,ip:port]。

如果看到控制台输出 ```config servers and shards contacted successfully```，那说明一切正常。

连接上 Mongos：

```
./bin/mongo --port 50005
```

添加分片：

```
> sh.addShard("s1/192.168.192.105:30001") # 只需要添加主节点的 IP 和端口就好。
> sh.addShard("s2/192.168.192.105:40001")
> sh.status() #查看分片信息
```

对数据库开启分片：

```
> sh.enableSharding("mydb") #首先对数据库启用分片
> sh.shardCollection("mydb.c1", {"name": 1}) #再对集合进行分片，name字段是片键。片键的选择：利于分块、分散写请求、查询数据。
> sh.status() #查看分片信息
```

可以尝试往 mydb 的 c1 集合里面添加一些数据，以测试是否成功分片，当然要多添加一些数据才会有效果哦。

看起来需要很多服务器，貌似很复杂的样子，其实也很简单啦。

### 用户验证

本文示涉及到用户验证的配置，其配置和副本集的配置是一样的。
