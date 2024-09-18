---
title: Maven命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Maven,Backend,Package]
---
Maven 是一个强大的项目管理和构建工具，主要用于 Java 项目。它通过 POM（Project Object Model）文件（即 `pom.xml`）来管理项目的构建、依赖和文档。以下是一些常用的 Maven 命令，可以帮助你管理和构建项目。

### 基础命令

- **初始化项目**
  - `mvn archetype:generate`：生成一个新的 Maven 项目。
  - `mvn archetype:generate -DgroupId=com.example -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`：生成一个简单的 Java 项目。

- **查看帮助**
  - `mvn help:help`：显示 Maven 的帮助信息。
  - `mvn help:describe -Dcmd=install`：显示特定命令的详细信息。

### 构建和编译

- **编译源代码**
  - `mvn compile`：编译项目的源代码。

- **编译测试代码**
  - `mvn test-compile`：编译项目的测试代码。

- **运行测试**
  - `mvn test`：运行项目的测试用例。

- **打包项目**
  - `mvn package`：打包项目，生成 JAR、WAR 等文件。

- **安装到本地仓库**
  - `mvn install`：将项目安装到本地 Maven 仓库，通常位于 `~/.m2/repository`。

- **部署到远程仓库**
  - `mvn deploy`：将项目部署到远程仓库，需要在 `pom.xml` 中配置仓库信息。

### 清理

- **清理构建输出**
  - `mvn clean`：删除构建输出目录，通常为 `target/`。

### 生命周期阶段

- **默认生命周期**
  - `validate`：验证项目的正确性。
  - `compile`：编译项目的源代码。
  - `test`：运行测试用例。
  - `package`：打包项目。
  - `verify`：验证包是否有效。
  - `install`：将包安装到本地仓库。
  - `deploy`：将包部署到远程仓库。

- **站点生命周期**
  - `pre-site`：执行站点生成前的操作。
  - `site`：生成项目站点文档。
  - `post-site`：执行站点生成后的操作。
  - `site-deploy`：将生成的站点文档部署到服务器。

- **清理生命周期**
  - `pre-clean`：执行清理前的操作。
  - `clean`：清理构建输出目录。
  - `post-clean`：执行清理后的操作。

### 依赖管理

- **下载依赖**
  - `mvn dependency:resolve`：下载项目所需的依赖。

- **查看依赖树**
  - `mvn dependency:tree`：显示项目的依赖树。

- **分析依赖**
  - `mvn dependency:analyze`：分析项目的依赖，显示未使用的依赖和未声明的依赖。

### 插件管理

- **查看插件帮助**
  - `mvn help:describe -Dplugin=org.apache.maven.plugins:maven-compiler-plugin`：显示特定插件的详细信息。

- **运行插件目标**
  - `mvn plugin:goal`：运行插件的特定目标。
  - 例如：`mvn compiler:compile` 编译源代码。

### 调试和日志

- **查看详细日志**
  - `mvn -X`：启用调试模式，显示详细的日志信息。

- **指定日志级别**
  - `mvn --debug`：启用调试日志。
  - `mvn --quiet`：启用安静模式，减少日志输出。

### 多模块项目

- **构建多模块项目**
  - `mvn clean install`：清理并安装所有模块。

- **构建特定模块**
  - `mvn -pl module-name clean install`：构建特定的模块。

- **构建模块及其依赖**
  - `mvn -pl module-name -am clean install`：构建特定模块及其依赖的模块。

### 其他实用命令

- **生成项目文档**
  - `mvn site`：生成项目的站点文档。

- **生成项目依赖报告**
  - `mvn dependency:sources`：下载项目依赖的源代码。
  - `mvn dependency:resolve-plugins`：解析项目依赖的插件。

- **查看项目信息**
  - `mvn help:effective-pom`：显示有效的 POM 文件，包括继承和属性替换后的结果。
  - `mvn help:effective-settings`：显示有效的设置文件，包括继承和属性替换后的结果。

### 示例

假设你有一个名为 `my-app` 的 Maven 项目，包含多个模块，你可以使用以下命令：

- **初始化项目**
  ```sh
  mvn archetype:generate -DgroupId=com.example -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
  ```

- **编译项目**
  ```sh
  mvn compile
  ```

- **运行测试**
  ```sh
  mvn test
  ```

- **打包项目**
  ```sh
  mvn package
  ```

- **安装到本地仓库**
  ```sh
  mvn install
  ```

- **部署到远程仓库**
  ```sh
  mvn deploy
  ```

- **查看依赖树**
  ```sh
  mvn dependency:tree
  ```

- **构建特定模块**
  ```sh
  mvn -pl module-name clean install
  ```

- **生成项目文档**
  ```sh
  mvn site
  ```

这些命令涵盖了 Maven 的大多数常用功能。