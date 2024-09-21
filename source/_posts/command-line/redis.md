---
title: Redis命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Redis,Database]
---
Redis（Remote Dictionary Server）是一个开源的、支持网络、基于内存、键值对存储数据库，它使用键值结构存储数据，并提供了丰富的数据类型支持。下面是一些常用的Redis命令。

### 字符串 (String) 命令
- `SET key value`：设置指定key的值。
  ```redis
  SET mykey "Hello"
  ```
- `GET key`：获取指定key的值。
  ```redis
  GET mykey
  ```
  输出：
  ```
  "Hello"
  ```
- `INCR key`：将key的值加一，如果key不存在，则创建key并将其值设为0后加一。
  ```redis
  INCR mycounter
  ```
- `DECR key`：将key的值减一，如果key不存在，则创建key并将其值设为0后减一。
  ```redis
  DECR mycounter
  ```
- `INCRBY key increment`：将key中的值增加指定的整数值。
  ```redis
  INCRBY mycounter 5
  ```
- `DECRBY key decrement`：将key中的值减少指定的整数值。
  ```redis
  DECRBY mycounter 3
  ```
- `APPEND key value`：如果key已经存在并且是一个字符串，那么这个命令将value追加到key已有的值之后。
  ```redis
  APPEND mykey " World"
  ```

### 列表 (List) 命令
- `LPUSH key value`：将一个值插入到列表头部。
  ```redis
  LPUSH mylist "first"
  ```
- `RPUSH key value`：将一个值插入到列表尾部。
  ```redis
  RPUSH mylist "last"
  ```
- `LPOP key`：移除并返回列表的第一个元素。
  ```redis
  LPOP mylist
  ```
- `RPOP key`：移除并返回列表的最后一个元素。
  ```redis
  RPOP mylist
  ```
- `LRANGE key start stop`：获取列表中指定范围内的元素。
  ```redis
  LRANGE mylist 0 -1
  ```
- `LLEN key`：获取列表的长度。
  ```redis
  LLEN mylist
  ```

### 集合 (Set) 命令
- `SADD key member`：向集合添加一个成员。
  ```redis
  SADD myset "apple"
  ```
- `SMEMBERS key`：获取集合中所有的成员。
  ```redis
  SMEMBERS myset
  ```
- `SREM key member`：从集合中移除一个成员。
  ```redis
  SREM myset "apple"
  ```
- `SCARD key`：获取集合的成员数量。
  ```redis
  SCARD myset
  ```
- `SISMEMBER key member`：判断member是否是集合key的成员。
  ```redis
  SISMEMBER myset "banana"
  ```

### 有序集合 (Sorted Set) 命令
- `ZADD key score member`：向有序集合添加一个成员，或更新已存在的成员分数。
  ```redis
  ZADD myzset 1 "one"
  ```
- `ZRANGE key start stop [WITHSCORES]`：按升序返回有序集合中指定范围的成员。
  ```redis
  ZRANGE myzset 0 -1 WITHSCORES
  ```
- `ZREVRANGE key start stop [WITHSCORES]`：按降序返回有序集合中指定范围的成员。
  ```redis
  ZREVRANGE myzset 0 -1 WITHSCORES
  ```
- `ZREM key member`：从有序集合中删除一个成员。
  ```redis
  ZREM myzset "one"
  ```
- `ZCARD key`：获取有序集合的成员数量。
  ```redis
  ZCARD myzset
  ```
- `ZSCORE key member`：返回有序集合中成员的分数。
  ```redis
  ZSCORE myzset "two"
  ```

### 哈希表 (Hash) 命令
- `HSET key field value`：将哈希表key中的field的值设为value。
  ```redis
  HSET myhash field1 "Hello"
  ```
- `HGET key field`：获取哈希表key中field的值。
  ```redis
  HGET myhash field1
  ```
- `HDEL key field`：删除哈希表key中的一个或多个field字段。
  ```redis
  HDEL myhash field1
  ```
- `HEXISTS key field`：查看哈希表key中，给定的field是否存在。
  ```redis
  HEXISTS myhash field1
  ```
- `HKEYS key`：获取哈希表中所有的field。
  ```redis
  HKEYS myhash
  ```
- `HVALS key`：获取哈希表中所有的value。
  ```redis
  HVALS myhash
  ```
