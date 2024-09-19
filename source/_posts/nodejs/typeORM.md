---
title: "TypeORM介绍"
date: 2024-09-19
author: "pzc"
cover: /assets/images/jpg/28.jpg
categories: [nodejs]
tags: [Server,SQL]
---
TypeORM 是一个面向对象的 ORM（Object-Relational Mapping）框架，它允许开发者使用 TypeScript 或 JavaScript (ES5, ES6, ES7, ES8) 编写代码来操作数据库。TypeORM 支持多种数据库，包括 MySQL、PostgreSQL、MariaDB、SQLite、Microsoft SQL Server 等等，并且可以在 Node.js 环境中运行。

### 主要特点

1. **类型安全**：因为它是基于 TypeScript 开发的，所以可以利用 TypeScript 的类型系统，提供编译时的类型检查，减少运行时错误。

2. **实体映射**：通过定义实体类，可以将数据库中的表结构映射到应用程序中的对象，使得对数据库的操作更加直观和方便。

3. **查询构建器**：提供了强大的查询构建工具，可以轻松地构建复杂的 SQL 查询语句。

4. **事务支持**：支持事务处理，确保数据的一致性和完整性。

5. **迁移功能**：可以使用迁移脚本来管理数据库模式的变化，这有助于团队协作开发和版本控制。

6. **连接池**：内置了数据库连接池，能够有效地管理和复用数据库连接，提高应用性能。

7. **事件监听**：支持在执行 CRUD 操作前后触发自定义的事件处理器，便于实现业务逻辑。

8. **灵活的配置方式**：可以通过配置文件或代码来设置 TypeORM 的运行参数。

### 安装 TypeORM 和数据库驱动

首先，你需要安装 TypeORM 和相应的数据库驱动。以下是一些常见数据库的安装命令：

```bash
# 安装 TypeORM
npm install typeorm

# 安装 MySQL 驱动
npm install mysql2

# 安装 PostgreSQL 驱动
npm install pg

# 安装 SQLite 驱动
npm install sqlite3

# 安装 Microsoft SQL Server 驱动
npm install mssql
```

### 初始化项目

TypeORM 提供了一个 CLI 工具来帮助初始化项目和生成配置文件。首先需要全局安装 TypeORM CLI：

```bash
npm install -g typeorm
```

然后在项目根目录下初始化 TypeORM：

```bash
typeorm init --name MyProject --database mysql
```

这将生成一个基本的项目结构，包括 `src` 目录和 `ormconfig.json` 配置文件。

### 配置文件

TypeORM 的配置文件通常命名为 `ormconfig.json`，可以放在项目的根目录下。以下是一个示例配置：

```json
{
  "type": "mysql",
  "host": "localhost",
  "port": 3306,
  "username": "test",
  "password": "test",
  "database": "test",
  "entities": ["src/entity/**/*.ts"],
  "migrations": ["src/migration/**/*.ts"],
  "subscribers": ["src/subscriber/**/*.ts"],
  "synchronize": true,
  "logging": false
}
```

### 示例代码

这里是一个简单的 TypeORM 使用示例，展示如何定义一个实体并进行基本的增删改查操作：

```typescript
import { Entity, PrimaryGeneratedColumn, Column, CreateDateColumn, UpdateDateColumn } from 'typeorm';

@Entity()
export class User {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @Column()
    email: string;

    @CreateDateColumn()
    createdAt: Date;

    @UpdateDateColumn()
    updatedAt: Date;
}
```

接下来，你可以使用 `Connection` 对象来与数据库交互：

```typescript
import { createConnection, getRepository } from 'typeorm';
import { User } from './entity/User';

createConnection().then(async connection => {
    const userRepository = getRepository(User);

    // 创建新用户
    const user = new User();
    user.name = 'John Doe';
    user.email = 'john.doe@example.com';
    await userRepository.save(user);

    // 查询所有用户
    const users = await userRepository.find();
    console.log(users);
}).catch(error => console.log(error));
```

### 核心概念

#### 1. 实体（Entities）
实体是 TypeORM 中的核心概念，它们代表了数据库中的表。每个实体都是一个 TypeScript 类，通过装饰器来描述该类的属性与数据库表字段之间的映射关系。

```typescript
import { Entity, PrimaryGeneratedColumn, Column } from 'typeorm';

@Entity()
export class User {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    firstName: string;

    @Column()
    lastName: string;

    @Column({ unique: true })
    email: string;
}
```

