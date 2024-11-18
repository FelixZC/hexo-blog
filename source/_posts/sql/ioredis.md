---
title: ioredis
date: 2024-10-24
author: "pzc"
cover: /assets/images/jpg/63.jpg
categories: [sql]
tags: [Database]
---
### ioredis 简介
ioredis 是为 Node.js 设计的一个高性能 Redis 客户端库。它支持 Redis 的所有功能，并且拥有丰富的高级特性，如自动重连、集群支持、哨兵支持等。ioredis 提供了直观的API，让开发者可以轻松地与Redis进行交互。

### 主要特点
- **自动重连**：在连接丢失后自动尝试重新建立。
- **集群支持**：支持Redis Cluster，实现数据分片。
- **哨兵支持**：支持Redis Sentinel模式，确保高可用性。
- **流水线（Pipelining）**：批量发送命令以减少网络延迟。
- **发布/订阅**：支持Redis的发布/订阅模式。
- **Lua脚本**：可以直接执行Lua脚本来完成复杂的事务处理。
- **Promise API**：支持基于Promise的异步操作，同时也兼容传统的回调函数方式。

### 快速安装
你可以通过npm来安装ioredis：
```bash
npm install ioredis
```

### 基础使用示例
#### 连接Redis
```javascript
const Redis = require('ioredis');
// 创建客户端，默认连接到localhost:6379
const redis = new Redis();
```

#### 存储与获取数据
```javascript
redis.set('mykey', 'value')
  .then(() => {
    return redis.get('mykey');
  })
  .then(value => {
    console.log(`Retrieved value: ${value}`); // 输出 "Retrieved value: value"
  })
  .catch(err => {
    console.error(err);
  });
```

#### 关闭连接
```javascript
redis.disconnect(); // 当不再需要时关闭连接
```

### 高级特性

#### 1. 发布/订阅模式
ioredis 支持 Redis 的发布/订阅模式，可以用于构建实时消息传递系统。
```javascript
const Redis = require('ioredis');
const redis = new Redis();

// 订阅频道
redis.subscribe('news', (err, count) => {
  if (err) throw err;
  console.log(`Subscribed to ${count} channels`);
});

// 监听消息
redis.on('message', (channel, message) => {
  console.log(`Received ${message} from ${channel}`);
});

// 在另一个客户端或同一个客户端的不同部分发布消息
redis.publish('news', 'Hello world!');
```

#### 2. 使用 Lua 脚本
ioredis 可以执行 Lua 脚本来保证原子性操作。
```javascript
const script = `
  local value = redis.call('GET', KEYS[1])
  if not value then
    return nil
  end
  value = tonumber(value)
  return value * ARGV[1]
`;

redis.eval(script, 1, 'mykey', 2).then(result => {
  console.log(`Result: ${result}`); // 输出计算结果
});
```

#### 3. Redis Cluster 支持
如果你的 Redis 是集群模式部署，ioredis 可以无缝地与之交互。
```javascript
const Redis = require('ioredis');
const cluster = new Redis.Cluster([
  { port: 7000, host: '127.0.0.1' },
  { port: 7001, host: '127.0.0.1' }
]);

cluster.set('foo', 'bar').then(() => {
  return cluster.get('foo');
}).then(result => {
  console.log(result); // "bar"
  cluster.disconnect();
});
```

#### 4. Sentinel 支持
对于高可用性的需求，ioredis 提供了对 Redis Sentinel 的支持。
```javascript
const Redis = require('ioredis');
const sentinel = new Redis({
  sentinels: [{ host: 'localhost', port: 26379 }],
  name: 'mymaster',
  role: 'master'
});

sentinel.set('key', 'value').then(() => {
  return sentinel.get('key');
}).then(result => {
  console.log(result); // "value"
  sentinel.disconnect();
});
```

#### 5. 流水线（Pipelining）
流水线可以将多个命令一起发送到服务器，减少网络延迟。
```javascript
const pipeline = redis.pipeline();

pipeline.set('batch1', 'data1');
pipeline.set('batch2', 'data2');
pipeline.get('batch1');
pipeline.get('batch2');

pipeline.exec().then(results => {
  console.log(results); // 结果数组包含每个命令的结果
});
```

### 更多用法

#### 1. 事务（Transactions）
ioredis 支持 Redis 的事务机制，可以确保一系列命令作为单个原子操作执行。
```javascript
const multi = redis.multi();
multi.set('key1', 'value1');
multi.set('key2', 'value2');
multi.get('key1');

multi.exec().then(results => {
  console.log(results); // ["OK", "OK", "value1"]
});
```

#### 2. 监控（Monitoring）
ioredis 可以用来监控 Redis 服务器上的命令执行情况，这对于调试非常有用。
```javascript
redis.monitor((time, args, source, database) => {
  console.log(`${time}: ${args} from ${source} (db ${database})`);
});

// 执行一些命令
redis.set('monitor-test', 'test-value');

// 关闭监控
setTimeout(() => {
  redis.unrefMonitor();
}, 5000);
```

#### 3. 发布/订阅模式中的频道模式
在发布/订阅模式中，你可以同时监听多个频道。
```javascript
const Redis = require('ioredis');
const pub = new Redis();
const sub = new Redis();

sub.subscribe('channel1', 'channel2', (err, count) => {
  if (err) throw err;
  console.log(`Subscribed to ${count} channels`);
});

sub.on('message', (channel, message) => {
  console.log(`Received ${message} from ${channel}`);
});

// 发布消息到不同频道
pub.publish('channel1', 'Hello channel1');
pub.publish('channel2', 'Hello channel2');
```

#### 4. 错误处理
良好的错误处理是开发健壮应用的关键部分。
```javascript
redis.set('key', 'value')
  .catch(err => {
    console.error('Error occurred:', err);
  });

// 全局错误处理
redis.on('error', (err) => {
  console.error('Redis error:', err);
});
```

#### 5. 自定义连接选项
你可以自定义连接 Redis 时的各种选项。
```javascript
const Redis = require('ioredis');
const redis = new Redis({
  port: 6379,
  host: 'localhost',
  family: 4, // 4 (IPv4) or 6 (IPv6)
  password: 'authpassword',
  db: 0
});
```

#### 6. 使用 Sentinel 进行主从切换
ioredis 可以与 Redis Sentinel 配合工作，当主节点发生变化时自动更新连接。
```javascript
const Redis = require('ioredis');
const sentinel = new Redis({
  sentinels: [{ host: 'localhost', port: 26379 }],
  name: 'mymaster'
});

sentinel.on('roleChanged', (role) => {
  console.log(`Role changed to: ${role}`); // 当角色改变时触发
});

// 正常操作
sentinel.set('foo', 'bar').then(() => {
  return sentinel.get('foo');
}).then(result => {
  console.log(result); // "bar"
  sentinel.disconnect();
});
```
