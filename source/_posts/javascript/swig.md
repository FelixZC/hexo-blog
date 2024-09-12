---
title: swig介绍
author: pzc
date: 2024-09-11
cover: /assets/images/jpg/21.jpg
categories: [JavaScript]
tags: [template]
---
### Swig 模板引擎介绍

Swig 是一个用于 Node.js 的轻量级模板引擎，它被设计用来生成 HTML 页面以及其他类型的文本输出。Swig 的设计灵感来源于 Django 模板引擎，但它是专门为 Node.js 应用程序而定制的。Swig 提供了一种简单而强大的方式来渲染动态内容。

### 特点

- **灵活性**：Swig 允许在模板中嵌入 JavaScript 代码片段，这意味着你可以在模板内部执行复杂的逻辑。
- **丰富的标签和过滤器**：Swig 提供了多种标签和过滤器，帮助开发者控制模板的流控制和数据处理。
- **易用性**：Swig 的语法清晰简洁，易于学习和使用。
- **跨平台**：Swig 作为一个 Node.js 库，可以在任何支持 Node.js 的环境中运行。
- **继承**：Swig 支持模板继承，使得复用代码变得更加容易。

### 基本语法

Swig 使用不同的分隔符来标记模板中的特殊部分：

- **变量插值**：使用双花括号 `{{ }}` 来输出变量的值。
- **控制流语句**：使用百分号加花括号 `{% %}` 来编写条件语句和循环。
- **注释**：使用两个百分号 `{##}` 来插入注释。
- **块**：使用 `{% block %}` 和 `{% endblock %}` 来定义可以被继承的模板区域。

### 安装 Swig

要使用 Swig，你需要首先安装 Swig 包。可以通过 npm（Node Package Manager）来安装：

```bash
npm install swig
```

### 使用 Swig

一旦安装了 Swig，你可以在 Node.js 应用程序中使用它来编译和渲染模板：

```javascript
const swig = require('swig');
swig.setDefaults({ cache: false });

// 编译模板文件
let template = swig.compileFile('path/to/template.swig');

// 渲染模板
let context = {
    title: 'Hello Swig',
    items: ['item1', 'item2', 'item3']
};
let html = template(context);

console.log(html);
```

### 示例模板

下面是一个简单的 Swig 模板示例：

```swig
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}Default Title{% endblock %}</title>
</head>
<body>
    <header>
        <h1><a href="/">Home</a></h1>
    </header>
    <main>
        {% block content %}
            <h2>Welcome to the default page!</h2>
            <p>This is a simple example of Swig template engine.</p>
        {% endblock %}
    </main>
    <footer>
        <p>&copy; 2024 Example Inc.</p>
    </footer>
</body>
</html>
```

在这个模板中，我们定义了两个块 `block title` 和 `block content`。这些块可以被子模板继承并重写。

### 继承示例

接下来，我们可以创建一个继承上述模板的子模板：

```swig
{% extends "base.swig" %}

{% block title %}Child Page Title{% endblock %}

{% block content %}
    <h2>This is a child template</h2>
    <p>Overriding content from base template.</p>
{% endblock %}
```

这个子模板继承了 `base.swig` 模板，并重写了 `title` 和 `content` 块的内容。

### Hexo 中的使用

在 Hexo 中，Swig 作为默认模板引擎之一被广泛使用。你可以创建 Hexo 主题并在 `_layout` 目录下编写 Swig 模板文件来定义页面布局。

### 模板标签和过滤器

Swig 提供了多种内置的标签和过滤器，用于简化模板的编写过程。以下是一些常见的标签和过滤器示例：

- **变量插值**：`{{ variable }}` 用于输出变量的值。
- **循环**：`{% for item in items %}` 用于遍历集合。
- **条件语句**：`{% if condition %}` 用于条件判断。
- **过滤器**：`| lower` 可以用于转换字符串为小写形式。

### 完整示例

下面是一个更详细的 Swig 模板示例，用于展示文章列表：

```swig
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Blog{% endblock %}</title>
</head>
<body>
    <header>
        <h1><a href="{{ config.url }}">{{ config.title }}</a></h1>
    </header>
    <main>
        {% block content %}
            <ul>
                {% for post in posts %}
                    <li><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date:'YYYY-MM-DD' }}</li>
                {% endfor %}
            </ul>
        {% endblock %}
    </main>
    <footer>
        <p>&copy; {{ config.copyright }}</p>
    </footer>
</body>
</html>
```

在这个示例中，我们定义了一个基本的 HTML 结构，并使用 Swig 语法来插入动态内容，如文章标题和发布日期。

Swig 是一个强大且灵活的模板引擎，非常适合用于生成静态页面或动态内容。它可以帮助开发者快速地生成结构化的 HTML 输出，并且可以很容易地集成到现有的 Node.js 项目中。