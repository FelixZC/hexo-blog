---
title: Jest命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Jest,Test]
---
Jest 是一个流行的 JavaScript 测试框架，广泛用于单元测试、集成测试和端到端测试。以下是 Jest 的一些常用命令，可以帮助你管理和运行测试。

### 基础命令

- **安装 Jest**
  - 使用 npm：
    ```sh
    npm install --save-dev jest
    ```
  - 使用 yarn：
    ```sh
    yarn add --dev jest
    ```

- **初始化 Jest 配置文件**
  - Jest 会自动查找 `package.json` 中的 `jest` 字段或 `jest.config.js` 文件。如果没有配置文件，可以手动创建：
    ```js
    // jest.config.js
    module.exports = {
      testEnvironment: 'node',
      moduleFileExtensions: ['js', 'json', 'ts'],
      rootDir: 'src',
      testRegex: '.spec.ts$',
      transform: {
        '^.+\\.(t|j)s$': 'ts-jest',
      },
    };
    ```

### 运行测试

- **运行所有测试**
  - 使用 npm：
    ```sh
    npx jest
    ```
  - 使用 yarn：
    ```sh
    yarn jest
    ```

- **运行指定测试文件**
  - ```sh
    npx jest path/to/test.spec.js
    ```

- **运行匹配特定模式的测试文件**
  - ```sh
    npx jest 'pattern'
    ```

- **运行指定测试套件**
  - ```sh
    npx jest --testPathPattern=path/to/suite
    ```

- **运行指定测试用例**
  - ```sh
    npx jest --testNamePattern='test name'
    ```

### 交互式模式

- **进入交互式模式**
  - ```sh
    npx jest --watch
    ```
  - 这将启动一个交互式界面，允许你选择要运行的测试文件。

- **只运行更改的测试**
  - ```sh
    npx jest --watchAll
    ```
  - 这将监视文件更改并自动运行受影响的测试。

### 覆盖率报告

- **生成覆盖率报告**
  - ```sh
    npx jest --coverage
    ```
  - 这将生成一个覆盖率报告，默认保存在 `coverage/` 目录下。

- **指定覆盖率报告格式**
  - ```sh
    npx jest --coverage --coverageReporters=text
    ```
  - 支持的报告格式有 `text`, `lcov`, `html`, `clover` 等。

### 调试

- **调试测试**
  - 使用 Node.js 的调试器：
    ```sh
    node --inspect-brk node_modules/.bin/jest --runInBand
    ```
  - 使用 VSCode 的调试配置：
    ```json
    {
      "version": "0.2.0",
      "configurations": [
        {
          "type": "node",
          "request": "launch",
          "name": "Jest Current File",
          "program": "${workspaceFolder}/node_modules/.bin/jest",
          "args": ["${fileBasenameNoExtension}"],
          "console": "integratedTerminal",
          "internalConsoleOptions": "neverOpen",
          "disableOptimisticBPs": true,
          "windows": {
            "program": "${workspaceFolder}/node_modules/jest/bin/jest.js"
          }
        }
      ]
    }
    ```

### 高级选项

- **更新快照**
  - ```sh
    npx jest -u
    ```
  - 这将更新所有失败的快照。

- **指定配置文件**
  - ```sh
    npx jest --config jest.config.js
    ```

- **指定环境变量**
  - ```sh
    ENV=production npx jest
    ```

- **指定测试超时时间**
  - ```sh
    npx jest --maxWorkers=2 --timeout=60000
    ```

- **指定测试重试次数**
  - ```sh
    npx jest --retryTimes=3
    ```

### 清理

- **清除缓存**
  - ```sh
    npx jest --clearCache
    ```
  - 这将删除 Jest 的缓存目录，通常为 `node_modules/.cache/jest`。

### 示例

假设你有一个项目结构如下：

```
my-project/
├── src/
│   ├── components/
│   │   └── Button/
│   │       └── Button.test.js
├── jest.config.js
└── package.json
```

你可以使用以下命令来运行测试：

- **运行所有测试**
  ```sh
  npx jest
  ```

- **运行特定测试文件**
  ```sh
  npx jest src/components/Button/Button.test.js
  ```

- **生成覆盖率报告**
  ```sh
  npx jest --coverage
  ```

- **进入交互式模式**
  ```sh
  npx jest --watch
  ```

- **更新快照**
  ```sh
  npx jest -u
  ```

这些命令涵盖了 Jest 的大多数常用功能。