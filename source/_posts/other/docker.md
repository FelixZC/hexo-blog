---
title: docker相关
author: pzc
date: 2024-09-14
cover: /assets/images/jpg/25.jpg
categories: [other]
tags: [Docker]
---
## 介绍

Docker 是一个开源的应用容器引擎，基于 Go 语言并遵从 Apache2.0 授权协议。Docker 可以让开发者打包应用及其依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互隔离，互不影响，从而可以保证程序的一致性与隔离性。

以下是 Docker 的一些关键概念：

- **镜像 (Image)**: 镜像是创建容器的基础。它是一个只读模板，可以理解为一个轻量级、可执行的独立软件包，包含了运行该软件所需的所有内容（代码、运行时、库、环境变量和其他依赖）。

- **容器 (Container)**: 容器是由镜像创建的一个运行实例。容器几乎是一个完整的操作系统环境，但是它比虚拟机更轻量，因为容器共享主机操作系统的资源而不是自带一个完整的操作系统。

- **仓库 (Registry)**: Docker 使用仓库的概念来存储镜像。这些仓库可以是公开的或私有的，最著名的公共仓库叫做 Docker Hub。

- **Dockerfile**: 这是一个文本文件，包含了所有构建一个镜像所需的命令。用户可以通过这个文件来自动化地构建一个镜像。

Docker 提供了标准化的方法来开发、打包、运行应用程序，使得它们可以在任何地方运行。这为开发人员提供了一种在他们自己的笔记本电脑上构建和测试应用程序的方式，并确保其在生产环境中能够正常工作。

Docker 有以下几个主要特点：
- 轻量级：相比传统虚拟机，Docker 容器启动速度更快，占用资源更少；
- 可移植性：Docker 容器可以很容易地从一台机器迁移到另一台机器；
- 一致性和隔离性：Docker 确保了应用的一致性和隔离性，有助于减少“它在我的机器上可以工作”之类的问题；
- 易于定义开发环境：通过 Dockerfile 文件可以很容易地定义一个应用的服务依赖、环境变量等。

Docker 已经成为开发和运维（DevOps）领域中的重要工具，尤其是在云计算和微服务架构中。

## 资源

Docker 官方网站提供了丰富的资源，包括官方文档、教程、博客文章以及社区论坛，帮助用户快速上手和深入了解 Docker 技术。下面是几个有用的链接和资源：

### Docker 官方网站

