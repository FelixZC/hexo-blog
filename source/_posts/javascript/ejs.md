---
title: ejs介绍
author: pzc
date: 2024-09-11
cover: /assets/images/jpg/22.jpg
categories: [JavaScript]
tags: [template]
---
EJS (Embedded JavaScript Templates) 是一个简单的JavaScript模板引擎，它允许你在 HTML 文件中嵌入 JavaScript 代码以生成动态的内容。EJS 设计得非常灵活，可以用来生成任何格式的数据，不仅仅是 HTML，比如 XML、JSON 等。以下是 EJS 的一些特点：

- **语法简洁**：EJS 提供了一种简单的标签语法，可以在 HTML 中插入 JavaScript 表达式，也可以包含任意的 JavaScript 代码块。
- **嵌入式 JavaScript**：EJS 允许在模板中直接编写 JavaScript 逻辑，这使得数据处理和页面生成非常直观。
- **非侵入性**：EJS 不强制使用特定的标签或语法糖，你可以选择使用或不使用标签来标记 JavaScript 区域。
- **强大的功能**：尽管 EJS 的核心是轻量级的，但它可以通过插件和其他工具扩展功能，例如循环、条件判断等。
- **易用性**：由于它是基于 JavaScript 的，所以对于熟悉 JavaScript 的开发者来说很容易上手。

### 基本用法示例

假设你有一个简单的 EJS 模板文件 `index.ejs`：

```html
<!DOCTYPE html>
<html>
<head>
    <title><%= title %></title>
</head>
<body>
    <h1>Welcome <%= name %>!</h1>
    <% items.forEach(item => { %>
        <p><%= item %></p>
    <% }) %>
</body>
</html>
```

在这个例子中，`<%= %>` 标签用于输出变量值，`<% %>` 标签内的内容是 JavaScript 代码块，可以用来执行逻辑操作。

### 如何使用 EJS

要在 Node.js 项目中使用 EJS，你需要先安装 EJS 包：

```bash
npm install ejs
```

然后，在你的 Node.js 应用程序中，你可以这样渲染一个 EJS 模板：

```javascript
const ejs = require('ejs');
const fs = require('fs');

let data = {
    title: 'Hello World',
    name: 'User',
    items: ['Item 1', 'Item 2', 'Item 3']
};

ejs.renderFile('./views/index.ejs', data, {}, function(err, str){
    if (err){ 
        console.log("Error rendering file", err);
    } else {
        // str is the rendered string
        console.log(str);
        fs.writeFile('output.html', str, function(err) {
            if (err) throw err;
            console.log('File is created successfully.');
        });
    }
});
```

这个例子展示了如何将一个 EJS 模板渲染成 HTML 字符串，并将其写入到文件中。

EJS 是一个非常适合 Web 开发的模板引擎，因为它可以很好地与 Node.js 集成，同时也适用于生成静态页面或其他类型的数据文件。


### EJS在Hexo的应用
Hexo 是一个快速、简洁且高效的博客框架，它使用 Markdown 语法来编写文章，并且可以生成静态页面。默认情况下，Hexo 使用 Swig 作为它的模板引擎，但是用户可以根据需要更换为其他的模板引擎，包括 EJS。

如果你想在 Hexo 中使用 EJS 作为模板引擎，你需要遵循以下几个步骤：

1. **安装 EJS 引擎**：
   你需要安装 Hexo 支持 EJS 模板引擎的插件。虽然 Hexo 默认没有直接支持 EJS 的插件，但你可以使用一些社区提供的插件或者自己实现一个。例如，你可以尝试查找是否有类似 `hexo-renderer-ejs` 的插件，并安装它：

   ```bash
   npm install hexo-renderer-ejs --save
   ```

2. **配置 Hexo**：
   安装完 EJS 渲染器之后，你需要在 Hexo 的配置文件 `_config.yml` 中添加 EJS 引擎的支持。你可能需要修改或添加渲染引擎的相关配置项。

   ```yaml
   # _config.yml 示例
   default_layout: post
   ...
   markdown:
     render:
       highlight:
         enable: true
         line_numbers: true
         css_class: 'highlight'
      .renderer:
         # 添加 EJS 渲染引擎配置
         - ejs
   ```

   这里假设你已经有了一个 `_config.yml` 文件，并且你知道如何编辑它来适应新的渲染引擎。

3. **编写 EJS 模板**：
   一旦配置好 EJS 引擎，你就可以开始在你的主题目录下的布局文件中使用 EJS 语法了。例如，你可以创建一个 `.ejs` 后缀的文件，并在里面使用 EJS 语法来生成 HTML 页面。

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title><%= config.title %></title>
   </head>
   <body>
       <h1>Welcome to my blog!</h1>
       <% posts.forEach(post => { %>
           <h2><a href="<%= post.url %>"><%= post.title %></a></h2>
           <div><%= post.content %></div>
       <% }) %>
   </body>
   </html>
   ```
请注意，上述步骤是一个大致的指南，具体细节可能会因为 Hexo 的版本以及所使用的插件的不同而有所变化。确保你查阅最新的 Hexo 文档和相关插件的文档来获取最准确的信息。如果你发现没有现成的 EJS 插件满足你的需求，你可能需要自己编写一个，或者继续使用 Hexo 默认支持的模板引擎。

### 更换模板引擎

如果你想更换模板引擎，比如从 Swig 切换到 EJS，你需要确保已经正确安装了相应的渲染插件，并且在 Hexo 的配置文件中进行了正确的设置。

Hexo 的模板系统是非常灵活的，允许你根据个人喜好和项目需求来定制你的博客或静态网站的外观和功能。通过选择合适的模板引擎和编写适当的模板文件，你可以轻松地管理网站的内容布局。