#### 2. 装饰器（Decorators）
TypeORM 提供了一系列装饰器来帮助定义实体及其属性。常见的装饰器有：
- `@Entity()`：标记一个类为实体。
- `@PrimaryGeneratedColumn()`：定义主键，通常是自增长的。
- `@Column()`：定义普通的列。
- `@ManyToOne()`, `@OneToMany()`, `@OneToOne()`, `@ManyToMany()`：定义关联关系。
- `@BeforeInsert()`, `@AfterInsert()`, `@BeforeUpdate()`, `@AfterUpdate()`, `@BeforeRemove()`, `@AfterRemove()`：定义生命周期钩子。

#### 3. 连接（Connections）
连接是与数据库建立会话的过程。TypeORM 允许在一个应用中配置多个数据库连接。

```typescript
import { createConnection } from 'typeorm';

createConnection({
    type: 'mysql',
    host: 'localhost',
    port: 3306,
    username: 'test',
    password: 'test',
    database: 'test',
    entities: [User],
    synchronize: true,
    logging: false,
}).then(connection => {
    console.log('Database connection established');
}).catch(error => console.error('Database connection error:', error));
```

### 高级特性

#### 1. 关联关系（Relations）
TypeORM 支持多种类型的关联关系，如一对一、一对多、多对一和多对多关系。

```typescript
@Entity()
export class Post {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    title: string;

    @ManyToOne(type => User, user => user.posts)
    author: User;
}

@Entity()
export class User {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @OneToMany(type => Post, post => post.author)
    posts: Post[];
}
```

#### 2. 查询构建器（Query Builder）
TypeORM 提供了一个强大的查询构建器，可以用来构建复杂的 SQL 查询。

```typescript
const posts = await connection.getRepository(Post)
    .createQueryBuilder("post")
    .where("post.title = :title", { title: "Hello" })
    .leftJoinAndSelect("post.author", "author")
    .getMany();
```

#### 3. 事务（Transactions）
TypeORM 支持事务管理，确保一系列操作的原子性。

```typescript
await connection.transaction(async transactionalEntityManager => {
    await transactionalEntityManager.save(post1);
    await transactionalEntityManager.save(post2);
});
```

#### 4. 数据库迁移（Migrations）
TypeORM 提供了命令行工具来生成和执行数据库迁移脚本，帮助开发者管理数据库模式的变化。

```bash
typeorm migration:create -n AddUserEmail
typeorm migration:run
```
### 常用命令

#### 1. 连接到数据库

```bash
typeorm connection:show
```

#### 2. 生成实体

```bash
typeorm entity:create -n User
```

这将在 `src/entity` 目录下生成一个 `User.ts` 文件。

#### 3. 生成迁移文件

```bash
typeorm migration:create -n AddUserTable
```

这将在 `src/migration` 目录下生成一个迁移文件，例如 `1634567890123-AddUserTable.ts`。

#### 4. 运行迁移

```bash
typeorm migration:run
```

这将执行所有未运行的迁移文件，将数据库模式更新到最新状态。

#### 5. 回滚迁移

```bash
typeorm migration:revert
```

这将回滚最近一次运行的迁移文件。

#### 6. 列出所有迁移

```bash
typeorm migration:show
```

这将列出所有已运行和未运行的迁移文件。

#### 7. 生成并运行迁移

```bash
typeorm schema:log
```

这将显示当前数据库模式与实体定义之间的差异。

```bash
typeorm schema:sync
```

这将同步数据库模式与实体定义，但不建议在生产环境中使用，因为它可能会导致数据丢失。

```bash
typeorm schema:drop
```

这将删除所有表，同样不建议在生产环境中使用。

#### 8. 生成订阅者

```bash
typeorm subscriber:create -n UserSubscriber
```

这将在 `src/subscriber` 目录下生成一个订阅者文件，例如 `UserSubscriber.ts`。

### 最佳实践

1. **环境变量**：使用环境变量来存储数据库连接信息和其他敏感数据，避免硬编码。
2. **错误处理**：在处理数据库操作时，添加适当的错误处理机制，以保证系统的健壮性。
3. **测试**：编写单元测试和集成测试，确保数据库操作的正确性和性能。
4. **性能优化**：合理设计索引，避免不必要的关联查询，使用缓存机制提高读取性能。
5. **安全性**：防止 SQL 注入攻击，使用参数化查询或 ORM 提供的安全方法。

### 总结

TypeORM 是一个功能丰富且灵活的 ORM 框架，特别适合用于需要处理复杂数据库操作的 Node.js 应用程序。通过合理的配置和使用，可以显著提升开发效率，同时保持代码的可维护性和扩展性。希望上述介绍能帮助你更好地理解和使用 TypeORM。


