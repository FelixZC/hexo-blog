---
title: websocket
author: pzc
date: 2024-12-04
cover: /assets/images/jpg/105.jpg
categories: [other]
tags: [Socket,Http]
---
## 介绍

WebSocket 是一种在单个 TCP 连接上进行全双工通信的协议。它使得客户端和服务器之间的数据交换变得更加简单，允许服务器主动向客户端推送数据。WebSocket 通信协议在2011年由 IETF 制定为 RFC 6455 标准，并由 WHATWG 定义了 WebSocket JavaScript API。

以下是关于 WebSocket 的详细介绍：

### 特点

- **全双工通信**：一旦连接建立，WebSocket 允许服务器和客户端之间同时发送数据。
- **减少延迟**：相比 HTTP 请求/响应模式，WebSocket 可以显著减少延迟，因为它不需要为每个请求建立新的连接。
- **低开销**：与 HTTP 相比，WebSocket 消息头更小，减少了传输的数据量。
- **保持连接**：WebSocket 连接在会话期间保持打开状态，除非被显式关闭或发生错误。

### 工作流程

1. **握手阶段**：WebSocket 会话开始于一个 HTTP 请求，这个请求包含了特殊的 Upgrade 头信息，用来请求将现有的 HTTP 连接升级到 WebSocket 协议。
2. **连接建立**：如果服务器同意升级，它会返回一个 101 Switching Protocols 状态码以及必要的响应头来完成握手过程。此时，HTTP 连接就转换成了 WebSocket 连接。
3. **数据传输**：一旦连接建立，双方可以自由地发送帧（frame）格式的数据。这些帧可以是文本或二进制数据。
4. **连接关闭**：当任意一方想要关闭连接时，需要发送一个关闭帧给对方，然后等待对方也发送关闭帧确认关闭。之后，双方都可以安全地关闭连接。

### 使用场景

- 实时聊天应用
- 在线游戏
- 实时更新的仪表盘或通知系统
- 股票市场数据流
- 文件上传进度跟踪

### API 和库

大多数现代浏览器都支持 WebSocket API，开发者可以直接通过 JavaScript 来使用 WebSocket。此外，有许多服务器端实现和技术栈支持 WebSocket，如 Node.js、Java、Python、Ruby 等等。对于移动开发，iOS 和 Android 平台也有各自的 WebSocket 库和支持。

### WebSocket URL

WebSocket 使用 `ws://` 或者加密的 `wss://` 作为协议前缀，类似于 HTTP 和 HTTPS。

### 安全性

WebSocket 支持通过 TLS 加密连接，确保数据传输的安全性。WSS（WebSocket Secure）就是通过 SSL/TLS 加密的 WebSocket 协议。

### 浏览器兼容性

几乎所有现代浏览器都支持 WebSocket。然而，在使用 WebSocket 之前，应该检查目标用户的浏览器是否支持此功能，或者提供回退方案。

WebSocket 提供了一种高效的方式来进行双向通信，非常适合需要实时交互的应用程序。

## 示例

下面我会给出一个简单的 WebSocket 示例，包括服务器端和客户端的实现。这里以 Node.js 作为服务器端语言，并使用 `ws` 这个流行的 WebSocket 库来创建 WebSocket 服务器。对于客户端，我将展示如何使用原生 JavaScript 来连接到 WebSocket 服务器。

### 服务器端（Node.js）

首先，你需要安装 `ws` 包。如果你还没有安装 Node.js 和 npm，请先进行安装。

```bash
npm install ws
```

然后创建一个名为 `server.js` 的文件，添加以下代码：

```javascript
const WebSocket = require('ws');

// 创建 WebSocket 服务器，监听 8080 端口
const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', function connection(ws) {
    console.log('新客户端已连接');

    // 监听来自客户端的消息
    ws.on('message', function incoming(message) {
        console.log('收到消息： %s', message);

        // 向所有客户端广播消息
        wss.clients.forEach(function each(client) {
            if (client !== ws && client.readyState === WebSocket.OPEN) {
                client.send(`有人发来了消息: ${message}`);
            }
        });
    });

    // 当连接关闭时触发
    ws.on('close', function close() {
        console.log('客户端已断开');
    });
});

console.log('WebSocket 服务器正在运行在 ws://localhost:8080/');
```

### 客户端（HTML + JavaScript）

创建一个 HTML 文件 `index.html`，并添加如下代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>WebSocket Client</title>
</head>
<body>

<h2>WebSocket 测试</h2>
<div id="messages"></div>
<input type="text" id="messageText" placeholder="输入消息..." />
<button onclick="sendMessage()">发送消息</button>

<script>
let ws;

function initWebSocket() {
    // 连接到 WebSocket 服务器
    ws = new WebSocket('ws://localhost:8080');

    // 连接成功时触发
    ws.onopen = function() {
        console.log('连接已建立');
    };

    // 接收消息时触发
    ws.onmessage = function(event) {
        const messages = document.getElementById('messages');
        const message = document.createElement('div');
        message.textContent = event.data;
        messages.appendChild(message);
    };

    // 连接关闭时触发
    ws.onclose = function() {
        console.log('连接已关闭');
    };

    // 发生错误时触发
    ws.onerror = function(error) {
        console.error('WebSocket 错误: ', error);
    };
}

