---
title: Redis命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Redis,Database]
---
Redis（Remote Dictionary Server）是一个开源的、支持网络、基于内存、键值对存储数据库，它使用键值结构存储数据，并提供了丰富的数据类型支持。下面是一些常用的Redis命令，这些命令可以分为几个主要类别：字符串、列表、集合、有序集合、哈希表等。

### 字符串 (String) 命令
- `SET key value`：设置指定key的值。
- `GET key`：获取指定key的值。
- `INCR key`：将key的值加一，如果key不存在，则创建key并将其值设为0后加一。
- `DECR key`：将key的值减一，如果key不存在，则创建key并将其值设为0后减一。
- `INCRBY key increment`：将key中的值增加指定的整数值。
- `DECRBY key decrement`：将key中的值减少指定的整数值。
- `APPEND key value`：如果key已经存在并且是一个字符串，那么这个命令将value追加到key已有的值之后。

### 列表 (List) 命令
- `LPUSH key value`：将一个值插入到列表头部。
- `RPUSH key value`：将一个值插入到列表尾部。
- `LPOP key`：移除并返回列表的第一个元素。
- `RPOP key`：移除并返回列表的最后一个元素。
- `LRANGE key start stop`：获取列表中指定范围内的元素。
- `LLEN key`：获取列表的长度。

### 集合 (Set) 命令
- `SADD key member`：向集合添加一个成员。
- `SMEMBERS key`：获取集合中所有的成员。
- `SREM key member`：从集合中移除一个成员。
- `SCARD key`：获取集合的成员数量。
- `SISMEMBER key member`：判断member是否是集合key的成员。

### 有序集合 (Sorted Set) 命令
- `ZADD key score member`：向有序集合添加一个成员，或更新已存在的成员分数。
- `ZRANGE key start stop [WITHSCORES]`：按升序返回有序集合中指定范围的成员。
- `ZREVRANGE key start stop [WITHSCORES]`：按降序返回有序集合中指定范围的成员。
- `ZREM key member`：从有序集合中删除一个成员。
- `ZCARD key`：获取有序集合的成员数量。
- `ZSCORE key member`：返回有序集合中成员的分数。

### 哈希表 (Hash) 命令
- `HSET key field value`：将哈希表key中的field的值设为value。
- `HGET key field`：获取哈希表key中field的值。
- `HDEL key field`：删除哈希表key中的一个或多个field字段。
- `HEXISTS key field`：查看哈希表key中，给定的field是否存在。
- `HKEYS key`：获取哈希表中所有的field。
- `HVALS key`：获取哈希表中所有的value。
- `HLEN key`：获取哈希表中field的数量。

### 通用命令
- `DEL key`：删除一个key。
- `EXISTS key`：检查给定key是否存在。
- `TYPE key`：返回key存储的值的类型。
- `KEYS pattern`：查找所有符合给定模式的key。
- `EXPIRE key seconds`：设置key的过期时间。
- `TTL key`：获取key的剩余生存时间。

以上仅是Redis命令的一部分，Redis还支持事务、发布/订阅、Lua脚本等功能。对于更详细的信息，建议参考官方文档或使用`HELP`命令来获取帮助。例如，可以在Redis客户端输入`HELP @string`来获取关于字符串的所有命令的帮助信息。