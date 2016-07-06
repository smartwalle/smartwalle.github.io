---
layout: post
title: "Redis 学习笔记 - LIST"
date: 2016-07-06 21:00:00 +0800
categories: Redis
---
## LIST

Redis 的 List 基于 Linked List 实现，当向一个拥有大量元素列表的首或者尾添加元素的时候，速度也是极快，缺点是利用索引访问元素的时候，性能会有一些影响。

Redis 的 List 允许用户从序列的两端推入或者弹出元素、获取列表元素，以及执行各种常见的列表操作。

### List 的阻塞操作
Redis 的 List 提供了阻塞式访问的命令: BRPOP 和 BLPOP。在获取数据时可以指定如果数据不存在阻塞的时间，如果在时限内获得数据，则正常返回，如果超时还没有数据，则返回 null，如果超时时间设置为0，则表示一直阻塞，直到接收到数据为止。

| 命令 | 描述 | 返回值 |
| --- | --- | --- |
| BLPOP key [key ...] timeout | 从第一个非空列表中弹出位于最左边的元素，如果列表都为空，则会阻塞 timeout 秒并等待元素的出现。 | |
| BRPOP key [key ...] timeout| 与 BLPOP 一致，只不是弹出位于列表最右端的元素。 | |
| BRPOPLPUSH source-key dest-key timeout | 弹出 source-key 列表中最右端的元素，将该元素添加到 dest-key 列表的最左端，并返回这个元素。如果 source-key 为空，则会阻塞 timeout 秒并等待元素的出现。 | |
| LINDEX key index | 获取列表中指定索引的元素。索引是从0开始的。-1 为最后一个元素，-2为倒数第二个元素。 | 当指定索引不存在的时候，则会返回 null |
| LINSERT key BEFORE\|AFTER pivot value | 在基准值(pivot)的前面或者后面插入一个新值(value)。key 如果不存在，则不作执行任何操作。 | |
| LLEN key | 获取列表的长度。 | |
| LPOP key | 移除并且返回列表最左边的元素。 | |
| LPUSH key value [value ...] | 将指定的值添加到列表的头部。 | 添加值之后列表的长度 |
| LPUSHX key value | 当 key 对应的 list 存在的时候，向 list 的头部添加指定值。 | 添加值之后列表的长度 |
| LRANGE key start end | 获取指定偏移量范围内的所有元素（包括 start 和 end）。 | |
| LREM key count value | 从列表中移除前 count 次出现的值为 value 的元素。 count > 0，从头往尾移除；count < 0，从尾往头移除；count = 0，移除所有值为 value 的元素。 | |
| LSET key index value | 设置指定索引位置的元素值 | |
| LTRIM key start end | 修剪指定列表，只保留 start 到 end 之间的元素，包括 start 和 end。 | |
| RPOP key | 移除并且返回列表最右边的元素。 | |
| RPOPLPUSH source-key dest-key | 移除 source-key 列表最右边的元素，将该元素添加到 dest-key 列表的左端，并且返回该元素。 | |
| RPUSH key value [value ...] | 向列表尾部添加指定的值。 | 添加值之后列表的长度 |
| RPUSHX key value | 当 key 对应的 list 存在的时候，向 list 的尾部添加指定值。 | 添加值之后列表的长度 |