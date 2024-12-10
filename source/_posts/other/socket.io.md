---
title: socket.io
author: pzc
date: 2024-12-04
cover: /assets/images/jpg/106.jpg
categories: [other]
tags: [Socket,Http]
---
## 介绍

`Socket.IO` 是一个用于实时双向事件驱动通信的库，它使得在 Web 应用中实现 WebSocket 功能变得更加简单。`Socket.IO` 支持多种传输方式（如 WebSocket、轮询等），并且提供了自动重连、断线检测等功能，以及更好的跨浏览器兼容性和简单的 API。

### Socket.IO 的特点

- **自动降级**：如果 WebSocket 不可用，`Socket.IO` 会自动切换到其他传输方式，比如长轮询。
- **内置心跳机制**：可以监控连接状态，确保连接活跃。
- **命名空间和房间**：支持创建逻辑分离的通信通道，允许更灵活的消息路由。
- **事件驱动模型**：通过事件来发送和接收数据，简化了应用逻辑。
- **中间件支持**：可以添加自定义中间件来处理握手请求或消息。
- **易于使用**：API 简洁，易于上手。 

### 安装与设置

首先确保你已经安装了 Node.js 和 npm。然后你可以通过 npm 来安装 `socket.io`：

```bash
npm install socket.io express
```

### 创建一个简单的 Socket.IO 应用

#### 服务器端 (Node.js)

创建一个名为 `server.js` 的文件，并添加以下代码：

```javascript
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');

// 创建 Express 应用程序
const app = express();
const server = http.createServer(app);
const io = new Server(server);

// 监听连接事件
io.on('connection', (socket) => {
    console.log('新客户端已连接');

    // 监听来自客户端的消息
    socket.on('chat message', (msg) => {
        console.log('收到消息: ' + msg);
        
        // 广播给所有其他客户端
        io.emit('chat message', msg);
    });

    // 当连接关闭时触发
    socket.on('disconnect', () => {
        console.log('用户断开了连接');
    });
});

// 启动 HTTP 服务器
server.listen(3000, () => {
    console.log('监听 http://localhost:3000');
});
```

#### 客户端 (HTML + JavaScript)

创建一个 HTML 文件 `index.html`，并添加如下代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Socket.IO Chat</title>
<script src="/socket.io/socket.io.js"></script>
<script>
    const socket = io();

    function sendMessage() {
        const input = document.getElementById('messageText');
        const message = input.value;
        socket.emit('chat message', message);
        input.value = '';
    }

    socket.on('chat message', function(msg) {
        const messages = document.getElementById('messages');
        const item = document.createElement('li');
        item.textContent = msg;
        messages.appendChild(item);
        window.scrollTo(0, document.body.scrollHeight);
    });
</script>
</head>
<body>
<h2>Socket.IO 聊天室</h2>
<ul id="messages"></ul>
<form onsubmit="sendMessage(); return false;">
    <input id="messageText" autocomplete="off" /><button>发送</button>
</form>
</body>
</html>
```

### 运行应用程序

1. 在命令行中启动 Socket.IO 服务器：
   ```bash
   node server.js
   ```

2. 打开浏览器访问 `http://localhost:3000`，你应该能够看到聊天界面，并且可以在不同标签页间发送消息。

### 更多功能

- **命名空间**：可以通过不同的命名空间来隔离不同类型的连接。
- **房间**：将多个客户端加入到同一个房间内，以便只向特定的一组客户端广播消息。
- **认证**：可以结合 JWT 或者 session 来验证用户身份。
- **性能优化**：考虑使用 Redis 或者其他适配器来实现水平扩展和负载均衡。

`Socket.IO` 提供了丰富的功能集，适合构建需要实时交互的应用程序，如在线游戏、协作工具、实时通知系统等。

## 与websocket关系

`Socket.IO` 和 WebSocket 是两个不同的概念，但它们之间存在紧密的关系。简单来说，`Socket.IO` 是建立在 WebSocket 协议之上的一个库，它不仅支持 WebSocket 作为传输协议，还兼容其他几种传输方式，以确保最佳的跨浏览器和网络环境兼容性。以下是两者之间的关系及区别：

