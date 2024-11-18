---
title: "请求头Header"
date: 2024-11-18
author: "pzc"
cover: /assets/images/jpg/75.jpg
categories: [other]
tags: [Http]
---
## 介绍

请求头（Request Headers）是HTTP请求的一部分，它们包含了客户端发送给服务器的附加信息。这些信息有助于服务器更好地理解请求的上下文，并作出相应的响应。请求头以键值对的形式存在，每行一个，直到请求头部分结束。

以下是一些常见的请求头及其用途：

### 通用请求头
- **Cache-Control**：指定请求或响应遵循的缓存机制。
- **Connection**：控制网络连接的状态，如`keep-alive`保持连接，`close`关闭连接。
- **Date**：创建请求的时间。
- **Pragma**：向后兼容的请求指令，通常用于控制缓存。
- **Trailer**：指示在消息尾部存在的字段。
- **Transfer-Encoding**：定义传输的编码方式。
- **Upgrade**：请求服务器升级到另一种协议版本。
- **Via**：记录请求经过的代理服务器信息。
- **Warning**：关于消息实体的警告信息。

### 请求头
- **Accept**：客户端可接受的内容类型列表，如`text/html, application/xhtml+xml`。
- **Accept-Charset**：客户端可接受的字符集列表。
- **Accept-Encoding**：客户端可接受的内容编码，如`gzip, deflate`。
- **Accept-Language**：客户端偏好的语言列表。
- **Authorization**：包含访问资源所需的认证信息。
- **Cookie**：发送存储在客户端的与该域名相关的cookie。
- **Expect**：期望服务器在继续处理之前满足某些条件。
- **From**：发送请求的用户的电子邮件地址。
- **Host**：请求的主机名和端口号。
- **If-Match**：只有当实体标签匹配时才执行请求。
- **If-Modified-Since**：如果自指定日期以来资源未被修改，则返回304状态码。
- **If-None-Match**：与If-Match相反，当实体标签不匹配时才执行请求。
- **If-Range**：如果实体未被修改，则只返回部分内容。
- **If-Unmodified-Since**：只有当资源自指定日期以来未被修改时才执行请求。
- **Max-Forwards**：限制消息通过代理或网关的最大跳数。
- **Proxy-Authorization**：提供代理服务器的身份验证凭证。
- **Range**：请求资源的部分内容。
- **Referer**：请求的来源页面URL。
- **TE**：客户端支持的传输编码及其优先级。
- **User-Agent**：客户端的信息，包括浏览器类型、操作系统等。
- **Upgrade-Insecure-Requests**：请求浏览器将所有不安全的请求（如HTTP）升级为安全的请求（如HTTPS）。

这些请求头可以单独使用或组合使用，以实现更复杂的功能，比如内容协商、用户身份验证、缓存控制等。在开发Web应用时，了解并正确使用这些请求头对于优化性能和增强安全性非常重要。



## 示例

下面是一些常用的HTTP请求头及其示例，这些请求头在实际开发中非常常见：

### 1. **Host**
指定请求的目标服务器和端口号。
```http
Host: www.example.com
```

### 2. **User-Agent**
描述发送请求的客户端信息，如浏览器类型和版本。
```http
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
```

### 3. **Accept**
客户端可接受的内容类型列表。
```http
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
```

### 4. **Accept-Language**
客户端偏好的语言列表。
```http
Accept-Language: en-US,en;q=0.5
```

### 5. **Accept-Encoding**
客户端可接受的内容编码方式。
```http
Accept-Encoding: gzip, deflate, br
```

### 6. **Content-Type**
请求体中的数据格式。
```http
Content-Type: application/json
```

### 7. **Content-Length**
请求体的长度（字节数）。
```http
Content-Length: 34
```

