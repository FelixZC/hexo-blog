---
title: nodemailer
author: pzc
date: 2024-12-05
cover: /assets/images/jpg/108.jpg
categories: [nodejs]
tags: [Mail]
---
## 介绍

`nodemailer` 是一个非常流行的 Node.js 模块，用于发送电子邮件。它抽象了 SMTP 协议的复杂性，使得通过各种邮件服务提供商（如 Gmail, Yahoo, Outlook 等）发送邮件变得简单。

### 安装

要使用 `nodemailer`，首先你需要在你的项目中安装它：

```bash
npm install nodemailer
```

如果你使用的是 yarn：

```bash
yarn add nodemailer
```

### 创建传输器

在你能够发送邮件之前，需要创建一个传输器对象。这个对象负责连接到邮件服务器，并且可以配置为使用不同的传输方法（例如 SMTP、直接发送等）。最常用的配置是使用 SMTP 传输：

```javascript
const nodemailer = require('nodemailer');

// 创建可重用的传输器对象，使用指定的运输方式和选项
let transporter = nodemailer.createTransport({
  host: 'smtp.example.com', // 使用的 SMTP 服务器
  port: 587,                // SMTP 服务器端口
  secure: false,            // true 表示使用 SSL，false 表示 TLS
  auth: {
    user: 'your-email@example.com',
    pass: 'your-email-password'
  }
});

```

### 发送邮件

一旦有了传输器对象，就可以用它来发送邮件：

```javascript
let mailOptions = {
  from: '"Fred Foo " <foo@bar.com>', // 发件人
  to: 'bar@baz.com, baz@bar.com',    // 收件人列表
  subject: 'Hello ✔',                // 主题行
  text: 'Hello world?',              // 纯文本内容
  html: '<b>Hello world?</b>'        // HTML 内容
};

// 发送邮件
transporter.sendMail(mailOptions, (error, info) => {
  if (error) {
    return console.log(error);
  }
  console.log("Message sent: %s", info.messageId);
  // 预览 URL 只有在你使用 Sendmail 或 SES 运输时才有意义
  console.log("Preview URL: %s", nodemailer.getTestMessageUrl(info));

  // 消息发送后关闭传输器（仅限于临时传输器）
  transporter.close();
});
```

### 注意事项

- **安全性**：不要硬编码敏感信息，如邮箱密码。最好使用环境变量或安全的配置管理工具。
- **SPF 和 DKIM**：确保你的域名已经设置了正确的 SPF 和 DKIM 记录，以提高邮件的可送达性和防止被标记为垃圾邮件。
- **速率限制**：许多邮件服务提供商对每小时或每天可以发送的邮件数量有限制，请确保了解这些限制。
- **错误处理**：始终检查并适当地处理发送邮件过程中可能发生的错误。

以上就是关于如何使用 `nodemailer` 的基本介绍。你可以根据自己的需求深入研究其官方文档，探索更多高级功能，比如使用模板引擎、附件支持、OAuth2 认证等。

## 资料

对于 Nodemailer 的官方资料，最权威的来源是其官方 GitHub 仓库和官方网站。以下是获取官方资料的直接链接：

