---
title: Vite命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Vite,Server,Package]
---
Vite 是一个由 Vue.js 作者尤雨溪开发的现代前端构建工具，它利用原生 ES 模块导入来提供更快的开发服务器启动时间和更快的热更新。以下是 Vite 的一些常用命令，可以帮助你管理和运行项目。

### 基础命令

- **安装 Vite**
  - 使用 npm：
    ```sh
    npm install -g create-vite
    ```
  - 使用 yarn：
    ```sh
    yarn global add create-vite
    ```

- **创建新项目**
  - 使用 npm：
    ```sh
    npm create vite@latest my-vue-app --template vue
    ```
  - 使用 yarn：
    ```sh
    yarn create vite my-vue-app --template vue
    ```

  可用的模板包括：
  - `vue`：Vue 3 单文件组件 (SFC) 项目
  - `react`：React 项目
  - `preact`：Preact 项目
  - `vanilla`：纯 JavaScript 项目
  - `vanilla-ts`：纯 TypeScript 项目

### 项目管理

- **安装项目依赖**
  - 使用 npm：
    ```sh
    cd my-vue-app
    npm install
    ```
  - 使用 yarn：
    ```sh
    cd my-vue-app
    yarn
    ```

- **启动开发服务器**
  - 使用 npm：
    ```sh
    npm run dev
    ```
  - 使用 yarn：
    ```sh
    yarn dev
    ```

  这将启动 Vite 开发服务器，并在浏览器中打开项目。

### 构建和部署

- **构建项目**
  - 使用 npm：
    ```sh
    npm run build
    ```
  - 使用 yarn：
    ```sh
    yarn build
    ```

  这将生成生产环境的静态文件，通常位于 `dist/` 目录下。

- **预览构建结果**
  - 使用 npm：
    ```sh
    npm run preview
    ```
  - 使用 yarn：
    ```sh
    yarn preview
    ```

  这将启动一个本地服务器来预览构建结果，方便在部署前进行检查。

### 配置

- **编辑配置文件**
  - Vite 的配置文件通常是 `vite.config.js` 或 `vite.config.ts`。你可以在这个文件中配置各种选项，如别名、代理、插件等。

  示例配置文件：
  ```js
  // vite.config.js
  import { defineConfig } from 'vite';
  import vue from '@vitejs/plugin-vue';

  export default defineConfig({
    plugins: [vue()],
    server: {
      port: 3000,
      open: true,
      proxy: {
        '/api': 'http://localhost:3001',
      },
    },
    resolve: {
      alias: {
        '@': '/src',
      },
    },
  });
  ```

### 插件管理

- **安装插件**
  - 使用 npm：
    ```sh
    npm install @vitejs/plugin-vue
    ```
  - 使用 yarn：
    ```sh
    yarn add @vitejs/plugin-vue
    ```

  在 `vite.config.js` 中使用插件：
  ```js
  import { defineConfig } from 'vite';
  import vue from '@vitejs/plugin-vue';

  export default defineConfig({
    plugins: [vue()],
  });
  ```

### 调试和日志

- **查看详细日志**
  - 启动开发服务器时，Vite 会显示详细的日志信息。如果需要更多调试信息，可以在 `vite.config.js` 中配置日志级别：
  ```js
  import { defineConfig } from 'vite';

  export default defineConfig({
    server: {
      logLevel: 'info', // 可选值：'silent', 'error', 'warn', 'info', 'debug'
    },
  });
  ```

### 其他实用命令

- **生成类型定义文件**
  - 如果你在使用 TypeScript，可以生成类型定义文件：
  ```sh
  npx tsc --init
  ```

- **运行自定义脚本**
  - 你可以在 `package.json` 中定义自定义脚本：
  ```json
  {
    "scripts": {
      "dev": "vite",
      "build": "vite build",
      "preview": "vite preview",
      "lint": "eslint ."
    }
  }
  ```

  运行自定义脚本：
  ```sh
  npm run lint
  ```

### 示例

假设你有一个名为 `my-vue-app` 的 Vite 项目，你可以使用以下命令来管理和运行项目：

- **创建新项目**
  ```sh
  npm create vite@latest my-vue-app --template vue
  ```

- **安装项目依赖**
  ```sh
  cd my-vue-app
  npm install
  ```

- **启动开发服务器**
  ```sh
  npm run dev
  ```

- **构建项目**
  ```sh
  npm run build
  ```

- **预览构建结果**
  ```sh
  npm run preview
  ```

- **编辑配置文件**
  ```js
  // vite.config.js
  import { defineConfig } from 'vite';
  import vue from '@vitejs/plugin-vue';

  export default defineConfig({
    plugins: [vue()],
    server: {
      port: 3000,
      open: true,
      proxy: {
        '/api': 'http://localhost:3001',
      },
    },
    resolve: {
      alias: {
        '@': '/src',
      },
    },
  });
  ```

这些命令涵盖了 Vite 的大多数常用功能。