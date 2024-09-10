# 我的Hexo博客

[![Build Status](https://travis-ci.org/hexojs/hexo.svg?branch=master)](https://travis-ci.org/hexojs/hexo)
[![GitHub license](https://img.shields.io/github/license/Naereen/StrapDown.js.svg)](https://github.com/hexojs/hexo/blob/master/LICENSE)

## 项目简介

这是一个基于 [Hexo](https://hexo.io/) 构建的静态网站生成器的个人博客项目。它使用了 [flexblock主题](https://github.com/miiiku/hexo-theme-flexblock) 作为前端样式框架，并且包含了基本的配置来快速启动一个具有丰富功能的博客站点。

## 目录结构

```
my-hexo-blog/
├── _config.yml            # Hexo 配置文件
├── source/                # 源文件目录
│   ├── _posts/            # 博客文章存放目录
│   └── _data/             # 数据文件（如友情链接等）
├── public/                # 编译后的文件存放目录
├── themes/                # 主题文件存放目录
│   └── flexblock/              # flexblock主题目录
└── package.json           # Node.js 包管理文件
```

## 安装与运行

确保你的机器上已经安装了 Node.js 和 npm。然后按照以下步骤操作：

1. 克隆此仓库到本地：
    ```bash
    git clone https://github.com/FelixZC/hexo-blog
    cd my-hexo-blog
    ```

2. 安装依赖包：
    ```bash
    npm install
    ```

3. 启动本地服务器进行开发测试：
    ```bash
    hexo server
    ```
    访问 http://localhost:4000 查看你的博客。

4. 生成静态文件：
    ```bash
    hexo generate
    ```
    编译后的文件会存放在 `public` 目录下，可以直接部署到任何支持静态文件的服务器上。

## 贡献指南

如果你发现了任何错误或有好的建议，请通过提交 Issue 或 Pull Request 的方式贡献代码。请确保遵守项目中的编码规范。