---
title: supertest
author: pzc
date: 2024-09-26
cover: /assets/images/jpg/44.jpg
categories: [javaScript]
tags: [Test]
---
`supertest` 是一个非常流行的轻量级 Node.js 库，主要用于 HTTP 请求的测试。它通过一个简洁的 API 提供了强大的功能，使得编写 HTTP 测试变得非常简单和直观。

### 安装

首先，你需要安装 `supertest` 及其相关的依赖。如果你正在使用一个基于 Express 或者 NestJS 的项目，通常还需要安装 `@types/supertest` 以获得类型定义。

```bash
npm install supertest --save-dev
npm install @types/supertest --save-dev
```

### 基本用法

`supertest` 可以与任何 Node.js HTTP 服务器库一起使用，例如 Express、Koa、Fastify 等。以下是一个简单的例子，展示如何使用 `supertest` 测试一个 Express 应用：

#### 示例应用

假设你有一个简单的 Express 应用：

```javascript
// app.js
const express = require('express');
const app = express();

app.get('/hello', (req, res) => {
  res.send('Hello, World!');
});

module.exports = app;
```

#### 测试代码

你可以使用 `supertest` 来测试这个应用：

```javascript
// test/app.test.js
const request = require('supertest');
const app = require('../app');

describe('GET /hello', () => {
  it('should return "Hello, World!"', async () => {
    const response = await request(app).get('/hello');
    expect(response.status).toBe(200);
    expect(response.text).toBe('Hello, World!');
  });
});
```

### 主要功能

1. **发送请求**：
   - `request(app)`：创建一个请求对象，`app` 是你的 HTTP 服务器实例。
   - `get(path)`：发送 GET 请求。
   - `post(path)`：发送 POST 请求。
   - `put(path)`：发送 PUT 请求。
   - `patch(path)`：发送 PATCH 请求。
   - `delete(path)`：发送 DELETE 请求。

2. **设置请求头**：
   - `set(header, value)`：设置请求头。
   - `set(headers)`：设置多个请求头，`headers` 是一个对象。

3. **发送请求体**：
   - `send(data)`：发送请求体数据，`data` 可以是字符串、对象或缓冲区。

4. **附加文件**：
   - `attach(field, file, [filename])`：附加文件到请求体。

5. **查询参数**：
   - `query(params)`：设置查询参数，`params` 是一个对象。

6. **期望响应**：
   - `expect(status)`：期望响应状态码。
   - `expect(body)`：期望响应体。
   - `expect(header, value)`：期望响应头。
   - `expect(callback)`：期望回调函数，用于更复杂的断言。

### 高级用法

#### 链式调用

`supertest` 支持链式调用，使得代码更加简洁：

```javascript
it('should return "Hello, World!"', async () => {
  await request(app)
    .get('/hello')
    .set('Accept', 'application/json')
    .expect('Content-Type', /json/)
    .expect(200)
    .expect({ message: 'Hello, World!' });
});
```

#### 测试 POST 请求

```javascript
it('should create a new user', async () => {
  const response = await request(app)
    .post('/users')
    .send({ name: 'John Doe', email: 'john@example.com' })
    .expect(201);

  expect(response.body.name).toBe('John Doe');
  expect(response.body.email).toBe('john@example.com');
});
```

#### 测试文件上传

```javascript
it('should upload a file', async () => {
  const response = await request(app)
    .post('/upload')
    .attach('file', 'path/to/file.txt')
    .expect(200);

  expect(response.body.message).toBe('File uploaded successfully');
});
```

### 结合测试框架

`supertest` 经常与 Jest、Mocha、Chai 等测试框架一起使用。以下是一个结合 Jest 的例子：

```javascript
// test/app.test.js
const request = require('supertest');
const app = require('../app');

describe('GET /hello', () => {
  it('should return "Hello, World!"', async () => {
    const response = await request(app).get('/hello');
    expect(response.status).toBe(200);
    expect(response.text).toBe('Hello, World!');
  });
});
```

### 总结

`supertest` 是一个非常强大且易用的库，适用于各种 HTTP 测试场景。它通过简洁的 API 和链式调用方式，使得编写测试代码变得非常直观和高效。