### 8. **Authorization**
包含访问资源所需的认证信息。
```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

### 9. **Cookie**
发送存储在客户端的与该域名相关的cookie。
```http
Cookie: sessionid=abc123; user=JohnDoe
```

### 10. **Referer**
请求的来源页面URL。
```http
Referer: https://www.example.com/page1
```

### 11. **Cache-Control**
控制缓存的行为。
```http
Cache-Control: no-cache
```

### 12. **Connection**
控制网络连接的状态。
```http
Connection: keep-alive
```

### 13. **Range**
请求资源的部分内容。
```http
Range: bytes=0-1023
```

### 14. **Upgrade-Insecure-Requests**
请求浏览器将所有不安全的请求（如HTTP）升级为安全的请求（如HTTPS）。
```http
Upgrade-Insecure-Requests: 1
```

### 15. **X-Requested-With**
标识请求是否为AJAX请求。
```http
X-Requested-With: XMLHttpRequest
```

### 16. **Origin**
CORS请求中，表示请求的源。
```http
Origin: https://www.example.com
```

### 17. **If-Modified-Since**
如果自指定日期以来资源未被修改，则返回304状态码。
```http
If-Modified-Since: Wed, 21 Oct 2015 07:28:00 GMT
```

### 18. **If-None-Match**
与If-Match相反，当实体标签不匹配时才执行请求。
```http
If-None-Match: "737060cd8c284d8af7ad3082f209582d"
```

这些请求头在实际开发中非常有用，可以帮助开发者实现各种功能，如内容协商、用户身份验证、缓存控制等。



## 可选项

以下是HTTP请求头中一些最常用和重要的头字段及其可能的值。这些头字段在不同的场景下有不同的用途，可以根据需要选择合适的头字段和值。

### 通用请求头
1. **Cache-Control**
   - `no-cache`
   - `no-store`
   - `max-age=<seconds>`
   - `must-revalidate`
   - `public`
   - `private`

2. **Connection**
   - `keep-alive`
   - `close`

3. **Date**
   - `Wed, 21 Oct 2015 07:28:00 GMT`

4. **Pragma**
   - `no-cache`

5. **Trailer**
   - `<field-name>`

6. **Transfer-Encoding**
   - `chunked`
   - `compress`
   - `deflate`
   - `gzip`
   - `identity`

7. **Upgrade**
   - `HTTP/2.0`
   - `SHTTP/1.3`
   - `WTLS/1.1`
   - `TCP`

8. **Via**
   - `1.0 fred, 1.1 example.com (Apache/1.1)`

9. **Warning**
   - `110 http://example.com/ "Response is stale"`

### 请求头
1. **Accept**
   - `text/html`
   - `application/json`
   - `*/*`

2. **Accept-Charset**
   - `ISO-8859-1, utf-8, *;q=0.7`

3. **Accept-Encoding**
   - `gzip`
   - `deflate`
   - `br`
   - `*`

4. **Accept-Language**
   - `en-US`
   - `en;q=0.5`

5. **Authorization**
   - `Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==`
   - `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...`

6. **Cookie**
   - `sessionid=abc123; user=JohnDoe`

7. **Expect**
   - `100-continue`

8. **From**
   - `user@example.com`

9. **Host**
   - `www.example.com`

10. **If-Match**
    - `"737060cd8c284d8af7ad3082f209582d"`

11. **If-Modified-Since**
    - `Wed, 21 Oct 2015 07:28:00 GMT`

12. **If-None-Match**
    - `"737060cd8c284d8af7ad3082f209582d"`

13. **If-Range**
    - `"737060cd8c284d8af7ad3082f209582d"`
    - `Wed, 21 Oct 2015 07:28:00 GMT`

14. **If-Unmodified-Since**
    - `Wed, 21 Oct 2015 07:28:00 GMT`

15. **Max-Forwards**
    - `10`

16. **Proxy-Authorization**
    - `Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==`

17. **Range**
    - `bytes=0-1023`
    - `bytes=500-999`

18. **Referer**
    - `https://www.example.com/page1`

19. **TE**
    - `trailers`
    - `deflate`

20. **User-Agent**
    - `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36`

21. **Upgrade-Insecure-Requests**
    - `1`

22. **X-Requested-With**
    - `XMLHttpRequest`

23. **Origin**
    - `https://www.example.com`

24. **Content-Type**
    - `application/x-www-form-urlencoded`
    - `multipart/form-data`
    - `text/plain`
    - `application/json`

25. **Content-Length**
    - `34`

26. **Content-Encoding**
    - `gzip`
    - `deflate`
    - `br`

27. **Content-Language**
    - `en-US`

28. **Content-Disposition**
    - `attachment; filename="filename.txt"`

29. **Content-Range**
    - `bytes 21010-47021/47022`

30. **Content-MD5**
    - `Q2hlY2sgSW50ZWdyaXR5IQ==`

这些请求头在实际开发中非常有用，可以根据具体需求选择合适的头字段和值。