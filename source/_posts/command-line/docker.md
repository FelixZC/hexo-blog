---
title: Docker命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Docker,Server]
---
Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器或 Windows 机器上，也可以实现虚拟化。以下是一些常用的 Docker 命令行操作：

### 镜像管理

- **搜索镜像**：
  ```bash
  docker search [镜像名称]
  ```

- **拉取镜像**：
  ```bash
  docker pull [镜像名称]:[标签]
  ```

- **列出本地镜像**：
  ```bash
  docker images
  ```

- **删除镜像**：
  ```bash
  docker rmi [镜像ID]
  ```

- **构建镜像**：
  ```bash
  docker build -t [用户名]/[镜像名称]:[标签] .
  ```

### 容器管理

- **运行容器**：
  ```bash
  docker run -d -p [宿主机端口]:[容器端口] --name [容器名] [镜像名称]
  ```
  - `-d` 后台运行
  - `-p` 端口映射
  - `--name` 指定容器名称

- **列出所有运行中的容器**：
  ```bash
  docker ps
  ```

- **列出所有容器（包括停止的）**：
  ```bash
  docker ps -a
  ```

- **停止容器**：
  ```bash
  docker stop [容器ID/容器名]
  ```

- **启动已停止的容器**：
  ```bash
  docker start [容器ID/容器名]
  ```

- **重启容器**：
  ```bash
  docker restart [容器ID/容器名]
  ```

- **删除容器**：
  ```bash
  docker rm [容器ID/容器名]
  ```

- **强制删除容器**：
  ```bash
  docker rm -f [容器ID/容器名]
  ```

- **进入容器**：
  ```bash
  docker exec -it [容器ID/容器名] /bin/bash
  ```

### 数据卷管理

- **创建数据卷**：
  ```bash
  docker volume create [数据卷名称]
  ```

- **列出所有数据卷**：
  ```bash
  docker volume ls
  ```

- **删除数据卷**：
  ```bash
  docker volume rm [数据卷名称]
  ```

### 网络管理

- **创建网络**：
  ```bash
  docker network create [网络名称]
  ```

- **列出所有网络**：
  ```bash
  docker network ls
  ```

- **删除网络**：
  ```bash
  docker network rm [网络名称]
  ```

- **连接容器到网络**：
  ```bash
  docker network connect [网络名称] [容器名称]
  ```

- **断开容器与网络的连接**：
  ```bash
  docker network disconnect [网络名称] [容器名称]
  ```

- **创建自定义桥接网络**：
  ```bash
  docker network create --driver bridge [网络名称]
  ```

- **创建覆盖网络**（Swarm 模式下）：
  ```bash
  docker network create --driver overlay [网络名称]
  ```

- **连接容器到多个网络**：
  ```bash
  docker network connect [网络名称] [容器名称]
  ```


### 其他常用命令

- **查看容器日志**：
  ```bash
  docker logs [容器ID/容器名]
  ```

- **查看容器运行信息**：
  ```bash
  docker inspect [容器ID/容器名]
  ```

- **查看Docker系统信息**：
  ```bash
  docker info
  ```

- **清理未使用的资源**：
  ```bash
  docker system prune
  ```

### 更多镜像管理

- **标记镜像**：
  ```bash
  docker tag [源镜像ID] [仓库名]:[标签]
  ```

- **推送镜像到仓库**：
  ```bash
  docker push [仓库名]:[标签]
  ```

- **列出悬空镜像**（没有标签的镜像）：
  ```bash
  docker images -f "dangling=true"
  ```

- **删除悬空镜像**：
  ```bash
  docker rmi $(docker images -f "dangling=true" -q)
  ```

### 更多容器管理

- **查看容器的实时资源使用情况**：
  ```bash
  docker stats [容器ID/容器名]
  ```

- **复制文件从容器到主机**：
  ```bash
  docker cp [容器ID/容器名]:[容器内路径] [主机路径]
  ```

- **复制文件从主机到容器**：
  ```bash
  docker cp [主机路径] [容器ID/容器名]:[容器内路径]
  ```

- **暂停容器的所有进程**：
  ```bash
  docker pause [容器ID/容器名]
  ```

- **恢复容器的所有进程**：
  ```bash
  docker unpause [容器ID/容器名]
  ```

- **导出容器为 tar 文件**：
  ```bash
  docker export [容器ID] > container.tar
  ```

- **从 tar 文件导入容器**：
  ```bash
  cat container.tar | docker import - [镜像名]:[标签]
  ```

### Docker Compose

Docker Compose 是一个用于定义和运行多容器 Docker 应用程序的工具。通过一个 YAML 文件来配置应用程序的服务。

- **启动服务**：
  ```bash
  docker-compose up
  ```

- **后台启动服务**：
  ```bash
  docker-compose up -d
  ```

- **停止服务**：
  ```bash
  docker-compose down
  ```

- **重建服务**：
  ```bash
  docker-compose up --build
  ```

### Docker Swarm

Docker Swarm 是 Docker 的原生集群管理和编排工具。

- **初始化 Swarm**：
  ```bash
  docker swarm init
  ```

- **加入节点到 Swarm**：
  ```bash
  docker swarm join --token [TOKEN] [MANAGER-IP]:[MANAGER-PORT]
  ```

- **部署服务到 Swarm**：
  ```bash
  docker service create --replicas 1 --name [服务名] [镜像名]
  ```

- **更新服务**：
  ```bash
  docker service update --image [新镜像名] [服务名]
  ```

- **列出所有服务**：
  ```bash
  docker service ls
  ```

- **删除服务**：
  ```bash
  docker service rm [服务名]
  ```

### Docker 安全性

- **限制容器的资源使用**（如 CPU 和内存）：
  ```bash
  docker run -m 512m --cpus="1.5" [镜像名]
  ```

- **设置容器的安全选项**（如 SELinux 标签）：
  ```bash
  docker run --security-opt label=disable [镜像名]
  ```

这些命令是使用 Docker 进行日常开发和运维的基础。根据不同的场景，可能还需要更多的高级命令和配置来满足特定的需求。