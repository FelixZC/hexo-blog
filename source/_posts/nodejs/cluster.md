---
title: Cluster
author: pzc
date: 2024-10-06
cover: /assets/images/jpg/50.jpg
categories: [nodejs]
tags: [API]
---
`node:cluster` 是 Node.js 内置模块之一，用于创建多进程应用程序。它允许开发者轻松地创建子进程（也称为 worker 进程），这些子进程可以共享同一个 TCP 连接，从而提高应用的性能和稳定性。`cluster` 模块特别适用于利用多核 CPU 的能力，因为单个 Node.js 进程默认情况下只能在一个 CPU 核心上运行。

### 主要概念

- **主进程 (Master Process)**: 当你使用 `cluster` 模块启动一个进程时，这个进程作为主进程运行。主进程的主要职责是监听端口，并将连接请求分发给工作进程。
- **工作进程 (Worker Process)**: 由主进程创建的工作进程实际处理网络请求。每个工作进程都是一个完整的 Node.js 进程，拥有自己的内存空间和 V8 引擎实例。

### 使用场景

- **负载均衡**: 在多核系统上，可以通过创建多个工作进程来平衡负载，充分利用所有可用的 CPU 资源。
- **热更新/零停机部署**: 可以在不停止现有服务的情况下，逐步替换旧版本的工作进程，实现平滑升级。

### 基本用法

下面是一个简单的示例，展示如何使用 `node:cluster` 模块创建一个多进程的 HTTP 服务器：

```javascript
const cluster = require('node:cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isPrimary) {
  console.log(`主进程 ${process.pid} 正在运行`);

  // 叉出工作进程
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', (worker, code, signal) => {
    console.log(`工作进程 ${worker.process.pid} 已退出`);
  });
} else {
  // 工作进程可以共享任何 TCP 连接
  // 在这里，我们创建了一个 HTTP 服务器
  const server = http.createServer((req, res) => {
    res.writeHead(200);
    res.end('你好，世界！');
  });

  server.listen(8000);

  console.log(`工作进程 ${process.pid} 已启动`);
}
```

在这个例子中：
- 如果是主进程（通过 `cluster.isPrimary` 判断），则会根据 CPU 核数创建相应数量的工作进程。
- 如果是工作进程，则会启动一个 HTTP 服务器，监听 8000 端口。

### 高级特性

#### 1. **消息传递**

主进程和工作进程之间可以通过消息传递机制进行通信。这在需要协调多个工作进程或在工作进程之间共享数据时非常有用。

**示例代码：**

```javascript
const cluster = require('node:cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isPrimary) {
  console.log(`主进程 ${process.pid} 正在运行`);

  // 叉出工作进程
  for (let i = 0; i < numCPUs; i++) {
    const worker = cluster.fork();
    worker.send({ hello: 'world' });  // 向工作进程发送消息
  }

  cluster.on('message', (worker, message) => {
    console.log(`收到工作进程 ${worker.process.pid} 的消息:`, message);
  });

  cluster.on('exit', (worker, code, signal) => {
    console.log(`工作进程 ${worker.process.pid} 已退出`);
  });
} else {
  process.on('message', (message) => {
    console.log(`工作进程 ${process.pid} 收到消息:`, message);
  });

  // 工作进程可以共享任何 TCP 连接
  const server = http.createServer((req, res) => {
    res.writeHead(200);
    res.end('你好，世界！');
  });

  server.listen(8000);

  console.log(`工作进程 ${process.pid} 已启动`);
}
```

#### 2. **动态调整工作进程数量**

可以根据系统负载动态调整工作进程的数量。例如，当系统负载较高时，可以增加工作进程数量；当系统负载较低时，可以减少工作进程数量。

**示例代码：**

```javascript
const cluster = require('node:cluster');
const http = require('http');
const os = require('os');

let workers = [];

if (cluster.isPrimary) {
  console.log(`主进程 ${process.pid} 正在运行`);

  // 初始创建工作进程
  for (let i = 0; i < os.cpus().length; i++) {
    const worker = cluster.fork();
    workers.push(worker);
  }

  // 监听系统负载并动态调整工作进程数量
  setInterval(() => {
    const load = os.loadavg()[0];
    const currentWorkers = workers.length;
    const targetWorkers = Math.max(1, Math.min(os.cpus().length, Math.ceil(load)));

    if (targetWorkers > currentWorkers) {
      for (let i = 0; i < targetWorkers - currentWorkers; i++) {
        const worker = cluster.fork();
        workers.push(worker);
      }
    } else if (targetWorkers < currentWorkers) {
      for (let i = 0; i < currentWorkers - targetWorkers; i++) {
        const worker = workers.pop();
        worker.disconnect();
        worker.kill();
      }
    }
  }, 10000);  // 每 10 秒检查一次

  cluster.on('exit', (worker, code, signal) => {
    console.log(`工作进程 ${worker.process.pid} 已退出`);
    workers = workers.filter(w => w !== worker);
  });
} else {
  const server = http.createServer((req, res) => {
    res.writeHead(200);
    res.end('你好，世界！');
  });

  server.listen(8000);

  console.log(`工作进程 ${process.pid} 已启动`);
}
```