- `HLEN key`：获取哈希表中field的数量。
  ```redis
  HLEN myhash
  ```

### 通用命令
- `DEL key`：删除一个key。
  ```redis
  DEL mykey
  ```
- `EXISTS key`：检查给定key是否存在。
  ```redis
  EXISTS mykey
  ```
- `TYPE key`：返回key存储的值的类型。
  ```redis
  TYPE mykey
  ```
- `KEYS pattern`：查找所有符合给定模式的key。
  ```redis
  KEYS my*
  ```
- `EXPIRE key seconds`：设置key的过期时间。
  ```redis
  EXPIRE mykey 60
  ```
- `TTL key`：获取key的剩余生存时间。
  ```redis
  TTL mykey
  ```

### 事务 (Transaction) 命令
- `MULTI`：标记一个事务块的开始。
  ```redis
  MULTI
  ```
- `EXEC`：执行所有事务块内的命令。
  ```redis
  EXEC
  ```
- `DISCARD`：取消事务，放弃执行事务块内的所有命令。
  ```redis
  DISCARD
  ```
- `WATCH key [key ...]`：监视一个(或多个)key，如果在事务执行之前这个(或这些)key被其他客户端修改了，那么事务将被打断。
  ```redis
  WATCH mykey
  ```

### 发布/订阅 (Pub/Sub) 命令
- `PUBLISH channel message`：将信息发送到指定的频道。
  ```redis
  PUBLISH news "Breaking News!"
  ```
- `SUBSCRIBE channel [channel ...]`：监听给定的一个或多个频道上的消息。
  ```redis
  SUBSCRIBE news
  ```
- `UNSUBSCRIBE [channel [channel ...]]`：停止监听给定的频道。
  ```redis
  UNSUBSCRIBE news
  ```
- `PSUBSCRIBE pattern [pattern ...]`：监听给定的一个或多个满足给定模式的频道。
  ```redis
  PSUBSCRIBE new.*
  ```
- `PUNSUBSCRIBE [pattern [pattern ...]]`：停止监听给定的模式。
  ```redis
  PUNSUBSCRIBE new.*
  ```

### 脚本 (Scripting) 命令
- `EVAL script numkeys key [key ...] arg [arg ...]`：执行给定的Lua脚本，其中`numkeys`指定了后续参数中有多少个是键名。
  ```redis
  EVAL "return redis.call('INCR', KEYS[1])" 1 mycounter
  ```
- `EVALSHA sha1 numkeys key [key ...] arg [arg ...]`：与`EVAL`类似，但是通过脚本的SHA1摘要来执行脚本，如果服务器没有缓存该脚本，则会返回错误。
  ```redis
  EVALSHA <sha1> 1 mycounter
  ```
- `SCRIPT EXISTS sha1 [sha1 ...]`：检查给定的脚本是否已经被缓存。
  ```redis
  SCRIPT EXISTS <sha1>
  ```
- `SCRIPT FLUSH`：清空所有先前执行过的脚本的缓存。
  ```redis
  SCRIPT FLUSH
  ```
- `SCRIPT KILL`：杀死当前正在运行的脚本，前提是该脚本没有执行写操作。
  ```redis
  SCRIPT KILL
  ```

### 连接 (Connection) 命令
- `AUTH password`：连接到密码保护的Redis实例。
  ```redis
  AUTH mypassword
  ```
- `PING`：测试与服务器的连接状态。
  ```redis
  PING
  ```
- `QUIT`：关闭连接。
  ```redis
  QUIT
  ```
- `SELECT index`：选择数据库编号为index的数据库进行操作。
  ```redis
  SELECT 1
  ```

### 服务器管理 (Server Management) 命令
- `INFO [section]`：获取服务器的各种信息和统计数字。
  ```redis
  INFO
  ```
- `MONITOR`：实时打印出服务器接收到的所有请求。
  ```redis
  MONITOR
  ```
- `CONFIG GET parameter`：获取配置参数的值。
  ```redis
  CONFIG GET maxmemory
  ```
- `CONFIG SET parameter value`：设置配置参数的值。
  ```redis
  CONFIG SET maxmemory 100mb
  ```
- `SHUTDOWN [NOSAVE|SAVE]`：关闭服务器，可选地保存数据。
  ```redis
  SHUTDOWN SAVE
  ```

希望这些示例能帮助你更好地理解和实践Redis命令。