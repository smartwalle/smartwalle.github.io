---
layout: post
title: "Redis 学习笔记 - HASH"
date: 2016-07-08 11:00:00 +0800
categories: Redis
---
## HASH

Redis 的 Hash 是一个字符串类型的 field 和 value 的映射表，适合用于存储对象。


| 命令 | 描述 | 返回值 |
| --- | --- | --- |
| HDEL key field [field ...] | 从散列里面删除指定的字段。 |
| HEXISTS key field | 判断指定散列里面是否存在某个字段。 |
| HGET key field | 获取散列指定字段的值。 | 
| HGETALL key | 获取散列所有的字段和值。 |
| HINCRBY key field increment | 对散列指定的字段执行递增的操作，增量为 increment。 | 
| HINCRBYFLOAT key field increment | 对散列指定的字段执行递增的操作，增量为 increment，类型为 float。| 字段执行递增之后的值。 |
| HKEYS key | 获取散列所有的字段。 |
| HLEN key | 获取散列所有字段的数量。 |
| HMGET key field [field ...] | 获取指定字段的值。 | 字段及其值的列表 |
| HMSET key field value [field value ...] | 设置字段的值。 |
| HSET key field value | 设置一个字段的值。 | 
| HSETNX key field vaue | 设置一个字段的值，只有当这个字段不存在的时候才会生效。 |
| HSTRLEN key field | 获取指定字段值的长度。 |
| HVALS key | 获取指定散列所有的值。 |