---
title: "handlebars"
date: 2024-12-19
author: "pzc"
cover: /assets/images/jpg/129.jpg
categories: [nodejs]
tags: [Template]
---
## 介绍

Handlebars 是一种用于生成模板的逻辑无感知（logic-less）模板引擎，广泛应用于Web开发中。它允许开发者定义模板文件，这些文件包含了静态HTML和一些特殊的语法标记，用于插入动态内容或控制结构（如条件语句和循环）。Handlebars 模板可以在服务器端（例如使用 Node.js）或客户端（浏览器中）进行渲染。

### 特点

- **逻辑无感知**：Handlebars 强调模板应该尽可能地简单，不包含复杂的业务逻辑。
- **可扩展性**：通过自定义辅助函数（helpers），可以添加特定的功能或逻辑到模板中。
- **部分模板（Partials）**：支持将常用代码片段提取为部分模板，以便在多个地方重用。
- **兼容 Mustache**：Handlebars 是 Mustache 的超集，意味着所有的 Mustache 模板都可以在 Handlebars 中正常工作，但 Handlebars 提供了更多的功能。

### 基本语法

- **表达式**：`{{expression}}` 用来输出变量值。
- **转义输出**：默认情况下，Handlebars 会自动对输出进行HTML转义以防止XSS攻击。
- **非转义输出**：`{{{expression}}}` 用于直接输出未经转义的内容。
- **注释**：`{{! this is a comment }}`
- **条件语句**：`{{#if condition}}{{/if}}` 和 `{{#unless condition}}{{/unless}}`
- **循环**：`{{#each array}}{{/each}}` 用来遍历数组或对象。

### 辅助函数（Helpers）

Handlebars 支持创建自定义的辅助函数来增强模板的功能。例如，你可以创建一个辅助函数来格式化日期、执行数学运算或构建更复杂的条件逻辑。

```javascript
Handlebars.registerHelper('ifeq', function(a, b, opts) {
  if (a == b) { 
    return opts.fn(this); 
  } else { 
    return opts.inverse(this); 
  }
});
```

### 部分模板（Partials）

部分模板是预定义的模板片段，可以在主模板中重复使用。它们有助于保持代码的DRY原则（Don't Repeat Yourself）。

```handlebars
{{> header }}
<!-- Main content -->
{{> footer }}
```

### 使用场景

- **服务器端渲染**：在Node.js应用中使用Express等框架与Handlebars结合，实现动态页面生成。
- **客户端模板**：在前端JavaScript应用中使用，特别是单页应用（SPA），用于根据用户交互更新页面的部分内容。
- **电子邮件模板**：用于构建基于用户数据定制的邮件内容。

## 资料

以下是一些关于 Handlebars 的详细资料和学习资源，帮助您更好地理解和使用这个强大的模板引擎。

### 官方文档

