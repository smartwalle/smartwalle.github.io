---
layout: post
title: "MongoDB 集群 - Master-Slave"
date: 2016-08-10 12:40:00 +0800
categories: MongoDB
---

**不推荐使用**

如果只是简单的作数据备份，可以考虑使用 Master-Slave 模式，其配置较之 Replica Set 也会稍微简单一点，但是从可持续提供服务上来讲，还是推荐使用 Replica Set 模式。

假设有两台服务器: 192.168.192.1 和 192.168.192.2。

在此，我们把 192.168.192.1 作为 Master(主节点)，192.168.192.2 作为 Slave(从节点)。

启动 Master:

```
./bin/mongod --dbpath ./mydb --master
```

对的，只需要添加一个```--master```参数。

启动 Slave:

```
./bin/mongod --dbpath ./mydb --slave --source 192.168.192.2
```

启动从节点稍微复杂一点，需要两个参数，即```--slave```和```--source```。

--slave 用于标记以从节点启动。
--source 用于指定需要备份的服务器。

至此，一个采用 Master-Slave 模式架构的 MongoDB 集群就部署完成了。

当然实际运用中，还需要考虑到安全问题，可以参考上一篇文章《MongoDB 集群 - Replica Set》，在启动 MongoDB 数据服务的时候加上 --keyFile 即可。