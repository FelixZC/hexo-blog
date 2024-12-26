---
title: cross-env
author: pzc
date: 2024-12-26
cover: /assets/images/jpg/132.jpg
categories: [nodejs]
tags: [Env]
---
# cross-env

## 介绍

`cross-env` 是一个用于在不同环境（如 Windows、macOS 和 Linux）之间设置进程环境变量的小型工具。它特别适用于那些需要跨平台兼容性的 Node.js 项目，因为它可以确保你在所有平台上使用相同的命令来设置环境变量。

通常情况下，在 Unix 系统（如 macOS 和 Linux）上，你可以直接在命令行中设置环境变量，例如：

```sh
NODE_ENV=production node app.js
```

然而，在 Windows 上，上述命令并不会按预期工作。为了解决这个问题，你可以使用 `cross-env` 包，它允许你以一种跨平台的方式设置环境变量。使用 `cross-env` 的命令看起来像这样：

```sh
cross-env NODE_ENV=production node app.js
```

无论是在哪个操作系统上执行上面的命令，`cross-env` 都会正确地设置 `NODE_ENV` 环境变量，并运行 `node app.js`。

要安装 `cross-env`，你可以使用 npm 或 yarn：

```sh
npm install --save-dev cross-env
# 或者
yarn add --dev cross-env
```

一旦安装完成，你就可以在你的构建脚本或者开发环境中使用它了。

## 资料

如果你需要关于 `cross-env` 或者其他开发工具的更详细资料，这里有几种获取信息的方式：

