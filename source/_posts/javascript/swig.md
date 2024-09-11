---
title: swig介绍
author: pzc
date: 2024-09-11
cover: /assets/images/jpg/21.jpg
categories: [JavaScript]
tags: [template]
---
Swig 是一个流行的模板引擎，用于在 Node.js 应用程序中生成文本输出，尤其是在 web 开发中用于生成 HTML 页面。Swig 受到 Django 模板引擎的启发，因此它的语法和 Django 类似，但它是专门为 Node.js 编写的。

### 特点

- **灵活性**：Swig 允许你在模板中嵌入 JavaScript 代码，这意味着你可以在模板中执行任何 JavaScript 逻辑。
- **丰富的标签和过滤器**：Swig 提供了一系列的标签和过滤器，用于控制流和数据处理。
- **易用性**：Swig 的语法清晰简洁，容易学习和使用。
- **跨平台**：Swig 是用 JavaScript 编写的，可以在任何支持 Node.js 的环境中运行。

### 基本语法

Swig 使用双大括号 `{% %}` 和 `{{ }}` 作为模板标签和变量插值的分隔符。以下是一些常见的 Swig 语法：

- **变量插值**：`{{ variable }}` 用于输出变量的值。
- **条件语句**：`{% if condition %}`...`{% endif %}` 用于条件判断。
- **循环**：`{% for item in list %}`...`{% endfor %}` 用于遍历数组。
- **块**：`{% block content %}`...`{% endblock %}` 用于定义可被子模板继承的部分。

### 示例

下面是一个简单的 Swig 模板示例：

```html
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Site{% endblock %}</title>
</head>
<body>
    <header>
        <h1><a href="/">Home</a></h1>
    </header>
    <main>
        {% block content %}
            <h2>Welcome!</h2>
            <p>This is some sample text.</p>
        {% endblock %}
    </main>
    <footer>
        <p>&copy; 2024 My Company</p>
    </footer>
</body>
</html>
```

在这个例子中，`{% block title %}` 和 `{% block content %}` 是可以被继承的区域，子模板可以覆盖这些区域以改变特定部分的内容。

### 安装和使用 Swig

要使用 Swig，你需要首先安装 Swig 包：

```bash
npm install swig
```

然后在 Node.js 应用程序中使用 Swig：

```javascript
const swig = require('swig');
swig.setDefaults({ cache false });

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

在这个示例中，`swig.compileFile()` 用于编译模板文件，`context` 对象包含了模板中使用的变量。

### 在 Hexo 中的使用

在 Hexo 中，默认使用 Swig 作为模板引擎。你可以在 Hexo 主题的 `_layout` 目录下找到 Swig 模板文件。这些文件定义了你的博客页面的布局和结构。

Swig 是一个强大且灵活的模板引擎，非常适合用于生成静态页面或动态内容。它可以帮助开发者快速地生成结构化的 HTML 输出，并且可以很容易地集成到现有的 Node.js 项目中。

### 模板标签

在模板文件中，你可以使用模板引擎特有的标签来插入动态内容，比如文章标题、作者信息等。以下是一些常见的模板标签示例：

- **变量插值**：用于显示变量的值，如 `<%= post.title %>`。
- **循环**：用于遍历数组或对象，如 `{% for post in posts %}`。
- **条件语句**：用于根据条件显示内容，如 `{% if user.is_admin %}`。
- **继承和嵌套**：允许你定义一个基础模板，然后让其他模板继承该基础模板并覆盖或扩展某些部分。

### 常见的模板文件

- **default.swig**：这是默认布局，可以被其他布局继承。
- **post.swig**：用于展示单独的文章页面。
- **archive.swig**：用于展示归档页面。
- **tag.swig**：用于展示标签页面。
- **category.swig**：用于展示分类页面。
- **index.swig**：首页或索引页面。

### 示例

这里是一个简单的 Swig 模板示例，用于展示文章列表：

```swig
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}{{ config.title }}{% endblock %}</title>
</head>
<body>
    <header>
        <h1><a href="{{ config.url }}">{{ config.title }}</a></h1>
    </header>
    <main>
        {% block content %}
            <ul>
                {% for post in site.posts %}
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

在这个例子中，我们定义了一个基本的 HTML 结构，并使用 Swig 语法来插入动态内容，比如文章标题和日期。