- **官方网站**: [https://www.docker.com/](https://www.docker.com/)
- **官方文档**: [https://docs.docker.com/](https://docs.docker.com/)
- **官方论坛**: [https://forums.docker.com/](https://forums.docker.com/)
- **Docker Hub**: [https://hub.docker.com/](https://hub.docker.com/) —— 这是一个公开的镜像仓库，你可以在这里查找、上传或者下载 Docker 镜像。

### Docker 教程

#### Docker 官方教程
- **Get Started with Docker**: [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/) —— 这是一系列适合初学者的教程，涵盖了 Docker 的基本概念和实践操作。
- **Tutorials**: [https://docs.docker.com/tutorials/](https://docs.docker.com/tutorials/) —— 包括了多个教程主题，比如如何使用 Docker Compose 和 Kubernetes。

#### 第三方教程和资源
- **Docker for Beginners**: 互联网上有许多第三方网站提供的 Docker 入门教程，比如在 YouTube 上有许多视频教程，或者在 Udemy、Coursera 等平台上也有付费课程。
- **Docker Book**: 有一些书籍专注于 Docker 技术的深入讲解，如《Docker in Action》等，这些书籍通常涵盖更广泛的主题并且适合不同技术水平的读者。

### Docker 社区资源
- **Stack Overflow**: 在 Stack Overflow 上，你可以找到大量的 Docker 相关问题和答案。
- **GitHub**: 有许多开源项目和示例可以在 GitHub 上找到，可以帮助你了解最佳实践和高级用法。

利用这些资源，无论是新手还是有经验的用户都能找到适合自己的学习路径，从基础概念到进阶技巧，都有所覆盖。对于想要深入研究 Docker 或者解决特定问题的人来说，官方文档和社区支持将是宝贵的资源。



## 创建，使用和配置

创建、使用和配置 Docker 主要涉及以下几个步骤：

### 创建 Docker 镜像

1. **编写 Dockerfile**:
   
   - 创建一个名为 `Dockerfile` 的文本文件，在其中编写构建镜像所需的指令。
   - 基本结构如下：
     ```
     # 使用的基础镜像
     FROM ubuntu:latest
     
     # 设置工作目录
     WORKDIR /app
     
     # 复制本地文件到容器
     COPY . /app
     
     # 设置环境变量
     ENV APP_ENV production
     
     # 指定容器启动后运行的命令
     CMD ["./start.sh"]
     ```
   
2. **构建镜像**:
   
   - 在包含 `Dockerfile` 的目录下运行以下命令来构建镜像：
     ```sh
     docker build -t my-image-name .
     ```

### 使用 Docker 容器

1. **启动容器**:
   
   - 使用 `docker run` 命令来启动一个容器：
     ```sh
     docker run -it --name my-container my-image-name
     ```
   - 参数 `-it` 表示交互式模式，`--name` 用于指定容器名称。
   
2. **管理容器**:
   
   - 查看正在运行的容器：
     ```sh
     docker ps
     ```
   - 查看所有容器（包括已停止的）：
     ```sh
     docker ps -a
     ```
   - 停止容器：
     ```sh
     docker stop my-container
     ```
   - 启动已停止的容器：
     ```sh
     docker start my-container
     ```

### 配置 Docker

1. **网络配置**:
   - Docker 允许为容器创建自定义网络，以便更好地控制容器之间的通信。
   - 创建一个网络：
     ```sh
     docker network create my-net
     ```
   - 将容器连接到特定网络：
     ```sh
     docker run -it --name my-container --network my-net my-image-name
     ```

2. **数据持久化**:
   
   - 使用卷 (`volumes`) 来保存数据，即使容器被删除，数据也不会丢失。
   - 创建一个卷：
     ```sh
     docker volume create my-volume
     ```
   - 在容器中挂载卷：
     ```sh
     docker run -it --name my-container -v my-volume:/data my-image-name
     ```
   
3. **端口映射**:
   
   - 将容器内的端口映射到主机端口，使外部可以访问容器内服务。
     ```sh
     docker run -it --name my-container -p 8080:80 my-image-name
     ```
   
4. **环境变量**:
   
   - 通过 `-e` 参数传递环境变量给容器内的应用程序。
     ```sh
     docker run -it --name my-container -e MY_VAR=myvalue my-image-name
     ```
   
5. **日志管理**:
   
   - Docker 可以将容器的日志输出到本地文件系统或其他日志管理系统。
     ```sh
     docker logs my-container
     ```

以上就是创建、使用和配置 Docker 的基本流程。当然，根据实际需求，还可能需要进行更详细的配置，例如设置资源限制、使用 Docker Compose 来管理多容器应用等。



## Docker Compose

Docker Compose 是一个用于定义和运行多容器 Docker 应用程序的工具。它允许您在一个 YAML 文件中定义一组相关的 Docker 服务，这样就可以一起启动和停止整个应用程序堆栈。Docker Compose 适用于开发环境以及持续集成/持续部署 (CI/CD) 流程。

### Docker Compose 的基本概念

- **服务 (Services)**: 一个服务代表应用程序的一部分，每个服务都由一个 Dockerfile 和一个或多个 Compose 文件中的配置项定义。

- **项目 (Projects)**: 一个项目包含一个或多个服务，这些服务通常构成一个完整的应用程序。

- **Compose 文件 (Compose Files)**: 这些文件描述了您的服务、网络和其他基础设施，通常命名为 `docker-compose.yml`。

### Docker Compose 的优点

- **简化多容器应用的管理**: Docker Compose 让您可以使用一条命令来启动或停止整个应用程序堆栈，而不需要单独处理每个服务。

- **一致性的开发环境**: 开发团队成员可以使用相同的配置文件来设置一致的开发环境。

- **易于扩展**: 可以方便地添加或移除服务，调整容器的数量等。

### Docker Compose 的基本使用

#### 创建 Docker Compose 文件

Docker Compose 文件通常使用 YAML 格式来定义服务和其他资源。下面是一个简单的 `docker-compose.yml` 示例：

```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  db:
    image: postgres
```

在这个例子中，我们定义了两个服务：`web` 和 `db`。`web` 服务是从当前目录构建的，并将容器内的端口 5000 映射到主机的端口 5000。`db` 服务使用的是 `postgres` 镜像。

#### 使用 Docker Compose

一旦您有了 `docker-compose.yml` 文件，就可以使用 Docker Compose 命令行工具来管理这些服务：

- **启动服务**:

  ```sh
  docker-compose up
  ```

  这条命令会构建并启动所有服务。

- **后台运行服务**:

  ```sh
  docker-compose up -d
  ```

  这条命令会在后台启动服务。

- **停止服务**:

  ```sh
  docker-compose down
  ```

  这条命令会停止并删除所有服务及网络。

- **查看服务状态**:

  ```sh
  docker-compose ps
  ```

  这条命令显示所有服务的状态。

Docker Compose 对于开发多容器应用非常有用，它简化了开发流程，特别是在需要协调多个服务之间依赖关系的时候。如果您正在构建一个多服务的应用程序，并希望在本地环境中模拟生产环境的配置，那么 Docker Compose 将是一个强大的工具。 



## 设置限制

在 Docker 中设置资源限制是非常重要的，尤其是在资源受限的环境下或者当您需要确保容器不会消耗过多资源时。您可以对容器设置 CPU、内存和其他资源的限制。以下是如何在 Docker 和 Docker Compose 中设置这些限制的方法。

### Docker 中设置资源限制

#### 内存限制

使用 `docker run` 命令时，可以使用 `--memory` 或 `-m` 参数来限制容器可用的最大内存。

```sh
docker run -it --name my-app --memory="200M" my-image
```

这将限制名为 `my-app` 的容器最大只能使用 200MB 的内存。

#### CPU 限制

Docker 也允许限制容器可以使用的 CPU 时间。这可以通过 `--cpus` 参数来实现。

```sh
docker run -it --name my-app --cpus="0.5" my-image
```

这将限制 `my-app` 容器只能使用半个 CPU 核心的时间。

#### 存储空间限制

还可以设置容器在磁盘上的存储空间限制：

```sh
docker run -it --name my-app --storage-opt size=2G my-image
```

这将限制 `my-app` 容器的数据存储不能超过 2GB。

### Docker Compose 中设置资源限制

在 Docker Compose 中，您可以在 `docker-compose.yml` 文件中设置资源限制。以下是示例：

```yaml
version: '3'
services:
  web:
    image: my-image
    mem_limit: 500m
    mem_reservation: 200m
    cpus: "0.5"
    shm_size: "1g"
```

- **mem_limit**: 设置容器的最大可用内存。
- **mem_reservation**: 设置容器的内存预留，即至少保证的内存数量。
- **cpus**: 设置容器可以使用的 CPU 核心数。
- **shm_size**: 设置容器共享内存大小。

请注意，不同的 Docker 版本和不同的平台可能支持的资源限制选项有所不同，请参考 Docker 文档以获取最新的信息。

### 注意事项

- 设置资源限制时，应考虑到容器的实际需求，过低的资源限制可能会导致容器频繁被杀死或性能下降。
- 资源限制应该根据您的硬件情况合理设置，以避免过度限制导致的性能问题。
- 在生产环境中，建议根据实际情况进行压力测试和监控，以确保设置的资源限制既能满足应用的需求又不至于浪费资源。

通过上述方法，您可以有效地管理和优化 Docker 容器的资源使用，确保您的系统稳定运行。

## 配置镜像加速
配置 Docker 使用镜像加速可以帮助提高从 Docker Hub 拉取镜像的速度，尤其是在网络条件不佳的情况下。以下是如何配置 Docker 使用国内镜像加速器的方法：

### Windows 和 macOS

#### 1. 打开 Docker Desktop
- 启动 Docker Desktop。

#### 2. 进入设置
- 点击右上角的齿轮图标进入设置。
- 选择 `Docker Engine` 选项卡。

#### 3. 编辑 `Docker Engine` 配置
- 在 `Docker Engine` 配置窗口中，找到 `registry-mirrors` 部分，并添加一个或多个镜像加速器地址。例如，使用阿里云的镜像加速器：
  ```json
  {
    "registry-mirrors": ["https://<你的加速器地址>.mirror.aliyuncs.com"]
  }
  ```

- 点击 `Apply & Restart` 应用更改并重启 Docker。

### Linux

#### 1. 编辑或创建 `daemon.json` 文件
- 打开终端，编辑或创建 `/etc/docker/daemon.json` 文件：
  ```sh
  sudo nano /etc/docker/daemon.json
  ```

#### 2. 添加镜像加速器配置
- 在文件中添加 `registry-mirrors` 配置，例如：
  ```json
  {
    "registry-mirrors": ["https://<你的加速器地址>.mirror.aliyuncs.com"]
  }
  ```

- 保存并关闭文件。

#### 3. 重启 Docker 服务
- 重启 Docker 服务以应用更改：
  ```sh
  sudo systemctl restart docker
  ```

### 常见的镜像加速器

- **阿里云**：注册后可以获得专属的加速器地址，例如 `https://<你的加速器地址>.mirror.aliyuncs.com`。
- **腾讯云**：提供公共镜像加速器 `https://mirrors.cloud.tencent.com/docker/`。
- **网易**：提供公共镜像加速器 `https://hub-mirror.c.163.com`。
- **DaoCloud**：提供公共镜像加速器 `https://mirrors.daocloud.io`。

### 验证配置

- 你可以通过运行以下命令来验证镜像加速器是否生效：
  ```sh
  docker info
  ```
  查看输出中的 `Registry Mirrors` 部分，确认加速器地址已经添加。

### 示例

假设你使用镜像加速器，你的 `daemon.json` 文件内容可能如下所示：

```json
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "experimental": false,
  "registry-mirrors": [
    "https://docker.registry.cyou",
    "https://docker-cf.registry.cyou",
    "https://dockercf.jsdelivr.fyi",
    "https://docker.jsdelivr.fyi",
    "https://dockertest.jsdelivr.fyi",
    "https://mirror.aliyuncs.com",
    "https://dockerproxy.com",
    "https://mirror.baidubce.com",
    "https://docker.m.daocloud.io",
    "https://docker.nju.edu.cn",
    "https://docker.mirrors.sjtug.sjtu.edu.cn",
    "https://docker.mirrors.ustc.edu.cn",
    "https://mirror.iscas.ac.cn",
    "https://docker.rainbond.cc"
  ]
}
```

希望这些步骤能帮助你成功配置 Docker 镜像加速。