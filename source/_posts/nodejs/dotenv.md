---
title: dotenv
author: pzc
date: 2024-09-20
cover: /assets/images/jpg/31.jpg
categories: [nodejs]
tags: [Env]
---

`dotenv` 是一个用于Node.js的零依赖模块，它可以帮助开发者轻松地加载环境变量到进程环境中。通常这些环境变量存储在一个名为 `.env` 的文件中，这个文件不会被提交到版本控制系统（如Git）中，以避免敏感信息泄露。这种方式在开发和部署应用时非常有用，因为它允许开发者为不同的环境设置不同的配置，而无需更改代码。

### 安装

要使用 `dotenv`，首先需要通过npm（Node包管理器）安装它。打开命令行工具，进入你的项目目录，然后运行以下命令：

```bash
npm install dotenv
```

### 使用

安装完成后，在你的应用程序中引入 `dotenv` 模块，并调用 `.config()` 方法来加载 `.env` 文件中的变量。这通常在应用的入口文件（如 `app.js` 或 `index.js`）中完成，以确保所有后续的代码都可以访问这些环境变量。

```javascript
require('dotenv').config();

console.log(process.env.DATABASE_URL); // 输出 .env 文件中定义的 DATABASE_URL 变量值
```

### .env 文件格式

`.env` 文件是一个简单的文本文件，其中每一行定义了一个环境变量。变量名和值之间用等号 `=` 分隔。例如：

```
DATABASE_URL=mongodb://localhost:27017/mydatabase
SECRET_KEY=your_secret_key_here
```

### 注意事项

- **安全性**：不要在 `.env` 文件中存储密码或API密钥等敏感信息，除非你确信该文件不会被泄露。确保将 `.env` 文件添加到 `.gitignore` 文件中，防止意外提交到公共仓库。
- **类型转换**：从 `.env` 文件读取的所有值都是字符串形式。如果需要其他数据类型（如数字或布尔值），你需要手动进行转换。
- **环境特定配置**：对于不同环境（如开发、测试、生产）有不同的配置需求时，可以考虑使用多个 `.env` 文件，如 `.env.development` 和 `.env.production`。`dotenv` 支持通过 `path` 参数指定不同的文件路径。

总之，`dotenv` 是一个简单而强大的工具，有助于管理和保护应用的配置信息，提高开发效率和安全性。