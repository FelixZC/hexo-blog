---
title: "Nestjs"
date: 2024-09-14
author: "pzc"
cover: /assets/images/jpg/26.jpg
categories: [nodejs]
tags: [Framework,Backend,Server]
---
Nest.js 是一个基于 Node.js 的渐进式框架，它使用 TypeScript 构建高效、可维护且可扩展的服务器端应用程序。Nest.js 结合了现代 JavaScript 与传统的架构原则（如模块化、依赖注入等），使得开发大型企业级应用变得更加简单。下面是对 Nest.js 的详细解析，旨在帮助您全面了解这一框架。

### 什么是 Nest.js？

Nest.js 是一个用于构建高效和可扩展的 Node.js 服务器端应用程序的框架。它基于 TypeScript（也支持纯 JavaScript）构建，并遵循了 Angular 的设计理念，引入了模块化和依赖注入等概念。Nest.js 的目标是提供一种灵活的方式来构建高度可扩展的应用程序，同时保持代码的整洁和模块化。


NestJS 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的框架。它使用现代 JavaScript，结合了 OOP（面向对象编程）、FP（函数式编程）和 FRP（函数响应式编程）的原则。下面是一些官方和社区提供的 NestJS 可用资源：

### 官方资源

1. **官方网站**:
   - [NestJS 官网](https://nestjs.com/) 提供了关于框架的基本信息以及入门指南。

2. **官方文档**:
   - [NestJS 文档](https://docs.nestjs.com/) 是学习 NestJS 的主要参考资料。它涵盖了从安装到高级特性的所有内容。
   - 包括但不限于快速开始、模块、控制器、服务、中间件、异常过滤器、管道、守卫、拦截器、自定义装饰器等。

3. **官方 GitHub 仓库**:
   - [NestJS GitHub](https://github.com/nestjs/nest) 是获取源代码的地方，你可以查看示例项目、报告问题或贡献代码。

4. **官方 CLI 工具**:
   - `@nestjs/cli` 命令行工具帮助你生成新的 NestJS 应用程序、模块、服务等，大大简化开发流程。
   - 安装命令：`npm i -g @nestjs/cli`

5. **官方论坛与社区**:
   - [NestJS Discord](https://discord.gg/G7Qnnhy) 社区是提问、讨论和交流的好地方。
   - [NestJS 中文社区](http://cn.nestjs.com/) 对于中文用户来说是一个很好的资源。

6. **官方博客**:
   - [NestJS Blog](https://trilon.io/blog/tags/nestjs) 上有最新的公告、更新日志和技术文章。

### 社区资源

- **教程和视频**:
  - Bilibili 上有许多开发者分享的 NestJS 教程，如 Kody Brown, Ben Awad 等知名开发者。
  - [Epic Web Dev](https://www.epicweb.dev/) 也提供了一些高质量的 NestJS 教学视频。

- **第三方库和插件**:
  - [NestJS Awesome List](https://github.com/juliandavidmr/awesome-nestjs) 收集了许多有用的第三方库、插件和其他资源。

- **书籍**:
  - 《NestJS实战》（中文版）是由阿里云开发者社区出版的一本介绍如何使用 NestJS 构建企业级应用的书籍。
  - 《Building Microservices with NestJS: A Practical Guide to Building Scalable and Maintainable Microservices in Node.js》提供了关于使用 NestJS 构建微服务架构的实际指导。

这些资源应该能为你提供一个全面的学习和发展平台，无论你是初学者还是想要深入研究特定领域的开发者。

### 主要特性

1. **模块化**: Nest.js 引入了模块的概念，允许开发者将应用程序划分为多个功能区域，每个区域都有自己的职责和服务。

2. **依赖注入**: 通过依赖注入（DI），Nest.js 使得组件之间的依赖关系更加清晰，并提高了代码的可测试性。

3. **装饰器**: Nest.js 利用了 TypeScript 的装饰器功能来简化元编程任务，例如路由、中间件、过滤器等。

4. **异步编程**: Nest.js 支持原生的 ES6+ 语法，包括 async/await，使得编写异步代码变得容易。

5. **可扩展性**: 由于其插件系统和开放的架构，Nest.js 可以轻松地扩展以适应各种需求。

6. **强大的 CLI 工具**: Nest CLI 使得脚手架搭建、代码生成、测试等任务变得简单快捷。

7. **广泛的生态系统**: Nest.js 有一个活跃的社区和丰富的生态系统，提供了大量的插件和工具。

### 架构

Nest.js 的核心架构包括以下几个部分：

- **模块 (Modules)**: 模块是应用程序的基本组成部分，它们可以包含控制器、提供者和服务。
- **控制器 (Controllers)**: 控制器负责处理客户端请求并将结果返回给客户端。
- **服务 (Services)**: 服务是用来处理业务逻辑的对象，通常不直接与 HTTP 请求交互。
- **提供者 (Providers)**: 提供者是一个更通用的概念，它可以是任何对象，只要它是通过 DI 注入到其他对象中的。
- **装饰器 (Decorators)**: 装饰器用来标记类、属性、方法等，以便框架能够识别并作出相应的处理。


NestJS 提供了一系列内置模块，这些模块可以帮助开发者快速构建应用程序。这些内置模块覆盖了从HTTP请求处理到数据库集成等多个方面。以下是一些常用的 NestJS 内置模块：

1. **Common 模块**:
   - `@nestjs/common` 是最基础的模块，包含了装饰器、异常处理、管道、守卫等核心功能。

2. **Core 模块**:
   - `@nestjs/core` 提供了框架的核心功能，比如应用初始化、模块注册等。它通常与 `@nestjs/common` 一起使用。

3. **CLI 模块**:
   - `@nestjs/cli` 虽然不是运行时使用的模块，但它是一个命令行工具，用于创建新项目、生成代码结构（如控制器、服务）等。

4. **Platform-Express 模块**:
   - `@nestjs/platform-express` 是一个适配层，使得 NestJS 可以基于 Express.js 运行。这允许你利用 Express 的强大功能，同时享受 NestJS 的架构优势。

5. **Platform-Fastify 模块**:
   - `@nestjs/platform-fastify` 类似于 `platform-express`，但它是基于 Fastify 的。Fastify 是一个专注于性能的轻量级 HTTP 框架。

6. **TypeORM 模块**:
   - `@nestjs/typeorm` 集成了 TypeORM，这是一个流行的 ORM 库，支持多种数据库系统，包括 MySQL, PostgreSQL, SQLite 等。

7. **Mongoose 模块**:
   - `@nestjs/mongoose` 为 MongoDB 提供了 Mongoose 的集成，使得在 NestJS 中操作 MongoDB 数据库变得简单易用。

8. **GraphQL 模块**:
   - `@nestjs/graphql` 提供了对 GraphQL 的支持，允许你构建强大的 API。

9. **Swagger 模块**:
   - `@nestjs/swagger` 用来生成和文档化 RESTful APIs，支持 Swagger/OpenAPI 规范。

10. **Passport 模块**:
    - `@nestjs/passport` 为 NestJS 应用程序提供 Passport 认证策略的支持，可以很容易地实现用户认证。

11. **WebSocket 模块**:
    - `@nestjs/websockets` 和 `@nestjs/platform-socket.io` 支持实时通信，通过 WebSocket 实现。

12. **Microservices 模块**:
    - `@nestjs/microservices` 用于构建微服务架构的应用程序，支持多种传输协议，如 TCP, Redis, RabbitMQ, NATS, MQTT 等。

13. **Caching 模块**:
    - `@nestjs/cache-manager` 提供了缓存管理的功能，支持多种后端存储，例如内存、Redis 等。

14. **Scheduler 模块**:
    - `@nestjs/schedule` 允许你在 NestJS 应用中轻松设置定时任务。

每个模块都有其特定的用途，并且可以通过官方文档来详细了解如何安装和配置它们。这些模块帮助开发者更加高效地构建复杂而健壮的应用程序。

### 应用场景

Nest.js 可以用于多种类型的 Web 应用程序开发：

- **RESTful API**: 创建高性能的 RESTful 服务。
- **GraphQL API**: 通过 GraphQL 模块支持 GraphQL 协议。
- **WebSocket**: 实现实时通信应用，如聊天室、在线协作工具等。
- **微服务架构**: 作为微服务架构的一部分，Nest.js 提供了很好的支持和工具。

### 开发实践

#### 代码组织

- **文件结构**: 通常按照功能或领域模型来组织代码，每个模块有自己的文件夹，包含控制器、服务、模型等。
- **命名约定**: 使用有意义的命名，如使用 PascalCase 命名类名，camelCase 命名属性等。

#### 测试

- **单元测试**: 对于每一个服务、控制器、提供者都应该编写单元测试。
- **集成测试**: 对于整个模块或应用程序进行集成测试，确保各个部分协同工作。
- **端到端测试**: 模拟真实用户行为，测试整个应用程序的工作流。

###  NestJS CLI 

NestJS CLI (Command Line Interface) 是一个强大的命令行工具，专为 NestJS 框架设计，旨在简化 NestJS 应用程序的创建、管理和开发过程。通过使用 NestJS CLI，开发者可以快速地生成新的项目、模块、服务、控制器等，而无需手动编写大量的模板代码。此外，CLI 还提供了许多其他功能，如启动开发服务器、构建生产环境的应用程序等。以下是一些主要特性和使用方法的介绍：

#### 安装

首先，你需要安装 NestJS CLI。可以通过 npm 全局安装：

```bash
npm install -g @nestjs/cli
```

#### 创建新项目

安装完成后，你可以使用 `nest new` 命令来创建一个新的 NestJS 项目：

```bash
nest new project-name
```

这将引导你完成一系列选择，比如选择包管理器（npm 或 yarn），是否需要安装 ESLint 等。完成后，CLI 会自动下载必要的依赖并初始化项目结构。

#### 生成模块、服务、控制器等

在项目中，你可以轻松地生成新的模块、服务、控制器、守卫、管道、中间件等。例如，要生成一个新的控制器，可以使用：

```bash
nest generate controller cats
```

这将在 `src/cats` 目录下创建一个名为 `cats.controller.ts` 的文件，并自动导入必要的模块。类似的命令有：

- `nest generate service cats`：生成服务。
- `nest generate module cats`：生成模块。
- `nest generate guard cats`：生成守卫。
- `nest generate pipe cats`：生成管道。
- `nest generate middleware cats`：生成中间件。
- `nest generate filter cats`：生成异常过滤器。

#### 开发服务器

要启动开发服务器，可以使用以下命令：

```bash
nest start
```

默认情况下，这将启动一个热重载的开发服务器。如果你想要在监视模式下启动（即文件更改时自动重启），可以使用：

```bash
nest start --watch
```

#### 构建生产环境应用

为了构建一个优化过的生产环境应用，可以使用：

```bash
nest build
```

这将根据你的配置文件（通常是 `tsconfig.json` 和 `nest-cli.json`）编译 TypeScript 代码，生成 JavaScript 文件，并准备好部署。

#### 其他常用命令

- `nest help`：显示帮助信息，列出所有可用的命令。
- `nest version`：显示已安装的 NestJS CLI 版本。
- `nest update`：更新 NestJS CLI 和相关依赖到最新版本。

#### 配置文件

NestJS CLI 使用 `nest-cli.json` 文件来配置项目的构建和其他设置。此文件通常位于项目的根目录中，包含了关于源代码位置、编译选项、插件等的信息。

#### 插件支持

NestJS CLI 支持插件，这使得开发者可以根据需要扩展其功能。例如 `@nestjs/swagger` 插件就是用来生成 API 文档的。你可以通过在 `nest-cli.json` 中配置插件来启用它们。


### 完整示例

创建一个完整的 NestJS 应用程序涉及多个步骤，包括初始化项目、添加模块、控制器、服务等。下面我将指导你如何从头开始创建一个简单的 NestJS 项目，并给出一些基本的代码示例。

### 步骤 1: 初始化 NestJS 项目

首先，你需要安装 Nest CLI（如果你还没有安装的话）。这可以通过 npm 完成：

```bash
npm i -g @nestjs/cli
```

然后，使用 Nest CLI 创建一个新的项目：

```bash
nest new project-name
```

这将引导你完成项目的创建过程，包括选择包管理器（如 npm 或 yarn）和安装必要的依赖。

### 步骤 2: 项目结构

创建后，你的项目结构看起来应该像这样：

```
project-name/
├── src/
│   ├── app.controller.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   └── main.ts
├── test/
├── .env
├── .gitignore
├── package.json
├── README.md
└── tsconfig.json
```

### 步骤 3: 修改 `main.ts`

`main.ts` 是应用程序的入口点。默认情况下，它会启动应用并监听指定端口。

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000); // 监听3000端口
}
bootstrap();
```

### 步骤 4: 创建控制器

在 `src/` 下创建一个名为 `cats` 的目录，并在此目录中创建 `cats.controller.ts` 文件。这个文件将处理与猫相关的请求。

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('cats')
export class CatsController {
  @Get()
  findAll(): string {
    return 'This action returns all cats';
  }
}
```

### 步骤 5: 创建服务

在同一 `cats` 目录下创建 `cats.service.ts` 来处理业务逻辑。

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class CatsService {
  getCats(): string[] {
    return ['Cat 1', 'Cat 2'];
  }
}
```

更新 `CatsController` 使用 `CatsService`：

```typescript
import { Controller, Get } from '@nestjs/common';
import { CatsService } from './cats.service';

@Controller('cats')
export class CatsController {
  constructor(private readonly catsService: CatsService) {}

  @Get()
  findAll(): string[] {
    return this.catsService.getCats();
  }
}
```

### 步骤 6: 更新模块

最后，在 `app.module.ts` 中导入新的 `CatsModule`。先创建 `cats.module.ts`:

```typescript
import { Module } from '@nestjs/common';
import { CatsController } from './cats.controller';
import { CatsService } from './cats.service';

@Module({
  controllers: [CatsController],
  providers: [CatsService],
})
export class CatsModule {}
```

然后在 `app.module.ts` 中引入 `CatsModule`：

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { CatsModule } from './cats/cats.module';

@Module({
  imports: [CatsModule],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

现在，你可以运行你的应用程序了：

```bash
npm run start
```

访问 `http://localhost:3000/cats` 将显示由 `CatsService` 提供的数据。

这就是一个基础的 NestJS 应用程序。随着你对框架越来越熟悉，你可以继续探索更多高级功能，比如数据库集成、身份验证、中间件等。


### 最佳实践

- **安全**: 实施适当的安全措施，如使用 HTTPS、XSS 和 CSRF 防护、输入验证等。
- **性能**: 优化性能瓶颈，如使用缓存、减少数据库查询次数等。
- **可维护性**: 保持代码的可读性和可维护性，如使用清晰的注释、遵循 SOLID 原则等。

### 未来展望

Nest.js 不断发展，未来可能会增加更多的特性和改进现有功能。随着 TypeScript 的不断成熟和发展，Nest.js 也将受益于 TypeScript 社区的进步。

### 总结

Nest.js 以其模块化的设计、依赖注入系统和对 TypeScript 的支持，成为了构建高性能 Node.js 应用的理想选择。无论您是在寻找一种构建微服务的方法，还是想要简化大型应用的开发流程，Nest.js 都是一个值得考虑的框架。随着它的不断发展和完善，未来还将提供更多功能和改进现有特性，进一步增强其作为顶级 Node.js 框架的地位。