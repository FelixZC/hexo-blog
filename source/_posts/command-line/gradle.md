---
title: Gradle命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Gradle,Package]
---
Gradle 是一个基于 Groovy 的构建工具，广泛用于 Java、Android 和其他语言的项目构建。以下是 Gradle 的一些常用命令，可以帮助你管理和构建项目。

### 基础命令

- **初始化项目**
  - `gradle init`：初始化一个新的 Gradle 项目。

- **查看帮助**
  - `gradle help`：显示 Gradle 的帮助信息。
  - `gradle help --task [task-name]`：显示特定任务的帮助信息。

- **查看项目结构**
  - `gradle projects`：显示项目的层次结构。
  - `gradle tasks`：列出项目中所有可用的任务。

### 构建和编译

- **构建项目**
  - `gradle build`：构建项目，包括编译、测试和打包。

- **编译代码**
  - `gradle compileJava`：编译 Java 源代码。
  - `gradle compileTestJava`：编译测试代码。

- **清理构建输出**
  - `gradle clean`：删除构建输出目录，通常为 `build/`。

### 测试

- **运行测试**
  - `gradle test`：运行项目的测试用例。

- **生成测试报告**
  - `gradle test --tests [test-class-or-method]`：运行特定的测试类或方法。

### 打包

- **生成 JAR 文件**
  - `gradle jar`：生成 JAR 文件。
  - `gradle bootJar`：对于 Spring Boot 项目，生成可执行的 JAR 文件。

- **生成 WAR 文件**
  - `gradle war`：生成 WAR 文件。

### 发布

- **发布到 Maven 仓库**
  - `gradle publish`：将构建的工件发布到 Maven 仓库。

### 依赖管理

- **查看依赖树**
  - `gradle dependencies`：显示项目的依赖树。
  - `gradle dependencyInsight --dependency [dependency-name]`：显示特定依赖的详细信息。

- **下载依赖**
  - `gradle build --refresh-dependencies`：强制重新下载所有依赖。

### 性能优化

- **启用离线模式**
  - `gradle build --offline`：在没有网络连接的情况下构建项目。

- **启用构建缓存**
  - `gradle build --build-cache`：启用构建缓存，加速后续构建。

### 调试和日志

- **查看详细日志**
  - `gradle build --info`：显示详细的信息日志。
  - `gradle build --debug`：显示调试级别的日志。

- **查看堆栈跟踪**
  - `gradle build --stacktrace`：在发生错误时显示完整的堆栈跟踪。

### 自定义任务

- **运行自定义任务**
  - `gradle [task-name]`：运行自定义的 Gradle 任务。

- **查看任务详情**
  - `gradle [task-name] --info`：显示特定任务的详细信息。

### 多模块项目

- **构建特定模块**
  - `gradle :module-name:build`：构建特定的模块。

- **查看多模块项目结构**
  - `gradle projects`：显示多模块项目的层次结构。

### 其他实用命令

- **检查项目健康**
  - `gradle check`：运行项目的各种检查任务，如静态代码分析和单元测试。

- **生成文档**
  - `gradle javadoc`：生成 Java 文档。
  - `gradle dokkaHtml`：生成 Kotlin 文档（需要 Dokka 插件）。

- **查看 Gradle 版本**
  - `gradle -v`：显示 Gradle 的版本信息。

### 示例

假设你有一个名为 `my-app` 的项目，包含多个模块，你可以使用以下命令：

- **初始化项目**
  ```sh
  gradle init
  ```

- **构建项目**
  ```sh
  gradle build
  ```

- **清理项目**
  ```sh
  gradle clean
  ```

- **运行测试**
  ```sh
  gradle test
  ```

- **查看依赖树**
  ```sh
  gradle dependencies
  ```

- **构建特定模块**
  ```sh
  gradle :module-name:build
  ```

- **生成 JAR 文件**
  ```sh
  gradle jar
  ```

- **发布到 Maven 仓库**
  ```sh
  gradle publish
  ```

这些命令涵盖了 Gradle 的大多数常用功能。