- **Nodemailer 官方网站**: [https://nodemailer.com/](https://nodemailer.com/)
- **Nodemailer GitHub 仓库**: [https://github.com/nodemailer/nodemailer](https://github.com/nodemailer/nodemailer)

在这些页面上，你可以找到以下资源：

1. **入门指南**：包括安装、配置和发送第一封邮件的基本步骤。
2. **API 文档**：详细的 API 参考，解释了所有可用的方法、属性及其用法。
3. **常见问题解答（FAQ）**：回答了许多常见的疑问和遇到的问题。
4. **示例代码**：提供了多种场景下的使用案例，帮助你理解如何在不同情况下应用 Nodemailer。
5. **贡献指南**：如果你有兴趣为项目做贡献，可以遵循此指南来了解如何参与开发。
6. **问题追踪器**：用户可以在 GitHub 上报告错误或请求新特性，也可以查看已知的问题。

此外，NPM（Node Package Manager）页面也提供了一些基本信息和版本发布日志：
- **NPM 页面**: [https://www.npmjs.com/package/nodemailer](https://www.npmjs.com/package/nodemailer)

这些资源应该能够为你提供关于 Nodemailer 的全面信息。

## 探索

Nodemailer 提供了丰富的高级功能，使得发送电子邮件变得更加灵活和强大。以下是关于使用模板引擎、附件支持、OAuth2 认证等高级特性的详细介绍：

### 使用模板引擎

为了简化邮件内容的创建，尤其是当需要根据不同的用户或情境生成个性化的邮件时，可以结合模板引擎来使用 Nodemailer。常见的 Node.js 模板引擎有 EJS、Pug（以前叫 Jade）、Handlebars 等。

**步骤：**

1. 安装你选择的模板引擎。
   ```bash
   npm install ejs
   ```

2. 创建模板文件（例如 `email-template.ejs`），并在其中定义变量位置。

3. 在代码中渲染模板，并将结果作为邮件正文传递给 Nodemailer。
   ```javascript
   const ejs = require('ejs');
   const fs = require('fs');
   
   // 渲染模板
   const template = fs.readFileSync(path.join(__dirname, 'email-template.ejs'), 'utf8');
   const compiledTemplate = ejs.compile(template);
   const htmlOutput = compiledTemplate({ /* 传递给模板的数据 */ });
   
   // 发送邮件
   transporter.sendMail({
     from: 'sender@example.com',
     to: 'receiver@example.com',
     subject: 'Subject',
     html: htmlOutput,
   });
   ```

### 附件支持

Nodemailer 支持多种类型的附件，包括普通文件、流、URL 和二进制数据。你可以通过设置 `attachments` 属性来添加一个或多个附件。

```javascript
transporter.sendMail({
  from: 'sender@example.com',
  to: 'receiver@example.com',
  subject: 'Sending Email with Attachment',
  text: 'Hello world?',
  attachments: [
    {   // 文件路径
      filename: 'file.txt',
      path: '/path/to/file.txt'
    },
    {   // 流对象
      filename: 'archive.tar.gz',
      content: fs.createReadStream('archive.tar.gz')
    },
    {   // URL
      filename: 'image.png',
      path: 'http://www.example.com/image.png'
    }
  ]
});
```

### OAuth2 认证

使用 OAuth2 进行认证是更加安全的方式，特别是当你想要避免在代码中硬编码邮箱密码时。对于 Gmail 用户来说，Google 推荐使用 OAuth2 来授权应用访问用户的邮箱账户。

**步骤：**

1. 注册你的应用程序以获取 OAuth2 客户端 ID 和秘密。
2. 设置 OAuth2 客户端并获取访问令牌。
3. 使用访问令牌配置 Nodemailer 的传输器。

```javascript
const { OAuth2 } = require('google-auth-library');
const oauth2Client = new OAuth2(
  YOUR_CLIENT_ID,
  YOUR_CLIENT_SECRET,
  YOUR_REDIRECT_URL
);

// 假设你已经有了刷新令牌
oauth2Client.setCredentials({ refresh_token: YOUR_REFRESH_TOKEN });

async function sendMail() {
  try {
    const accessToken = await oauth2Client.getAccessToken();
    
    let transporter = nodemailer.createTransport({
      service: 'gmail',
      auth: {
        type: 'OAuth2',
        user: 'your.email@gmail.com',
        clientId: YOUR_CLIENT_ID,
        clientSecret: YOUR_CLIENT_SECRET,
        refreshToken: YOUR_REFRESH_TOKEN,
        accessToken: accessToken.token
      }
    });

    let info = await transporter.sendMail({
      from: '"Your Name" <your.email@gmail.com>',
      to: "recipient@example.com",
      subject: "Hello ✔",
      text: "Hello world?",
      html: "<b>Hello world?</b>"
    });

    console.log("Message sent: %s", info.messageId);
  } catch (error) {
    console.error("Error occurred: ", error);
  }
}

sendMail();
```

请确保替换示例代码中的占位符（如 `YOUR_CLIENT_ID`）为实际值。如果你正在开发阶段，可能需要在 Google API 控制台中配置 OAuth 同意屏幕，并设置重定向 URI。此外，还需要处理刷新令牌的存储和更新逻辑，以便在访问令牌过期后能够自动获取新的令牌。