1. **官方文档和GitHub仓库**：
   - `cross-env` 的官方 GitHub 仓库是获取最新信息、使用说明、版本更新以及问题报告的最佳地点。你可以访问 [cross-env GitHub](https://github.com/kentcdodds/cross-env) 查看详细的README文件和其他资源。

2. **npm 页面**：
   - 每个 npm 包都有自己的页面，包含包的描述、安装指南、版本历史等。`cross-env` 的 npm 页面可以在 [npmjs.com](https://www.npmjs.com/package/cross-env) 找到。

3. **在线教程和博客文章**：
   - 许多开发者会在他们的博客上分享如何使用特定工具的经验。对于 `cross-env`，你可能会找到一些解释如何配置它来适应不同开发场景的文章。

4. **社区和支持论坛**：
   - Stack Overflow 和 Reddit 等网站上有活跃的开发者社区，你可以在这里提问或查找与 `cross-env` 相关的问题和答案。
   - 此外，GitHub Issues 页面也是寻求帮助的地方，尤其是当你遇到可能是bug的问题时。

5. **书籍和视频课程**：
   - 对于一些流行的工具和技术栈，会有专门的书籍或者视频课程深入讲解。虽然针对 `cross-env` 可能不会有专门的书籍，但有关 Node.js 和环境配置的资源通常会提及它。

## 进阶

如果你对 `cross-env` 的使用已经有一定了解，并希望深入探讨更高级的用法或相关主题，这里有一些进阶的内容供你参考：

### 1. 复杂环境变量设置
除了简单的键值对设置，`cross-env` 还支持更复杂的环境变量配置。例如，可以设置多个环境变量，或者将一个环境变量的值设置为其他环境变量的组合。

```sh
cross-env API_URL=https://api.example.com BASE_URL=https://example.com node app.js
```

甚至可以进行一些基本的字符串操作：

```sh
cross-env BASE_URL=https://example.com API_URL=${BASE_URL}/api node app.js
```

### 2. 使用 `.env` 文件
虽然 `cross-env` 本身不直接处理 `.env` 文件，但你可以结合 `dotenv` 包来加载 `.env` 文件中的环境变量。这在开发环境中特别有用，因为它允许你将敏感信息保存在文件中而不必硬编码到代码里。

安装 `dotenv`:

```sh
npm install dotenv --save-dev
```

然后，在你的应用程序入口处添加以下代码来加载 `.env` 文件：

```js
require('dotenv').config();
```

### 3. 集成 CI/CD 流水线
当你在持续集成和持续部署（CI/CD）流水线中使用 `cross-env` 时，确保它能够正确地与不同的平台和服务提供商协同工作。许多 CI/CD 工具都有自己的方式来管理环境变量，所以你可能需要调整 `cross-env` 的使用方式以适应这些工具。

### 4. 环境变量加密
对于包含敏感数据的环境变量，考虑使用加密存储解决方案。例如，AWS Secrets Manager、Azure Key Vault 或者 HashiCorp Vault 可以安全地存储和检索敏感信息。你可以在应用启动时通过 API 调用来获取解密后的值，并使用 `cross-env` 设置它们。

### 5. 自动化脚本
编写自动化脚本来简化复杂环境的设置。例如，你可以创建一个 npm 脚本来同时设置多个环境变量并启动应用程序：

```json
"scripts": {
  "start:prod": "cross-env NODE_ENV=production API_URL=https://api.prod.com node app.js"
}
```

### 6. 环境变量调试
为了更容易地调试环境变量问题，可以在应用程序中打印出所有当前的环境变量。Node.js 提供了 `process.env` 对象来访问环境变量，因此你可以简单地将它们打印出来：

```js
console.log(process.env);
```

或者，仅打印特定的环境变量：

```js
console.log('NODE_ENV:', process.env.NODE_ENV);
```

### 7. 版本控制和跨版本兼容性
确保你的项目依赖项（包括 `cross-env`）保持最新，但也要注意不要引入破坏性的变更。查看 `cross-env` 的发布说明，了解每个新版本带来的改动，并根据需要更新你的项目。

## 示例

下面我将提供一个使用 `cross-env` 的完整示例，包括项目设置、`.env` 文件的使用以及如何在 CI/CD 流水线中集成。这个例子假设你正在构建一个简单的 Node.js 应用程序，并希望确保环境变量配置可以在不同平台上顺利工作。

### 项目初始化

首先，创建一个新的 Node.js 项目并安装必要的依赖：

```sh
mkdir my-node-app
cd my-node-app
npm init -y
npm install --save-dev cross-env dotenv
```

### 创建 `.env` 文件

在项目根目录下创建一个 `.env` 文件来保存环境变量。对于生产环境和开发环境，你可以创建两个不同的文件，例如 `.env.development` 和 `.env.production`。

```plaintext
# .env.development
NODE_ENV=development
API_URL=http://localhost:3001
BASE_URL=http://localhost:3000

# .env.production
NODE_ENV=production
API_URL=https://api.example.com
BASE_URL=https://example.com
```

### 修改 `package.json` 添加脚本

编辑你的 `package.json` 文件，添加启动脚本以加载 `.env` 文件，并使用 `cross-env` 设置环境变量。

```json
{
  "name": "my-node-app",
  "version": "1.0.0",
  "scripts": {
    "start": "cross-env NODE_ENV=development node index.js",
    "start:prod": "cross-env NODE_ENV=production node index.js"
  },
  "devDependencies": {
    "cross-env": "^7.0.3",
    "dotenv": "^16.0.3"
  }
}
```

### 创建应用入口文件

创建一个名为 `index.js` 的文件作为应用程序的入口点。在这个文件里，我们将引入 `dotenv` 并根据当前的工作目录加载相应的 `.env` 文件。

```js
// index.js
require('dotenv').config({
  path: `.env.${process.env.NODE_ENV || 'development'}`
});

const express = require('express');
const app = express();
const port = process.env.PORT || 3000;

app.get('/', (req, res) => {
  res.send(`Hello World! Running in ${process.env.NODE_ENV} mode.`);
});

app.listen(port, () => {
  console.log(`Server running at http://${process.env.BASE_URL}:${port}`);
});
```

注意：如果你还没有安装 Express，请先通过 `npm install express` 安装它。

### 运行应用

现在你可以运行你的应用了。使用以下命令来启动开发服务器：

```sh
npm start
```

或者，为了模拟生产环境，你可以运行：

```sh
npm run start:prod
```

### 集成 CI/CD 流水线

假设你在 GitHub 上使用 GitHub Actions 作为 CI/CD 工具，可以创建一个 `.github/workflows/ci.yml` 文件来定义流水线步骤。你需要确保流水线中的环境变量与本地一致。 

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - name: Install dependencies
        run: npm ci
      - name: Start server
        run: npm run start:prod
        env:
          NODE_ENV: production
          API_URL: https://api.example.com
          BASE_URL: https://example.com
```

这个 CI/CD 流水线会在每次推送到 `main` 分支或创建拉取请求时触发，它会安装依赖项并以生产模式启动服务器。

### 总结

以上是一个完整的示例，展示了如何使用 `cross-env` 来管理不同平台上的环境变量，结合 `.env` 文件进行环境配置，并将其集成到 CI/CD 流水线中。这个示例涵盖了从项目初始化到部署的全过程，适用于大多数 Node.js 应用程序。