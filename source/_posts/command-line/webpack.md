---
title: Webpack命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Webpack,Package]
---
Webpack 是一个模块打包工具，广泛用于现代 Web 应用的开发。它可以通过配置文件（`webpack.config.js`）来管理项目的构建过程。以下是一些常用的 Webpack 命令，可以帮助你管理和构建项目。

### 基础命令

- **安装 Webpack 和 Webpack CLI**
  - 使用 npm：
    ```sh
    npm install --save-dev webpack webpack-cli
    ```
  - 使用 yarn：
    ```sh
    yarn add --dev webpack webpack-cli
    ```

- **初始化项目**
  - 创建 `webpack.config.js` 文件来配置 Webpack：
    ```js
    const path = require('path');

    module.exports = {
      entry: './src/index.js',
      output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
      },
      module: {
        rules: [
          {
            test: /\.js$/,
            exclude: /node_modules/,
            use: {
              loader: 'babel-loader'
            }
          },
          {
            test: /\.css$/,
            use: ['style-loader', 'css-loader']
          }
        ]
      },
      plugins: [],
      mode: 'development'
    };
    ```

### 构建和运行

- **基本构建**
  - 使用 npm：
    ```sh
    npx webpack
    ```
  - 使用 yarn：
    ```sh
    yarn webpack
    ```

- **指定配置文件**
  - ```sh
    npx webpack --config webpack.config.js
    ```

- **指定输出目录**
  - ```sh
    npx webpack --output-path ./dist
    ```

- **指定入口文件**
  - ```sh
    npx webpack --entry ./src/index.js
    ```

- **指定输出文件名**
  - ```sh
    npx webpack --output-filename bundle.js
    ```

### 开发模式

- **启动开发服务器**
  - 首先安装 `webpack-dev-server`：
    ```sh
    npm install --save-dev webpack-dev-server
    ```
  - 然后在 `package.json` 中添加启动脚本：
    ```json
    {
      "scripts": {
        "start": "webpack serve --open"
      }
    }
    ```
  - 启动开发服务器：
    ```sh
    npm start
    ```

- **热模块替换（HMR）**
  - 在 `webpack.config.js` 中启用 HMR：
    ```js
    module.exports = {
      // 其他配置...
      devServer: {
        hot: true
      }
    };
    ```

### 生产模式

- **生产模式构建**
  - 使用 npm：
    ```sh
    npx webpack --mode production
    ```
  - 使用 yarn：
    ```sh
    yarn webpack --mode production
    ```

- **代码分割**
  - 在 `webpack.config.js` 中配置代码分割：
    ```js
    module.exports = {
      // 其他配置...
      optimization: {
        splitChunks: {
          chunks: 'all'
        }
      }
    };
    ```

- **Tree Shaking**
  - 确保使用 ES6 模块语法，并在 `webpack.config.js` 中启用 Tree Shaking：
    ```js
    module.exports = {
      // 其他配置...
      mode: 'production',
      optimization: {
        usedExports: true
      }
    };
    ```

### 插件和加载器

- **安装插件和加载器**
  - 使用 npm：
    ```sh
    npm install --save-dev html-webpack-plugin babel-loader
    ```
  - 使用 yarn：
    ```sh
    yarn add --dev html-webpack-plugin babel-loader
    ```

- **配置插件和加载器**
  - 在 `webpack.config.js` 中配置插件和加载器：
    ```js
    const HtmlWebpackPlugin = require('html-webpack-plugin');
    const path = require('path');

    module.exports = {
      entry: './src/index.js',
      output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
      },
      module: {
        rules: [
          {
            test: /\.js$/,
            exclude: /node_modules/,
            use: {
              loader: 'babel-loader'
            }
          },
          {
            test: /\.css$/,
            use: ['style-loader', 'css-loader']
          }
        ]
      },
      plugins: [
        new HtmlWebpackPlugin({
          template: './src/index.html'
        })
      ],
      mode: 'development'
    };
    ```

### 调试和日志

- **查看详细日志**
  - 使用 `--display-error-details` 选项：
    ```sh
    npx webpack --display-error-details
    ```

- **启用性能提示**
  - 在 `webpack.config.js` 中启用性能提示：
    ```js
    module.exports = {
      // 其他配置...
      performance: {
        hints: 'warning', // 或 'error'
        maxAssetSize: 2000000, // 2MB
        maxEntrypointSize: 4000000 // 4MB
      }
    };
    ```

### 其他实用命令

- **生成统计报告**
  - 使用 `--profile` 和 `--json` 选项生成统计报告：
    ```sh
    npx webpack --profile --json > stats.json
    ```
  - 使用 `webpack-bundle-analyzer` 分析报告：
    ```sh
    npm install --save-dev webpack-bundle-analyzer
    ```
    ```js
    const { BundleAnalyzerPlugin } = require('webpack-bundle-analyzer');

    module.exports = {
      // 其他配置...
      plugins: [
        new BundleAnalyzerPlugin()
      ]
    };
    ```

- **清理输出目录**
  - 使用 `clean-webpack-plugin` 清理输出目录：
    ```sh
    npm install --save-dev clean-webpack-plugin
    ```
    ```js
    const { CleanWebpackPlugin } = require('clean-webpack-plugin');

    module.exports = {
      // 其他配置...
      plugins: [
        new CleanWebpackPlugin()
      ]
    };
    ```

### 示例

假设你有一个名为 `my-webpack-app` 的 Webpack 项目，你可以使用以下命令来管理和运行项目：

- **安装 Webpack 和 Webpack CLI**
  ```sh
  npm install --save-dev webpack webpack-cli
  ```

- **创建配置文件**
  ```js
  // webpack.config.js
  const path = require('path');

  module.exports = {
    entry: './src/index.js',
    output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'dist')
    },
    module: {
      rules: [
        {
          test: /\.js$/,
          exclude: /node_modules/,
          use: {
            loader: 'babel-loader'
          }
        },
        {
          test: /\.css$/,
          use: ['style-loader', 'css-loader']
        }
      ]
    },
    plugins: [],
    mode: 'development'
  };
  ```

- **安装依赖**
  ```sh
  npm install
  ```

- **启动开发服务器**
  ```sh
  npx webpack serve --open
  ```

- **生产模式构建**
  ```sh
  npx webpack --mode production
  ```

- **生成统计报告**
  ```sh
  npx webpack --profile --json > stats.json
  ```

这些命令涵盖了 Webpack 的大多数常用功能。