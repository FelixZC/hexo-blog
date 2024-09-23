---
title: PM2
author: pzc
date: 2024-09-23
cover: /assets/images/jpg/34.jpg
categories: [nodejs]
tags: [Progress]
---
PM2 是一个流行的 Node.js 应用程序的进程管理器。它允许开发者轻松地管理和保持应用程序的运行状态，即使在服务器重启或应用崩溃的情况下也能自动重启应用。以下是 PM2 的一些主要特点和功能：

### 主要特点

- **保持应用常驻**：PM2 可以确保你的 Node.js 应用始终保持运行，如果应用因为任何原因停止，PM2 会自动重启它。
- **负载均衡**：通过使用集群模式，PM2 能够将 Node.js 应用部署到多个 CPU 核心上，实现负载均衡，从而提高应用性能。
- **日志管理**：PM2 提供了日志聚合的功能，可以方便地查看所有由 PM2 管理的应用的日志输出。
- **监控与度量**：PM2 内置了一个实时监控界面，可以显示应用的状态、CPU 和内存使用情况等信息。
- **命令行接口**：提供了一系列强大的命令行工具来启动、停止、重启以及管理 Node.js 应用。
- **生态系统**：PM2 拥有一个活跃的社区和丰富的插件生态，支持更多的扩展功能。

### 安装

PM2 可以通过 npm（Node.js 的包管理器）来安装。打开终端或命令提示符，执行以下命令即可安装 PM2：

```bash
npm install -g pm2
```

### 基础命令

PM2 的命令行接口（CLI）提供了丰富而强大的功能，帮助开发者轻松管理 Node.js 应用程序。以下是 PM2 CLI 的一些基本命令及其用途，这些命令可以帮助你启动、管理、监控和维护你的应用程序。

1. **启动应用**

   ```bash
   pm2 start app.js
   ```

   这个命令会启动 `app.js` 脚本，并将其作为后台进程运行。

2. **启动多个实例**

   ```bash
   pm2 start app.js -i max
   ```

   使用 `-i` 参数可以指定启动的实例数，`max` 表示根据 CPU 核心数自动分配实例数。

3. **重启应用**

   ```bash
   pm2 restart app
   ```

   重启名为 `app` 的应用。如果没有指定名字，可以使用应用的 ID。

4. **停止应用**

   ```bash
   pm2 stop app
   ```

   停止名为 `app` 的应用。

5. **删除应用**

   ```bash
   pm2 delete app
   ```

   删除名为 `app` 的应用。删除后，该应用将不再由 PM2 管理。

6. **列出所有应用**

   ```bash
   pm2 list
   ```

   显示所有由 PM2 管理的应用列表，包括它们的状态、PID 等信息。

7. **查看日志**

   ```bash
   pm2 logs
   ```

   查看所有应用的日志输出。可以使用 `pm2 logs <app-name>` 查看特定应用的日志。

8. **清除日志**

   ```bash
   pm2 flush
   ```

   清除所有应用的日志文件。

9.  **查看应用详情**

    ```bash
    pm2 show <app-name>
    ```

    显示特定应用的详细信息，包括环境变量、启动脚本、日志文件路径等。

    

### 高级命令

1. **生成启动脚本**

   ```bash
   pm2 startup
   ```

   生成一个启动脚本，使 PM2 在系统启动时自动启动。根据提示选择操作系统类型，然后执行生成的命令。

2. **保存当前应用列表**

   ```bash
   pm2 save
   ```

   将当前运行的应用列表保存到 PM2 的配置文件中，以便在系统重启后恢复这些应用。

3. **加载保存的应用列表**

   ```bash
   pm2 resurrect
   ```

   从配置文件中恢复之前保存的应用列表。

4. **配置文件**

   ```bash
   pm2 start ecosystem.config.js
   ```

   使用 `ecosystem.config.js` 文件来启动应用。这个文件可以包含多个应用的配置，支持更复杂的部署场景。

5. **实时监控**

   ```bash
   pm2 monit
   ```

   打开 PM2 的实时监控界面，可以查看 CPU、内存使用情况等。

6. **优雅停机**

   ```bash
   pm2 graceful-stop app
   ```

   优雅地停止应用，等待所有正在进行的请求处理完毕后再停止。

### 其他有用命令

- **重新加载 PM2**

  ```bash
  pm2 reload all
  ```

  重新加载所有应用，适用于修改了配置文件后需要更新应用的情况。

- **查看帮助**

  ```bash
  pm2 help
  ```

  显示 PM2 的所有可用命令及其说明。

