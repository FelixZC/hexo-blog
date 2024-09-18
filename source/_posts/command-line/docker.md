---
title: Docker命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Docker,Server]
---
Docker 是一个开源的应用容器引擎，可以让开发者打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器或 Windows 机器上，也可以实现虚拟化。下面是一些常用的 Docker 命令，可以帮助你管理和操作 Docker 容器及镜像：

### 基础命令

- **获取帮助**
  - `docker --help`：显示 Docker 的所有可用命令。
  - `docker [command] --help`：显示特定命令的帮助信息。

- **版本信息**
  - `docker version`：显示 Docker 版本信息。

### 镜像管理

- **搜索镜像**
  - `docker search [image-name]`：在 Docker Hub 搜索镜像。

- **下载镜像**
  - `docker pull [image-name]`：从仓库下载镜像到本地。

- **列出镜像**
  - `docker images`：列出本地已有的镜像。

- **构建镜像**
  - `docker build -t [tag-name] .`：使用 Dockerfile 构建镜像，`.` 表示 Dockerfile 在当前目录下。

- **删除镜像**
  - `docker rmi [image-id]`：删除本地指定的镜像。
  - `docker rmi $(docker images -q)`：删除所有本地镜像。

### 容器管理

- **运行容器**
  - `docker run -d -p [host-port]:[container-port] [image-name]`：以后台模式运行容器，并映射端口。
  - `docker run -it [image-name] /bin/bash`：以交互模式运行容器，并启动 bash。

- **列出容器**
  - `docker ps`：列出所有正在运行的容器。
  - `docker ps -a`：列出所有容器，包括停止的。

- **停止/启动/重启容器**
  - `docker stop [container-id]`：停止一个运行中的容器。
  - `docker start [container-id]`：启动一个已停止的容器。
  - `docker restart [container-id]`：重启容器。

- **删除容器**
  - `docker rm [container-id]`：删除一个或多个容器。
  - `docker rm $(docker ps -a -q)`：删除所有容器。

- **查看容器日志**
  - `docker logs [container-id]`：查看容器的日志输出。

- **执行命令**
  - `docker exec -it [container-id] /bin/bash`：在运行中的容器内执行命令。

### 其他常用命令

- **导出容器为 tar 文件**
  - `docker export [container-id] > container.tar`：将容器导出为 tar 文件。

- **导入 tar 文件为镜像**
  - `cat container.tar | docker import - [image-name]`：从 tar 文件导入镜像。

- **查看系统信息**
  - `docker info`：显示 Docker 系统的信息，包括使用的存储驱动等。

- **清理未使用的资源**
  - `docker system prune`：清理所有未使用的容器、网络、镜像（包括未被任何标签引用的悬空镜像）。

这些命令覆盖了 Docker 日常使用中的大多数场景，但 Docker 功能强大，还有许多高级特性和配置选项可以探索。