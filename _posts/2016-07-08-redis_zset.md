---
layout: post
title: "Redis 学习笔记 - ZSET"
date: 2016-07-08 10:00:00 +0800
categories: Redis
---
## ZSET

Redis 的 ZSET 和 SET 类似，其存储的每一个元素都是唯一的，只不过在 ZSET 里面的元素都是经过排序的。

存储在 ZSET 里面的元素都有一个对应的分值，分值决定了该元素在 ZSET 里面的位置。


| 命令 | 描述 | 返回值 |
| --- | --- | --- |
| ZADD key [NX\|XX] [CH] [INCR] score member [score member ...] | 将多个元素添加到指定集合里面。可选参数说明：NX-不更新存在的成员，只添加新成员；XX-仅仅更新存在的成员，不添加新的成员；CH-修改返回值为；INCR-对成员的分值进行递增操作；| 
| ZCARD key | 获取集合的元素数量。 |
| ZCOUNT key min max | 获取指定分值范围内的元素数量。 |
| ZINCRBY key increment member | 为指定元素的分值作递增操作。 increment 为递增量。 | 成员新的分值 | 
| ZRANGE key start stop [WITHSCORES] | 获取指定偏移范围内的元素。 |
| ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT offset count] | 获取指定分值范围内的元素。 |
| ZRANK key member | 返回元素在集合中的排名。 |
| ZREM key member [member ...] | 从集合中删除指定的元素。 | 成功删除元素的数量 |
| ZREMRANGEBYRANK key start stop | 删除指定索引范围内的所有元素。 | 成功删除元素的数量 |
| ZREMRANGEBYSCORE key min max | 删除指定分值范围内的所有元素。 | 成功删除元素的数量 |
| ZREVRANGE key start stop [WITHSCORES] | 获取指定索引范围内的所有元素。排序方式是从高到低。 |
| ZREVRANGEBYSCORE key max min [WITHSCORES] [LIMIT offset count] | 获取指定分值范围内的所有元素。注意是从 max 到 min，即是从高分到低分。 |
| ZREVRANK key member | 获取元素在集合中的排名，排序方式是从大到小。 |
| ZSCORE key member | 获取指定元素的分值。 |