### WebSocket

- **WebSocket** 是一种通信协议，它允许服务器与客户端之间进行全双工、低延迟的数据交换。
- 它通过单一的 TCP 连接提供双向通信的能力，减少了 HTTP 请求/响应模型中的开销。
- WebSocket 需要显式地创建连接，并且只能在支持该协议的环境中工作。

### Socket.IO

- **Socket.IO** 是一个构建在 WebSocket 协议上的 JavaScript 库（有客户端和服务器端实现），它为实时应用提供了更高层次的抽象。
- `Socket.IO` 不仅使用 WebSocket 作为其底层传输机制之一，还会根据需要自动选择最合适的传输方式（如轮询）。这意味着即使 WebSocket 不被支持或不可用，`Socket.IO` 也能保持功能正常。
- 它引入了事件驱动的消息传递模式，使得开发者可以更方便地处理数据交换。
- `Socket.IO` 提供了一些额外的功能，比如命名空间、房间、自动重连、断线检测等，这些都是 WebSocket 标准本身不提供的。

### 关系总结

- **兼容性**：`Socket.IO` 设计之初就考虑到了不同浏览器和技术栈的支持问题，因此它可以在更多场景下工作，而不仅仅是那些原生支持 WebSocket 的地方。
- **易用性**：对于开发者而言，`Socket.IO` 提供了一个更加友好和简化的 API 来处理实时通信的需求，同时隐藏了底层传输细节。
- **灵活性**：尽管 `Socket.IO` 默认使用 WebSocket，但它也能够回退到其他传输方法，保证了更广泛的适用性和可靠性。
- **附加特性**：`Socket.IO` 增加了许多实用的功能，例如广播消息、加入/离开房间、身份验证中间件等，这些都是直接基于 WebSocket 更难以实现或者需要额外开发的工作。

### 什么时候应该选择哪一个？

- 如果你只需要基本的 WebSocket 功能，并且可以确保你的用户环境都支持 WebSocket，那么你可以直接使用 WebSocket。
- 如果你需要更好的兼容性、更简单的 API、更多的内置功能以及对非 WebSocket 环境的支持，那么 `Socket.IO` 可能是一个更好的选择。

总之，`Socket.IO` 是 WebSocket 的一个高级封装，它简化了很多操作并增加了额外的功能，但是如果你的应用需求非常明确并且不需要这些额外的功能，那么直接使用 WebSocket 也可以是一个轻量级的选择。

## 进阶

对于 `Socket.IO` 的进阶使用，我们可以深入探讨一些高级特性和最佳实践，这些将帮助你构建更复杂、更高效的实时应用程序。以下是几个关键领域：

### 1. 命名空间 (Namespaces)

命名空间允许你创建逻辑上分离的通信通道。这有助于组织不同类型的消息流，并且可以为不同的功能模块提供隔离。

```javascript
// 创建一个自定义命名空间 '/chat'
const chatNamespace = io.of('/chat');

chatNamespace.on('connection', (socket) => {
    console.log('有人连接到了 /chat');
    
    socket.on('chat message', (msg) => {
        chatNamespace.emit('chat message', msg); // 广播给所有在 /chat 的客户端
    });
});
```

### 2. 房间 (Rooms)

房间是进一步细分命名空间内用户的机制。你可以让多个用户加入同一个房间，以便只向特定的一组用户广播消息。

```javascript
io.on('connection', (socket) => {
    socket.join('room1'); // 用户加入 room1

    socket.on('chat message', (msg) => {
        io.to('room1').emit('chat message', msg); // 只发送给 room1 中的用户
    });

    socket.on('disconnect', () => {
        socket.leave('room1'); // 用户离开 room1
    });
});
```

### 3. 自定义事件和数据格式

通过定义明确的事件名称和结构化的数据格式（如 JSON），可以使你的应用逻辑更加清晰和易于维护。

```javascript
// 发送带有类型和内容的消息
socket.emit('message', { type: 'text', content: 'Hello World!' });

// 接收并处理消息
socket.on('message', (data) => {
    if (data.type === 'text') {
        console.log(`收到文本消息：${data.content}`);
    }
});
```

