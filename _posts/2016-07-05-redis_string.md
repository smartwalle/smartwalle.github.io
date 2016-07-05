---
layout: post
title: "Redis 学习笔记 - STRING"
date: 2016-07-05 12:00:00 +0800
categories: Redis
---
## STRING

字符串是 Redis 中最基础的数据存储类型，其值可以是任何种类的字符串（包括二进制数据），长度不能超过512MB。

虽然 STRING 是字符串类型，但是可以对其进行原子递增、原子递减等操作。

| 命令 | 描述 | 返回值 |
| --- | --- | --- |
| APPEND key value | 如果 key 已经存在，并且值为字符串，则把 value 追加到原来值的结尾；如果 key 不存在，则会先创建一个空的字符串，再执行追加操作。| 返回 Append 后字符串值的长度 |
| DECR key | 对指定 key 对应的数字做减1操作，如果 key 不存在，则会先将 key 的值设置为 0；如果 key 有一个错误类型的 value 或者是一个不能表示成数字的字符串，则返回错误。（最大支持 64位有符号的整数，只能是 value 可以表示为整数的字符串) | 递减之后的 value |
| DECRBY key decrement | 对指定 key 的 value 进行减少 decrement 的操作。(只能是 value 可以表示为整数的字符串) | 减少之后的 value |
| GET key | 获取 key 对应的 value，如果 key 不存在，则返回 nil；如果 key 对应的值不是字符串，则返回错误。 | value 或者 nil |
| GETRANGE key start end | 获取 key 对应字符串的子串，子串的范围由 start 和 end 决定(包含 start 和 end)。 | 包含在 start 和 end 范围内的子串 |
| GETSET key value | 获取该 key 的旧值，并为该 key 设置一个新的值 | 旧值 |
| INCR key | 对指定的 key 进行递增操作。(只能是 value 可以表示为整数的字符串) | 递增之后的 value |
| INCRBY key increment | 对指定 key 的 value 进行增加 increment 的操作。(只能是 value 可以表示为整数的字符串) | 增加之后的 value |
| INCRBYFLOAT key increment | 对指定 key 对应的浮点数做增加 increment 的操作。如果键不存在，则会将其值设置为 0。 | 增加之后的 value |
| MGET key [key ...] | 批量获取指定 key 列表的 value 列表，对于不存在的 key，将返回 nil。 | value 列表 |
| MSET key value [key value ...] | 批量设置 key value | OK |
| MSETNX key value [key value ...] | 批量设置 key value，如果指定的 key 列表中，已经存在一个 key，则都不会执行。 | 1 或者 0|
| PSETEX key milliseconds value | 设置 key 的值为 value，并且指定其过期时间，单位为毫秒。 | |
| SET key value  | 设置 key 的值为 value | |
| SETEX key seconds value | 设置 key 的值为 value，并且指定其过期时间，单位为秒。 | |
| SETNX key value | 设置 key 的值为 value，只有当 key 不存在的时候才会设置，当 key 存在的时候，则什么都不会做。 | |
| STRLEN key | 获取指定 key 对应字符串的长度，只能用于获取 STRING 类型Value 的长度。 | 值的长度 |
