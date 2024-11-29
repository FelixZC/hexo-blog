---
title: swagger
author: pzc
date: 2024-11-29
cover: /assets/images/jpg/82.jpg
categories: [other]
tags: [Doc,Java,Node]
---
## 介绍

Swagger 是一个非常流行的框架，用于设计、构建、文档化和使用 RESTful 飐格的 Web 服务。它允许开发者定义 API 的各个方面，如端点（URI）、参数、请求和响应格式等，并自动生成交互式文档。Swagger 已经成为 OpenAPI 规范（OAS）的事实标准实现，该规范是描述 RESTful API 的一种方式。

### Swagger 的主要组成部分

1. **OpenAPI Specification (OAS)**
   - 这是一个开放的标准，用于描述 RESTful API。最初称为 Swagger Specification，现在已更名为 OpenAPI Specification。
   - OAS 支持两种语法：YAML 和 JSON，可以用来定义 API 的结构。

2. **Swagger Editor**
   - 提供了一个在线编辑器，可以在其中编写和验证你的 API 定义。
   - 它可以帮助你确保你的 API 定义符合 OpenAPI 规范。

3. **Swagger UI**
   - 根据 OpenAPI 文档生成一个可交互的 API 文档界面。
   - 用户可以通过这个界面查看 API 的信息，尝试 API 调用，查看请求和响应示例。

4. **Swagger Codegen**
   - 基于 OpenAPI 文档自动生成客户端库、服务器存根、API 文档等。
   - 支持多种编程语言，如 Java, JavaScript, C#, Python 等。

5. **Swagger Inspector**
   - 允许用户测试 API 并从 API 响应中直接生成 OpenAPI 文档。

6. **Swagger Hub**
   - 提供了集中管理 API 文档的功能，支持版本控制和协作开发。
   - 可以在团队成员之间共享 API 设计，并且可以与 CI/CD 流水线集成。

### 使用场景

- **API 设计**：在编码之前，先设计好 API 的接口。
- **API 文档**：自动生成易于阅读的 API 文档。
- **API 测试**：通过 Swagger UI 直接测试 API。
- **客户端代码生成**：为不同的平台自动生成客户端代码。
- **API 发布**：发布 API 文档到 Swagger Hub 或其他地方，方便团队协作。

### 

Swagger 通过提供一系列工具和规范简化了 RESTful API 的整个生命周期管理，从设计到文档再到测试。它不仅帮助开发者提高效率，还促进了前后端之间的沟通，使得 API 更加易于理解和使用。如果你正在开发或维护 RESTful API，那么 Swagger 是一个值得考虑的强大工具。

## 资源

Swagger 的官方资源可以帮助开发者更好地理解和使用 Swagger 工具集。以下是一些主要的官方资源链接，你可以通过这些资源来获取文档、教程、工具和其他支持：