### 4. 认证和授权

确保只有经过验证的用户才能访问 WebSocket 连接或执行某些操作。

```javascript
// 使用中间件进行握手认证
io.use((socket, next) => {
    const token = socket.handshake.auth.token;
    if (verifyToken(token)) {
        return next();
    } else {
        return next(new Error('authentication error'));
    }
});

function verifyToken(token) {
    // 实现你的令牌验证逻辑
}
```

### 5. 性能优化

- **心跳检测**：启用心跳包来监控连接状态，防止僵尸连接。
- **压缩传输**：对 WebSocket 消息启用压缩以减少带宽消耗。
- **负载均衡**：当有大量并发连接时，可以考虑使用 Redis 或其他适配器来实现水平扩展。

```javascript
const io = require('socket.io')(server, {
    cors: {
        origin: "*",
        methods: ["GET", "POST"]
    },
    transports: ['websocket', 'polling'],
    perMessageDeflate: true, // 启用消息压缩
    pingTimeout: 60000,       // 心跳超时时间
    pingInterval: 25000       // 心跳间隔
});
```

### 6. 高可用性和集群支持

为了提高应用程序的可靠性和性能，可以在多台服务器之间分发 Socket.IO 连接。可以使用像 Sticky Sessions 或者共享会话存储（如 Redis）的方法。

```javascript
const { createAdapter } = require("@socket.io/redis-adapter");
const { createClient } = require("redis");

const pubClient = createClient({ url: "redis://localhost:6379" });
const subClient = pubClient.duplicate();

Promise.all([pubClient.connect(), subClient.connect()]).then(() => {
    io.adapter(createAdapter(pubClient, subClient));
});
```

### 7. 监控与日志记录

设置适当的监控和日志系统可以帮助你追踪 Socket.IO 服务器的状态和性能，及时发现并解决问题。

```javascript
io.on('connection', (socket) => {
    console.log(`新连接 ${socket.id}`);

    socket.on('disconnect', (reason) => {
        console.log(`断开连接 ${socket.id}: ${reason}`);
    });

    // 添加更多监控点...
});
```

### 8. 客户端 SDK 和跨平台支持

除了官方提供的 JavaScript SDK 外，还有多种语言和平台的支持，包括 iOS 和 Android 的原生 SDK，以及 .NET、Python 等其他语言的第三方库。

### 示例代码 - 增强版 Socket.IO 应用

这里给出一个更复杂的例子，包含了部分上述提到的功能：

```javascript
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');
const { createAdapter } = require('@socket.io/redis-adapter');
const { createClient } = require('redis');

// 创建 Express 应用程序
const app = express();
const server = http.createServer(app);
const io = new Server(server, {
    cors: {
        origin: "*",
        methods: ["GET", "POST"]
    },
    transports: ['websocket', 'polling'],
    perMessageDeflate: true,
    pingTimeout: 60000,
    pingInterval: 25000
});

// 设置 Redis 适配器用于集群支持
const pubClient = createClient({ url: "redis://localhost:6379" });
const subClient = pubClient.duplicate();

Promise.all([pubClient.connect(), subClient.connect()]).then(() => {
    io.adapter(createAdapter(pubClient, subClient));
});

// 使用中间件进行握手认证
io.use((socket, next) => {
    const token = socket.handshake.auth.token;
    if (verifyToken(token)) {
        return next();
    } else {
        return next(new Error('authentication error'));
    }
});

function verifyToken(token) {
    // 实现你的令牌验证逻辑
}

// 监听连接事件
io.on('connection', (socket) => {
    console.log(`新用户已连接: ${socket.id}`);

    // 加入房间
    socket.join('general');

    // 处理聊天消息
    socket.on('chat message', (msg) => {
        io.to('general').emit('chat message', msg);
    });

    // 断开连接时触发
    socket.on('disconnect', (reason) => {
        console.log(`用户断开了连接: ${socket.id}, 原因: ${reason}`);
    });
});

// 启动 HTTP 服务器
server.listen(3000, () => {
    console.log('监听 http://localhost:3000');
});
```