function sendMessage() {
    const input = document.getElementById('messageText');
    if (ws && ws.readyState === WebSocket.OPEN) {
        ws.send(input.value);
        input.value = '';
    } else {
        alert('WebSocket 连接未建立或已关闭');
    }
}

window.onload = initWebSocket;
</script>

</body>
</html>
```

### 运行示例

1. 在命令行中启动 WebSocket 服务器：
   ```bash
   node server.js
   ```

2. 打开浏览器，访问 `index.html` 文件所在的 URL（如果是本地文件可以直接打开，或者通过 HTTP 服务器提供服务）。

3. 打开多个浏览器标签页或窗口，尝试在不同页面间发送消息，你将会看到消息被实时地广播给所有连接的客户端。

这个例子演示了基本的 WebSocket 功能，包括连接、消息传递和广播。实际应用中可能会更加复杂，涉及到身份验证、消息格式化、错误处理等更多功能。

## 进阶

对于进阶的 WebSocket 应用，我们可以考虑以下几个方面来增强和优化服务器端实现：

### 1. 用户身份验证

在实际应用中，你可能需要知道谁连接到了 WebSocket 服务器。这可以通过将身份验证与 WebSocket 握手过程相结合来实现。

- **JWT (JSON Web Tokens)**：客户端可以在 HTTP 升级请求的头部携带 JWT。服务器可以解析并验证这个令牌以确认用户身份。
- **Session Cookies**：如果 WebSocket 握手是通过 HTTPS 进行的，那么浏览器会自动发送 cookies。你可以使用这些 cookies 来识别用户。

### 2. 消息格式化和序列化

为了确保消息的一致性和可读性，可以定义一个标准的消息格式。例如，使用 JSON 格式来封装消息内容、类型和其他元数据。

```javascript
// 发送消息示例
ws.send(JSON.stringify({
    type: 'chat',
    content: 'Hello World!',
    timestamp: Date.now()
}));
```

### 3. 消息队列和持久化

对于重要的消息或长时间运行的应用程序，你可能希望将消息存储到数据库或者使用消息队列服务（如 RabbitMQ, Kafka）来保证消息不会丢失。

### 4. 错误处理和重连机制

构建健壮的 WebSocket 应用程序需要良好的错误处理和重连策略。服务器应该能够优雅地处理各种异常情况，并允许客户端在断开后重新建立连接。

```javascript
ws.on('error', function(error) {
    console.error('WebSocket 错误:', error);
});

// 客户端实现重连逻辑
let ws;
function initWebSocket() {
    if (ws) { ws.close(); }
    ws = new WebSocket('ws://localhost:8080');
    // ... 其他事件监听 ...
    ws.onclose = function() {
        console.log('连接已关闭，尝试重连...');
        setTimeout(initWebSocket, 5000); // 5秒后重试
    };
}
```

### 5. 性能优化

- **心跳检测**：定期发送心跳包以保持连接活跃，并检测非活动连接。
- **压缩传输**：启用 WebSocket 压缩选项来减少网络流量。
- **负载均衡**：当有大量并发连接时，可以考虑使用负载均衡器分发连接到多个服务器实例。

### 6. 高可用性和集群支持

使用 Node.js 的 `cluster` 模块或者其他工具如 PM2 可以创建多进程集群来充分利用多核 CPU，提高应用程序的性能和可靠性。

### 7. 安全性增强

- 使用 WSS（WebSocket Secure）提供加密通信。
- 实施严格的 CORS 策略，限制哪些域名可以连接到你的 WebSocket 服务器。
- 对敏感信息进行额外的安全措施，比如对聊天内容进行加密。

### 8. 监控和日志记录

设置适当的监控和日志系统可以帮助你追踪 WebSocket 服务器的状态和性能，及时发现并解决问题。

### 示例代码 - 增强版 WebSocket 服务器

这里给出一个更复杂的例子，包含了部分上述提到的功能：

```javascript
const WebSocket = require('ws');
const http = require('http');
const express = require('express');
const jwt = require('express-jwt'); // 用于验证 JWT

// 创建 Express 应用程序
const app = express();

// 配置中间件以保护 WebSocket 路由
app.use(jwt({ secret: 'your-secret-key' }).unless({ path: '/ws' }));

// 创建 HTTP 服务器
const server = http.createServer(app);

// 创建 WebSocket 服务器
const wss = new WebSocket.Server({ server });

wss.on('connection', function connection(ws, req) {
    // 解析 JWT 从请求头中获取用户信息
    const user = req.user;

    console.log(`新用户 ${user.name} 已连接`);

    // 处理消息接收
    ws.on('message', function incoming(message) {
        const msg = JSON.parse(message);
        console.log(`收到消息: ${msg.content}`);
        
        // 广播消息给所有其他用户
        broadcast(msg, ws);
    });

    ws.on('close', function close() {
        console.log(`用户 ${user.name} 断开了连接`);
    });
});

function broadcast(message, sender) {
    for (let client of wss.clients) {
        if (client !== sender && client.readyState === WebSocket.OPEN) {
            client.send(JSON.stringify(message));
        }
    }
}

// 启动服务器
server.listen(8080, () => {
    console.log('WebSocket 服务器正在运行在 ws://localhost:8080/');
});
```

请注意，上面的代码片段仅作为概念证明，并没有包含完整的错误处理、安全配置或其他生产环境中必需的最佳实践。在真实项目中，你应该根据具体需求调整和完善这些功能。