1. **Swagger 官方网站**:
   - 网址: [https://swagger.io/](https://swagger.io/)
   - 这是 Swagger 的官方网站，提供了关于 Swagger 的最新信息、博客文章、案例研究和社区活动。

2. **OpenAPI 规范 (OAS)**:
   - 网址: [https://github.com/OAI/OpenAPI-Specification](https://github.com/OAI/OpenAPI-Specification)
   - OpenAPI 规范定义了如何描述 RESTful API 的结构，包括端点、操作、参数、请求体、响应等。

3. **Swagger Editor**:
   - 网址: [https://editor.swagger.io/](https://editor.swagger.io/)
   - 一个在线编辑器，用于编写和验证 OpenAPI 文档。它还允许你实时预览生成的 API 文档。

4. **Swagger UI**:
   - GitHub 仓库: [https://github.com/swagger-api/swagger-ui](https://github.com/swagger-api/swagger-ui)
   - 一个工具，可以将你的 OpenAPI 文档转换为交互式的 API 文档页面，用户可以直接在网页上测试 API。

5. **Swagger Codegen**:
   - GitHub 仓库: [https://github.com/swagger-api/swagger-codegen](https://github.com/swagger-api/swagger-codegen)
   - 根据 OpenAPI 文档自动生成客户端库、服务器存根和 API 文档。

6. **Swagger Inspector**:
   - 网址: [https://app.swaggerhub.com/tools/inspector](https://app.swaggerhub.com/tools/inspector)
   - 一个 API 测试工具，可以从 API 响应中直接生成 OpenAPI 文档。

7. **Swagger Hub**:
   - 网址: [https://app.swaggerhub.com/](https://app.swaggerhub.com/)
   - 一个协作平台，可以用来设计、开发、测试和发布 API。它支持版本控制，并且可以与 CI/CD 流水线集成。

8. **Swagger 官方文档**:
   - 网址: [https://swagger.io/docs/](https://swagger.io/docs/)
   - 提供了详细的指南和教程，帮助你了解如何使用 Swagger 的各种工具和服务。

9. **Swagger Blog**:
   - 网址: [https://swagger.io/blog/](https://swagger.io/blog/)
   - 包含了最新的行业新闻、最佳实践和技术文章。

10. **GitHub 项目**:
    - Swagger 的许多工具都是开源的，可以在 GitHub 上找到它们的源代码和问题跟踪。
    - 例如，[Swagger Core](https://github.com/swagger-api/swagger-core) 是 Java 平台上的实现。

如果你需要更具体的信息或有特定的问题，可以访问上述资源中的相应部分，或者在 Swagger 社区寻求帮助。Swagger 拥有一个活跃的社区，你可以在那里提问并获得其他开发者和专家的支持。



## 集成springbooot

为了更好地理解如何在项目中使用 Swagger，我将通过一个具体的示例来展示如何定义 API、配置 Swagger 以及生成和查看交互式文档。我们将使用 Spring Boot 和 Swagger 来创建一个简单的 RESTful Web 服务。

### 1. 创建 Spring Boot 项目

首先，确保你已经安装了 Java 和 Maven。然后，你可以使用 Spring Initializr（https://start.spring.io/）来创建一个新的 Spring Boot 项目。选择以下依赖：

- **Spring Web**
- **Spring Boot DevTools** (可选，用于开发时的热部署)
- **Lombok** (可选，用于减少样板代码)

### 2. 添加 Swagger 依赖

打开 `pom.xml` 文件，添加 Swagger 的相关依赖。这里我们使用的是 `springfox-boot-starter`，它简化了 Swagger 的集成过程。

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-boot-starter</artifactId>
    <version>3.0.0</version>
</dependency>
```

### 3. 定义数据模型

创建一个简单的 `Product` 类作为数据模型。

```java
package com.example.demo.model;

import io.swagger.v3.oas.annotations.media.Schema;
import lombok.Data;

@Data
public class Product {
    
    @Schema(description = "The unique identifier for a product", example = "1")
    private Long id;
    
    @Schema(description = "The name of the product", example = "Apple iPhone 13")
    private String name;
    
    @Schema(description = "The price of the product", example = "999.99")
    private double price;
}
```

### 4. 创建控制器

创建一个控制器类来处理 HTTP 请求。

```java
package com.example.demo.controller;

import com.example.demo.model.Product;
import io.swagger.v3.oas.annotations.Operation;
import io.swagger.v3.oas.annotations.Parameter;
import io.swagger.v3.oas.annotations.responses.ApiResponse;
import io.swagger.v3.oas.annotations.tags.Tag;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

@RestController
@RequestMapping("/api/products")
@Tag(name = "Products", description = "Operations pertaining to product management")
public class ProductController {

    private List<Product> products = new ArrayList<>();

    @Operation(summary = "Get all products", description = "Returns a list of all products")
    @ApiResponse(responseCode = "200", description = "Successful retrieval of products")
    @GetMapping
    public ResponseEntity<List<Product>> getAllProducts() {
        return ResponseEntity.ok(products);
    }

    @Operation(summary = "Get a product by ID", description = "Returns a single product with the given ID")
    @ApiResponse(responseCode = "200", description = "Successful retrieval of a product")
    @ApiResponse(responseCode = "404", description = "Product not found")
    @GetMapping("/{id}")
    public ResponseEntity<Product> getProductById(@Parameter(description = "ID of the product to retrieve") @PathVariable Long id) {
        Optional<Product> product = products.stream().filter(p -> p.getId().equals(id)).findFirst();
        if (product.isPresent()) {
            return ResponseEntity.ok(product.get());
        } else {
            return ResponseEntity.notFound().build();
        }
    }

    @Operation(summary = "Create a new product", description = "Creates a new product and returns the created product")
    @ApiResponse(responseCode = "201", description = "Product created successfully")
    @PostMapping
    public ResponseEntity<Product> createProduct(@RequestBody Product product) {
        product.setId((long) (products.size() + 1));
        products.add(product);
        return ResponseEntity.status(201).body(product);
    }

    // Add more methods as needed, e.g., update, delete
}
```

### 5. 配置 Swagger

创建一个配置类来启用 Swagger，并设置一些基本选项。

```java
package com.example.demo.config;

import io.swagger.v3.oas.models.OpenAPI;
import io.swagger.v3.oas.models.info.Info;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SwaggerConfig {

    @Bean
    public OpenAPI customOpenAPI() {
        return new OpenAPI()
                .info(new Info()
                        .title("Product API")
                        .version("1.0.0")
                        .description("A simple RESTful API for managing products"));
    }
}
```

### 6. 运行应用并查看 Swagger 文档

现在，你可以运行你的 Spring Boot 应用。默认情况下，Swagger UI 可以通过访问 `http://localhost:8080/swagger-ui.html` 来查看。你将看到一个交互式的界面，可以浏览和测试你的 API。

### 7. 测试 API

在 Swagger UI 界面中，你可以直接调用 API 方法，例如获取所有产品或创建新的产品。这有助于快速验证 API 的功能而无需编写额外的客户端代码。

这个示例展示了如何使用 Swagger 在 Spring Boot 项目中定义、配置和测试 RESTful API。通过这种方式，你可以轻松地为你的 API 生成详细的文档，并提供一个方便的接口供开发者进行测试。Swagger 不仅提高了开发效率，还增强了 API 的可维护性和可发现性。



## 集成express

在 Node.js 中使用 Swagger 通常涉及几个关键步骤：安装必要的依赖、配置 Swagger、定义 API 路由，并添加适当的注释来描述这些路由。下面我将通过一个简单的示例来展示如何在 Express 应用中集成 Swagger。

### 步骤 1: 创建一个新的 Node.js 项目

首先，创建一个新的目录并初始化一个新的 Node.js 项目：

```bash
mkdir my-swagger-app
cd my-swagger-app
npm init -y
```

### 步骤 2: 安装依赖

安装 Express 和 Swagger 相关的库：

```bash
npm install express
npm install --save-dev swagger-jsdoc swagger-ui-express
```

这里我们使用 `swagger-jsdoc` 来生成文档，`swagger-ui-express` 用来提供交互式的 API 文档界面。

### 步骤 3: 配置 Swagger

创建一个文件 `swagger.js` 来配置 Swagger：

```javascript
const swaggerJsdoc = require('swagger-jsdoc');
const swaggerUi = require('swagger-ui-express');

// Swagger 定义
const options = {
  definition: {
    openapi: '3.0.0',
    info: {
      title: 'My API',
      version: '1.0.0',
      description: 'A simple API to demonstrate Swagger integration with Node.js and Express'
    },
    servers: [
      {
        url: 'http://localhost:3000/api',
      }
    ],
  },
  apis: ['./routes/*.js'], // 指定包含 Swagger 注解的文件路径
};

const specs = swaggerJsdoc(options);

module.exports = (app) => {
  app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(specs));
};
```

### 步骤 4: 创建 API 路由

创建一个目录 `routes` 并在里面创建一个文件 `users.js` 来定义用户相关的 API 路由：

```javascript
/**
 * @swagger
 * tags:
 *   name: Users
 *   description: API endpoints for user management
 */

/**
 * @swagger
 * /api/users:
 *   get:
 *     summary: Returns a list of users
 *     tags: [Users]
 *     responses:
 *       200:
 *         description: A list of users
 *         content:
 *           application/json:
 *             schema:
 *               type: array
 *               items:
 *                 $ref: '#/components/schemas/User'
 *
 * components:
 *   schemas:
 *     User:
 *       type: object
 *       required:
 *         - id
 *         - name
 *       properties:
 *         id:
 *           type: integer
 *           description: The auto-generated id of the user
 *         name:
 *           type: string
 *           description: The name of the user
 *         email:
 *           type: string
 *           description: The email of the user
 *       example:
 *         id: 1
 *         name: John Doe
 *         email: john.doe@example.com
 */

const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  const users = [
    { id: 1, name: 'John Doe', email: 'john.doe@example.com' },
    { id: 2, name: 'Jane Doe', email: 'jane.doe@example.com' },
  ];
  res.json(users);
});

module.exports = router;
```

### 步骤 5: 设置 Express 应用

在你的主应用文件（例如 `app.js`）中，设置 Express 应用并加载路由和 Swagger 配置：

```javascript
const express = require('express');
const app = express();
const swaggerConfig = require('./swagger')(app); // 加载 Swagger 配置
const usersRouter = require('./routes/users'); // 加载用户路由

// 使用 JSON 中间件
app.use(express.json());

// 设置路由
app.use('/api/users', usersRouter);

// 启动服务器
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

### 步骤 6: 运行应用

现在你可以运行你的 Node.js 应用了：

```bash
node app.js
```

然后，在浏览器中访问 `http://localhost:3000/api-docs` 就可以看到自动生成的 API 文档了。

通过以上步骤，你已经成功地在 Node.js 和 Express 应用中集成了 Swagger。这个示例展示了如何定义 API 路由、添加 Swagger 注释以及配置 Swagger UI。这样，你就可以方便地为你的 API 提供详细的文档，并且可以轻松地进行测试。

## 集成@nestjs

在 NestJS 项目中使用 `@nestjs/swagger` 模块可以让你轻松地生成和维护 API 文档。这个模块是基于 OpenAPI 规范的，它能够自动生成文档，并且提供了一个交互式的 UI 来测试你的 API。下面我将详细介绍如何在 NestJS 应用程序中集成 Swagger。

### 步骤 1: 安装必要的依赖

首先，你需要安装 `@nestjs/swagger` 和 `swagger-ui-express`（如果你的应用使用 Express）或者 `fastify-swagger`（如果你的应用使用 Fastify）。这里我们假设你使用的是 Express：

```bash
npm install --save @nestjs/swagger swagger-ui-express
```

如果你使用的是 Fastify，则需要安装 `fastify-swagger` 而不是 `swagger-ui-express`：

```bash
npm install --save @nestjs/swagger fastify-swagger
```

### 步骤 2: 配置 SwaggerModule

接下来，在你的 `main.ts` 文件中配置 Swagger。你需要创建一个 `DocumentBuilder` 实例来定义 Swagger 文档的基本信息，然后使用 `SwaggerModule.createDocument()` 方法来创建文档对象。最后，使用 `SwaggerModule.setup()` 方法来设置 Swagger UI 的路径。

```typescript
import { NestFactory } from '@nestjs/core';
import { DocumentBuilder, SwaggerModule } from '@nestjs/swagger';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  // 创建 Swagger 文档选项
  const options = new DocumentBuilder()
    .setTitle('My Application')
    .setDescription('The my-application API description')
    .setVersion('1.0')
    .addTag('my-application')
    .build();

  // 生成 Swagger 文档
  const document = SwaggerModule.createDocument(app, options);
  // 设置 Swagger UI 的路径
  SwaggerModule.setup('api', app, document);

  await app.listen(3000);
}
bootstrap();
```

### 步骤 3: 在 DTO 中使用装饰器

为了使 Swagger 能够正确地反映你的 API 结构，你需要在数据传输对象 (DTO) 中添加适当的装饰器。例如，你可以使用 `@ApiProperty` 来描述属性。

```typescript
import { ApiProperty } from '@nestjs/swagger';

export class CreateUserDto {
  @ApiProperty({ description: 'The user name', example: 'John Doe' })
  name: string;

  @ApiProperty({ description: 'The user email', example: 'john.doe@example.com' })
  email: string;
}
```

### 步骤 4: 在控制器中使用装饰器

同样，你也需要在控制器的方法上使用装饰器来描述它们的功能。这包括使用 `@ApiOperation`、`@ApiResponse` 等来描述操作和响应。

```typescript
import { Controller, Post, Body } from '@nestjs/common';
import { ApiOperation, ApiResponse, ApiTags } from '@nestjs/swagger';
import { CreateUserDto } from './dto/create-user.dto';

@ApiTags('users')
@Controller('users')
export class UsersController {
  @Post()
  @ApiOperation({ summary: 'Create a new user' })
  @ApiResponse({ status: 201, description: 'User created successfully.' })
  @ApiResponse({ status: 400, description: 'Bad request.' })
  createUser(@Body() createUserDto: CreateUserDto) {
    // 处理创建用户逻辑
  }
}
```

### 步骤 5: 启动应用并查看 Swagger UI

现在，启动你的 NestJS 应用程序，然后访问 `http://localhost:3000/api`，你应该能看到 Swagger UI 页面，其中列出了所有可用的 API 端点以及它们的详细信息。

通过以上步骤，你就成功地在 NestJS 应用程序中集成了 Swagger。这样做不仅帮助开发者更好地理解 API，也为 API 的使用者提供了方便的接口测试工具。