### 最佳实践

#### 1. **错误处理和自动重启**

确保工作进程在遇到错误时能够自动重启，以保持服务的高可用性。

**示例代码：**

```javascript
const cluster = require('node:cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isPrimary) {
  console.log(`主进程 ${process.pid} 正在运行`);

  // 叉出工作进程
  for (let i = 0; i < numCPUs; i++) {
    forkWorker();
  }

  function forkWorker() {
    const worker = cluster.fork();
    worker.on('exit', (code, signal) => {
      console.log(`工作进程 ${worker.process.pid} 已退出，正在重启...`);
      forkWorker();  // 重启工作进程
    });
  }
} else {
  const server = http.createServer((req, res) => {
    res.writeHead(200);
    res.end('你好，世界！');
  });

  server.listen(8000);

  console.log(`工作进程 ${process.pid} 已启动`);
}
```

#### 2. **资源隔离**

确保每个工作进程有独立的资源，避免资源竞争。例如，每个工作进程可以有自己的数据库连接池。

#### 3. **日志管理**

使用统一的日志管理方案，确保所有工作进程的日志都能集中管理和分析。

#### 4. **负载均衡策略**

虽然 `cluster` 模块默认使用轮询（round-robin）算法分配连接，但你可以根据具体需求实现更复杂的负载均衡策略。

### 性能优化

#### 1. **减少进程间的通信开销**

尽量减少主进程和工作进程之间的通信，因为每次通信都会有一定的开销。只有在必要时才进行通信。

#### 2. **使用高效的数据结构**

在工作进程中使用高效的数据结构和算法，以减少内存和 CPU 的消耗。

### 监控和调试

#### 1. **使用性能监控工具**

可以使用一些性能监控工具，如 `pm2`、`forever` 或 `Node.js` 自带的 `--inspect` 标志来监控和调试多进程应用。

**示例代码：**

```bash
# 使用 pm2 启动应用
pm2 start app.js -i max
```

#### 2. **日志记录**

使用统一的日志记录库，如 `winston` 或 `log4js`，将所有工作进程的日志集中记录和分析。

**示例代码：**

```javascript
const cluster = require('node:cluster');
const http = require('http');
const winston = require('winston');

const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  transports: [
    new winston.transports.Console(),
    new winston.transports.File({ filename: 'combined.log' })
  ]
});

if (cluster.isPrimary) {
  console.log(`主进程 ${process.pid} 正在运行`);

  // 叉出工作进程
  for (let i = 0; i < numCPUs; i++) {
    forkWorker();
  }

  function forkWorker() {
    const worker = cluster.fork();
    worker.on('exit', (code, signal) => {
      logger.info(`工作进程 ${worker.process.pid} 已退出，正在重启...`);
      forkWorker();  // 重启工作进程
    });
  }
} else {
  process.on('uncaughtException', (err) => {
    logger.error(`未捕获的异常: ${err.stack}`);
    process.exit(1);  // 优雅地退出
  });

  process.on('unhandledRejection', (reason, promise) => {
    logger.error(`未处理的拒绝: ${reason}`);
    process.exit(1);  // 优雅地退出
  });

  const server = http.createServer((req, res) => {
    res.writeHead(200);
    res.end('你好，世界！');
  });

  server.listen(8000);

  logger.info(`工作进程 ${process.pid} 已启动`);
}
```

### 安全性

#### 1. **限制工作进程的权限**

确保工作进程只具有必要的权限，避免它们访问敏感数据或执行危险操作。

#### 2. **安全的进程间通信**

确保主进程和工作进程之间的通信是安全的，避免潜在的安全漏洞。


### 注意事项

- 虽然 `cluster` 模块使得创建多进程应用变得简单，但是每个工作进程都有自己的内存空间，因此它们之间不能直接共享数据。如果需要在工作进程间共享数据，可以考虑使用消息传递机制或外部存储。
- 工作进程的崩溃不会影响其他工作进程或主进程，但是建议设置适当的错误处理逻辑来重启失败的工作进程，确保服务的持续可用性。

### 其他注意事项
#### 1. **文件描述符限制**

在高并发环境下，确保系统的文件描述符限制足够高，以避免因文件描述符耗尽而导致的问题。

#### 2. **资源回收**

确保在工作进程退出时，释放所有占用的资源，如关闭数据库连接、释放文件句柄等。

### 总结

`node:cluster` 模块提供了强大的多进程支持，使得 Node.js 应用程序能够充分利用多核 CPU 的性能。通过合理的错误处理、性能优化、监控和调试，可以构建高性能、高可用的应用程序。