通过这些命令，你可以有效地管理 Node.js 应用程序，确保它们在生产环境中稳定运行。如果你有更复杂的需求，可以参考 PM2 的官方文档，了解更多高级功能和配置选项。



### 高级特性

- **配置文件**：可以通过 JSON 或 YAML 文件来配置 PM2 的启动参数，这使得管理复杂的应用部署更加容易。
- **生态系统模块**：PM2 支持各种生态系统模块，比如用于部署的 pm2-deploy，用于 Web 界面监控的 pm2-web，等等。
- **集成系统服务**：PM2 可以将自身注册为系统服务，这样即使服务器重启，PM2 也会自动启动并恢复之前管理的所有应用。

#### 1. 配置文件

PM2 的配置文件（通常命名为 `ecosystem.config.js` 或 `pm2.json`）允许你以声明式的方式定义和管理多个应用。这种方式比直接在命令行中输入参数更为灵活和强大。

##### 示例 `ecosystem.config.js`

```javascript
const { cpus } = require('node:os');
const cpuLen = cpus().length;

module.exports = {
  apps: [
    {
      name: 'api-server',
      script: './dist/api.js',
      autorestart: true,
      exec_mode: 'cluster',
      watch: false,
      instances: cpuLen,
      max_memory_restart: '1G',
      env: {
        NODE_ENV: 'production',
        PORT: 3000,
      },
      env_development: {
        NODE_ENV: 'development',
        PORT: 3001,
      },
    },
    {
      name: 'web-app',
      script: './dist/web.js',
      autorestart: true,
      exec_mode: 'fork',
      watch: true,
      instances: 1,
      max_memory_restart: '500M',
      env: {
        NODE_ENV: 'production',
        PORT: 8080,
      },
      env_development: {
        NODE_ENV: 'development',
        PORT: 8081,
      },
    }
  ],
  deploy: {
    production: {
      user: 'deploy-user',
      host: ['192.168.1.100', '192.168.1.101'],
      ref: 'origin/master',
      repo: 'git@github.com:yourusername/yourrepo.git',
      path: '/var/www/production',
      'pre-deploy-local': '',
      'post-deploy': 'npm install && pm2 reload ecosystem.config.js --env production',
      'pre-setup': ''
    },
    development: {
      user: 'dev-user',
      host: '192.168.1.102',
      ref: 'origin/develop',
      repo: 'git@github.com:yourusername/yourrepo.git',
      path: '/var/www/development',
      'post-deploy': 'npm install && pm2 startOrRestart ecosystem.config.js --env development',
      'pre-setup': ''
    }
  }
};
```

#### 2. 生态系统模块

PM2 的生态系统模块是一系列扩展 PM2 功能的插件。这些模块可以帮助你实现更多高级功能，如部署、Web 界面监控等。

##### 常用的生态系统模块

- **`pm2-deploy`**：用于自动化部署。
- **`pm2-logrotate`**：用于日志轮转。
- **`pm2-web`**：提供 Web 界面监控。
- **`pm2-metrics`**：收集和展示应用的性能指标。

##### 安装和使用 `pm2-deploy`

1. 安装 `pm2-deploy` 模块：

   ```sh
   npm install pm2-deploy --save-dev
   ```

2. 在 `ecosystem.config.js` 中配置 `deploy` 部分（如上所示）。

3. 部署应用：

   ```sh
   pm2 deploy ecosystem.config.js production setup
   pm2 deploy ecosystem.config.js production update
   ```

#### 3. 集成系统服务

PM2 可以将自身注册为系统服务，确保在系统启动时自动启动 PM2 并恢复之前管理的所有应用。

##### 生成启动脚本

1. 生成启动脚本：

   ```sh
   pm2 startup
   ```

   运行上述命令后，PM2 会生成一个适合你操作系统的启动脚本。例如，在 Ubuntu 上，你会看到类似以下的输出：

   ```sh
   [PM2] Init System found: systemd
   [PM2] To setup the Startup Script, copy/paste the following command:
   sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u your-username --hp /home/your-username
   ```

2. 执行生成的命令：

   ```sh
   sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u your-username --hp /home/your-username
   ```

##### 保存和恢复应用列表

1. 保存当前应用列表：

   ```sh
   pm2 save
   ```

2. 系统重启后，PM2 会自动恢复之前管理的所有应用。

### 总结

总之，PM2 是一个强大且易于使用的工具，对于希望在生产环境中部署和维护 Node.js 应用的开发者来说非常有价值。通过配置文件、生态系统模块和集成系统服务，PM2 提供了一套完整的工具链，帮助你在生产环境中高效地管理和维护 Node.js 应用。高级特性不仅提高了应用的可靠性和性能，还简化了部署和运维流程。