- **[Handlebars 官方网站](https://handlebarsjs.com/)**：这是获取最新信息、API 参考和官方教程的最佳地点。官方网站提供了详尽的指南，包括安装方法、基本语法、辅助函数、部分模板等内容。

### 社区和支持

- **GitHub Issues**：如果遇到 bug 或者想要请求新功能，可以在 Handlebars 的 GitHub 仓库中提交 issue。

### 实践项目

尝试构建一些小型项目来加深理解：

- **博客系统**：创建一个简单的博客应用，其中包含文章列表、单个文章页面等，利用 Handlebars 来动态生成 HTML。

### 高级主题

一旦掌握了基础知识，您可以探索更高级的主题，比如：

- **自定义辅助函数**：编写自己的辅助函数来处理日期格式化、字符串操作等任务。
- **预编译模板**：为了提高性能，可以提前编译 Handlebars 模板，然后在运行时使用预编译的结果。
- **集成与框架**：了解如何将 Handlebars 集成到像 Express、Next.js 等服务器端 JavaScript 框架中，或作为客户端库的一部分。
## 示例

下面是一个完整的 Handlebars 示例，包括创建自定义辅助函数、使用部分模板、预编译模板以及在 Node.js 中集成和渲染这些模板。这个例子将展示如何构建一个简单的博客系统，该系统可以列出文章并显示单个文章的详细信息。

### 1. 设置项目

首先，确保你已经安装了 Node.js 和 npm。然后创建一个新的项目目录，并初始化 npm：

```bash
mkdir handlebars-blog
cd handlebars-blog
npm init -y
```

安装必要的依赖包：

```bash
npm install express handlebars
```

### 2. 创建服务器文件

创建一个名为 `server.js` 的文件，作为项目的入口点：

```javascript
const express = require('express');
const exphbs = require('express-handlebars');
const path = require('path');
const fs = require('fs');

// 初始化 Express 应用
const app = express();
const port = process.env.PORT || 3000;

// 配置 Handlebars 引擎
app.engine('.hbs', exphbs.engine({ extname: '.hbs' }));
app.set('view engine', '.hbs');
app.set('views', path.join(__dirname, 'views'));

// 自定义辅助函数
const hbs = require('handlebars');
hbs.registerHelper('formatDate', (date) => {
  return new Date(date).toLocaleDateString();
});

// 模拟数据
const articles = [
  { id: 1, title: 'First Post', content: 'This is the content of the first post.', createdAt: new Date() },
  { id: 2, title: 'Second Post', content: 'This is the content of the second post.', createdAt: new Date() }
];

// 路由
app.get('/', (req, res) => {
  res.render('home', { articles });
});

app.get('/article/:id', (req, res) => {
  const article = articles.find(a => a.id == req.params.id);
  if (!article) return res.status(404).send('Article not found');
  res.render('article', { article });
});

// 启动服务器
app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

### 3. 创建视图文件夹和模板

在项目根目录下创建一个 `views` 文件夹，用于存放所有的 Handlebars 模板文件。

#### 主布局（`layout.hbs`）

```handlebars
<!DOCTYPE html>
<html>
<head>
  <title>Blog</title>
</head>
<body>
  {{{body}}}
</body>
</html>
```

#### 首页模板（`home.hbs`）

```handlebars
{{> header }}

<h1>Welcome to My Blog</h1>

<ul>
  {{#each articles}}
    <li>
      <a href="/article/{{id}}">{{title}}</a> - Published on {{ formatDate createdAt }}
    </li>
  {{/each}}
</ul>

{{> footer }}
```

#### 文章详情模板（`article.hbs`）

```handlebars
{{> header }}

<h1>{{article.title}}</h1>
<p>{{article.content}}</p>
<p>Published on {{ formatDate article.createdAt }}</p>

<a href="/">Back to Home</a>

{{> footer }}
```

#### 部分模板（`_header.hbs` 和 `_footer.hbs`）

创建两个部分模板文件 `_header.hbs` 和 `_footer.hbs` 来共享头部和尾部内容：

- `_header.hbs`

```handlebars
<header>
  <h1>My Awesome Blog</h1>
  <nav>
    <a href="/">Home</a>
  </nav>
</header>
```

- `_footer.hbs`

```handlebars
<footer>
  <p>&copy; 2024 My Awesome Blog</p>
</footer>
```

### 4. 运行应用

确保所有文件都已正确创建后，在命令行中运行以下命令启动服务器：

```bash
node server.js
```

打开浏览器并访问 `http://localhost:3000`，你应该能看到博客首页，点击文章链接可以查看每篇文章的详细信息。

### 5. 预编译模板（可选）

为了提高性能，你可以选择预编译 Handlebars 模板。这需要额外安装 `handlebars-cli` 工具：

```bash
npm install -g handlebars-cli
```

然后，使用它来预编译你的模板：

```bash
handlebars views/*.hbs -f compiledTemplates.js
```

最后，在 `server.js` 中加载这些预编译的模板：

```javascript
const templates = require('./compiledTemplates');
// 使用预编译的模板...
```

请注意，上面的代码片段仅用于说明如何加载预编译的模板；实际实现会根据你的项目结构有所不同。
## 进阶

下面是对 Handlebars 的一些进阶特性和概念的介绍。掌握这些特性将有助于您更高效地使用 Handlebars 创建复杂且动态的应用程序。

### 1. 自定义辅助函数（Custom Helpers）

Handlebars 允许你创建自定义辅助函数来扩展模板的功能。这可以包括逻辑判断、数学运算、日期格式化等。你可以通过 `Handlebars.registerHelper` 方法注册一个全局可用的辅助函数。

```javascript
// 注册一个简单的辅助函数用于比较两个值是否相等
Handlebars.registerHelper('ifCond', function(v1, operator, v2, options) {
  switch (operator) {
    case '==':
      return (v1 == v2) ? options.fn(this) : options.inverse(this);
    // 可以添加更多条件...
  }
});
```

### 2. 部分模板（Partials）

部分模板是预定义的模板片段，可以在主模板中重复使用。这对于构建可维护和模块化的模板非常有用。你可以使用 `{{> partialName }}` 来引用部分模板，并且可以通过 `@partial-block` 访问传递给部分模板的内容。

```handlebars
<!-- _header.partial.hbs -->
<header>
  <h1>{{title}}</h1>
</header>

<!-- main template -->
{{> _header }}
```

此外，还可以传递上下文或参数给部分模板：

```handlebars
{{> _userProfile user }}
```

### 3. 预编译模板（Precompilation）

为了提高性能，尤其是在生产环境中，你可以提前编译 Handlebars 模板。预编译会生成 JavaScript 函数，这些函数在运行时可以直接调用，而不需要再解析模板字符串。

```bash
# 使用命令行工具预编译模板
handlebars file.hbs -f compiledTemplate.js
```

然后，在你的应用中加载并使用这些预编译的模板：

```javascript
const template = require('./compiledTemplate');
const html = template(data);
```

### 4. 内置辅助函数（Built-in Helpers）

Handlebars 提供了一些内置的辅助函数，如 `each`、`if`、`unless` 等，它们可以帮助你在模板中实现循环和条件逻辑。了解如何有效利用这些内置辅助函数对于编写简洁的模板非常重要。

- **`each`**：遍历数组或对象。
- **`if` 和 `unless`**：基于表达式的真假来包含或排除模板部分。
- **`with`**：改变当前上下文。

### 5. 上下文与路径（Context and Paths）

理解 Handlebars 中的上下文转换和路径查找规则对于正确引用数据至关重要。例如，在嵌套结构中，你可以使用相对路径 `../` 回退到父级上下文，或者使用绝对路径 `/` 从根开始查找。

```handlebars
{{#each items}}
  {{name}} - {{../category.name}}
{{/each}}
```

### 6. 数据绑定（Data Binding）

虽然 Handlebars 是一种无逻辑的模板引擎，但它仍然支持双向数据绑定库（如 Ember.js）中的单向数据流模式。这意味着当模型数据更新时，视图也会相应更新。如果你正在构建一个交互式应用，考虑结合这些技术来增强用户体验。

### 7. 安全性与转义（Security and Escaping）

默认情况下，Handlebars 会对输出进行HTML转义以防止XSS攻击。然而，有时候你需要输出未经转义的原始HTML，这时可以使用三重大括号 `{{{ }}}`。但是，请务必谨慎使用，确保不会引入安全风险。

```handlebars
{{{rawHtmlContent}}}
```

### 8. 插件系统（Plugin System）

Handlebars 支持插件扩展其功能。例如，有插件可以提供额外的辅助函数集合，或是改进模板加载器的行为。探索社区提供的插件可以为你的项目增添更多灵活性。

