---
title: Nginx相关
author: pzc
date: 2024-09-14
cover: /assets/images/jpg/24.jpg
categories: [java]
tags: [Backend,Server]
---
##  Nginx介绍

Nginx 是一个高性能的HTTP和反向代理服务器，也是一个IMAP/POP3/SMTP代理服务器。它以其高性能、稳定性、丰富的功能集、简单的配置以及较低的内存消耗而闻名。Nginx 通常用于高流量站点，可以处理大量的并发连接，并且在负载均衡方面表现优异。

## Nginx 的特点
- **高效**：Nginx 采用了一个异步非阻塞的I/O模型，这意味着它可以处理大量并发连接。
- **稳定性**：Nginx 在高负载下依然保持稳定。
- **丰富的特性**：支持HTTP服务器、反向代理、负载均衡等功能。
- **低资源消耗**：Nginx 的设计使其能够在低资源环境下运行良好。
- **模块化**：可以通过第三方模块扩展其功能。


## 安装 Nginx
在 Ubuntu 上安装 Nginx 可以通过包管理器来完成：
```bash
sudo apt-get update
sudo apt-get install Nginx
```

在 Windows 上安装 Nginx 的过程与在 Linux 或 Unix 系统上有所不同。以下是在 Windows 上安装 Nginx 的步骤：

### 步骤 1: 下载 Nginx
你可以从 Nginx 官方网站下载适用于 Windows 的预编译版本。前往 [Nginx 官方下载页面](https://Nginx.org/en/download.html)，选择适用于 Windows 的版本。通常，你会看到一个 `.zip` 文件，例如 `Nginx.1.21.6.zip`。

### 步骤 2: 解压缩 Nginx 包
将下载的 `.zip` 文件解压到一个合适的目录。例如，你可以将其解压到 `C:\Nginx` 目录下。

### 步骤 3: 配置环境变量
为了方便地从命令行启动 Nginx，建议将 Nginx 的可执行文件所在目录添加到系统的 `PATH` 环境变量中。例如，假设你将 Nginx 解压到了 `C:\Nginx`，那么你需要将 `C:\Nginx` 添加到 `PATH` 环境变量中。

1. 打开“控制面板” -> “系统和安全” -> “系统” -> “高级系统设置” -> “环境变量”。
2. 在“系统变量”部分找到并编辑 `Path` 变量。
3. 将 `C:\Nginx` 添加到变量值中，确保前后有分号分隔其他条目。
4. 确定后关闭所有窗口。

### 步骤 4: 启动 Nginx
打开命令提示符或 PowerShell，然后导航到 Nginx 的目录，通常是 `C:\Nginx`。输入以下命令来启动 Nginx：
```shell
.\Nginx.exe
```

### 步骤 5: 测试 Nginx 是否启动成功
打开浏览器，访问 `http://localhost` 或 `http://127.0.0.1`，如果一切正常，你应该会看到 Nginx 的欢迎页面。

### 步骤 6: 停止 Nginx
停止 Nginx 也很简单，只需要在命令提示符中输入以下命令：
```shell
.\Nginx.exe -s stop
```

如果你使用的是 Windows 任务管理器或其他方法启动的 Nginx，也可以直接结束名为 `Nginx.exe` 的进程。

## 配置

### 基本配置

Nginx 的配置文件通常位于`/etc/Nginx/Nginx.conf`或`/usr/local/Nginx/conf/Nginx.conf`（取决于安装方式）。你可以根据需要修改这个文件来定制你的 Nginx 服务器的行为。配置文件分为全局块、事件块、HTTP块和Server块。

### 注意事项
- 如果你在 Windows 上遇到权限问题，请确保以管理员身份运行命令提示符或 PowerShell。
- 在企业环境中，你可能需要调整防火墙设置以允许外部访问。
- 确保没有其他服务正在使用端口 80（HTTP）或 443（HTTPS），否则 Nginx 将无法绑定到这些端口。

### 示例配置文件

```Nginx
user Nginx;
worker_processes auto;

error_log /var/log/Nginx/error.log warn;
pid /var/run/Nginx.pid;

events {
    worker_connections 1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    # 设置日志格式
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/Nginx/access.log  main;

    sendfile        on;
    tcp_nopush     on;
    tcp_nodelay    on;
    keepalive_timeout  65;
    types_hash_max_size 2048;

    # 配置静态文件缓存
    include /etc/Nginx/conf.d/*.conf;

    server {
        listen       80;
        server_name  localhost;

        # 静态文件服务
        location / {
            root   /usr/share/Nginx/html;
            index  index.html index.htm;
        }

        # 错误页面处理
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /usr/share/Nginx/html;
        }
    }
}
```

## 常用命令

- 启动 Nginx: `sudo systemctl start Nginx`
- 停止 Nginx: `sudo systemctl stop Nginx`
- 重新加载配置文件: `sudo systemctl reload Nginx`
- 检查配置文件是否正确: `sudo Nginx -t`


## 配置属性

Nginx 的配置文件由多个层级构成，每个层级可以包含一系列指令。以下是 Nginx 配置中一些常见的属性及其解释：

### 全局块
这是整个配置文件的第一层，包含了影响所有其他层级的设置。
- **user**：指定运行 Nginx 进程的用户或组。
- **worker_processes**：定义了 Nginx 可以创建的工作进程的数量。
- **error_log**：设置错误日志的位置及报告级别。
- **pid**：指定用来保存主进程 PID 的文件路径。

### events 块
这个块定义了如何处理客户端连接。
- **worker_connections**：每个工作进程允许的最大并发连接数。

### http 块
此块包含了所有 HTTP 相关的配置。
- **include**：引入其他配置文件。
- **log_format**：定义日志格式。
- **access_log**：指定访问日志的存储位置和格式。
- **sendfile**：启用或禁用高效的数据传输。
- **keepalive_timeout**：设定空闲超时时间。
- **gzip**：开启或关闭 gzip 压缩。

### server 块
每个 `server` 块定义了一个虚拟主机，可以用来处理特定域名或 IP 地址的请求。
- **listen**：指定了要监听的端口和地址。
- **server_name**：定义了该虚拟主机的域名。
- **charset**：设置默认字符集。
- **client_max_body_size**：设置客户端请求主体的最大大小。
- **add_header**：为响应添加额外的 HTTP 头。
- **root**：指定服务器文档的根目录。
- **index**：列出索引文件名。

### location 块
`location` 块进一步细化了对请求的处理逻辑。
- **location /**：匹配 URL 路径。
- **try_files**：尝试找到请求的文件，如果找不到则转向其他路径或返回特定状态码。
- **proxy_pass**：设置反向代理的目标地址。
- **rewrite**：重写 URL。
- **return**：直接返回一个固定的 HTTP 状态码或重定向到另一个 URL。


这些只是 Nginx 中一些基础的配置项，实际上还有许多其他选项可以根据需要来调整。在生产环境中，通常会有更多的安全和性能相关的配置。