这个例子展示了如何结合命名空间、房间、认证、性能优化、高可用性等特性来构建一个更为健壮和可扩展的 Socket.IO 应用程序。根据具体需求，你可以进一步调整和完善这些功能。

## @socket.io/redis-adapter

`@socket.io/redis-adapter` 是一个适配器，它使得 `Socket.IO` 可以使用 Redis 作为消息代理，从而实现跨多个进程或服务器的 WebSocket 连接共享。这对于构建高可用性和可扩展性的实时应用至关重要，因为它允许你在不同的实例之间同步事件和状态。

### 安装

首先，确保你已经安装了 `socket.io` 和 `redis`：

```bash
npm install socket.io @socket.io/redis-adapter redis
```

### 配置

接下来，在你的 Node.js 应用中配置 `@socket.io/redis-adapter`。这里有一个简单的例子来展示如何设置：

```javascript
const { createServer } = require('http');
const { Server } = require('socket.io');
const { createAdapter, createAdmin, setupPrimary } = require('@socket.io/redis-adapter');
const { createClient } = require('redis');

// 创建 HTTP 服务器
const httpServer = createServer();

// 创建 Socket.IO 服务器
const io = new Server(httpServer, {
  cors: {
    origin: "*",
    methods: ["GET", "POST"]
  }
});

// 创建 Redis 客户端
const pubClient = createClient({ url: 'redis://localhost:6379' });
const subClient = pubClient.duplicate();

// 等待 Redis 客户端连接成功
Promise.all([pubClient.connect(), subClient.connect()]).then(() => {
  // 使用 Redis 适配器
  io.adapter(createAdapter(pubClient, subClient));

  // 如果是主节点，则设置为 primary
  setupPrimary(io);

  // （可选）创建管理界面
  const admin = createAdmin(io);
  admin.attach(8081); // 在不同端口上运行管理界面
});

// 监听连接事件
io.on('connection', (socket) => {
  console.log('新客户端已连接');

  socket.on('disconnect', () => {
    console.log('用户断开了连接');
  });

  // 示例广播消息到所有客户端
  socket.on('chat message', (msg) => {
    io.emit('chat message', msg);
  });
});

// 启动 HTTP 服务器
httpServer.listen(3000, () => {
  console.log('监听 http://localhost:3000');
});
```

### 关键点解释

- **Redis 客户端**：我们创建了两个 Redis 客户端，一个是发布者 (`pubClient`)，另一个是订阅者 (`subClient`)。它们用于在不同 Socket.IO 实例之间交换信息。
  
- **适配器**：通过调用 `createAdapter(pubClient, subClient)`，我们将 Redis 适配器附加到了 Socket.IO 服务器上，这使得它可以与其他使用相同 Redis 实例的 Socket.IO 服务器共享连接和事件。

- **Primary 设置**：如果你的应用程序有多个主节点（例如在一个 Kubernetes 集群中），你可以指定其中一个作为主要节点来处理一些特定的任务。这可以通过 `setupPrimary(io)` 来完成。

- **管理界面**：`createAdmin(io)` 提供了一个内置的管理界面，可以用来监控和调试你的 Socket.IO 服务器。你可以选择将其绑定到不同的端口上。

### 使用场景

当你想要水平扩展你的应用程序并且需要保持 WebSocket 连接的一致性时，`@socket.io/redis-adapter` 就显得尤为重要。它特别适合以下几种情况：

- **负载均衡**：当你的应用部署在多个服务器后面，并且这些服务器都运行着独立的 Socket.IO 实例时，Redis 适配器可以帮助你在这些实例之间同步连接。
  
- **多区域部署**：如果你的应用分布在不同的地理位置或者云服务提供商的数据中心，那么 Redis 适配器可以确保即使用户连接到了不同的服务器，他们仍然能够接收到一致的消息。

- **高可用性**：通过将 Redis 适配器与 Redis 的持久化和复制特性结合，你可以构建更加健壮的应用架构，保证即使某个节点失败也不会丢失重要的 WebSocket 连接数据。

总之，`@socket.io/redis-adapter` 是构建大规模、分布式实时应用的一个重要工具，它简化了跨多个服务器共享 WebSocket 连接的过程。
