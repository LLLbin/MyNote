##### http
- HTTP（Hypertext Transfer Protocol）是一种用于传输超文本（Hypertext）的应用层协议，常用于在客户端和服务器之间传递Web页面和资源。HTTP协议定义了客户端和服务器之间的通信规则，使得浏览器可以请求并接收Web页面，服务器可以响应并发送Web页面。
HTTP协议的主要特点包括：
1. **无状态性（Stateless）：** 每次请求和响应之间都是相互独立的，服务器不会保留客户端的状态信息。这意味着服务器无法识别出多个请求是否来自同一客户端。
2. **请求-响应模式：** 客户端发送HTTP请求到服务器，服务器处理请求并返回HTTP响应给客户端。请求和响应由消息头（Headers）和消息体（Body）组成。
3. **URL（Uniform Resource Locator）：** 每个资源在Web上都有一个唯一的URL，通过URL来标识资源的位置。
4. **HTTP方法（HTTP Methods）：** 定义了对资源的操作，常见的HTTP方法包括GET（获取资源）、POST（提交数据）、PUT（更新资源）和DELETE（删除资源）等。
5. **状态码（Status Codes）：** 用于表示服务器对请求的处理结果，常见的状态码有200 OK（请求成功）、404 Not Found（资源未找到）和500 Internal Server Error（服务器内部错误）等。
6. **头部字段（Headers）：** 用于传递附加的信息，如User-Agent（浏览器类型）、Content-Type（数据类型）和Cookie等。
7. **内容类型（Content Types）：** 指示消息体的数据类型，例如text/html（HTML文档）、application/json（JSON数据）等。
8. **会话管理：** 为了解决无状态性的问题，HTTP引入了Cookie和Session机制，用于在多次请求之间保持状态信息。
##### http 消息
- HTTP消息由请求消息和响应消息两部分构成。每个部分都有其特定的结构和内容，用于在客户端和服务器之间传递信息。
1. 请求消息（Request Message）的构成：
    - 请求行：包含HTTP方法、URL和协议版本。
    - 请求头部（Headers）：包含关于请求的附加信息，如User-Agent、Accept、Content-Type等。
    - 空行：用于分隔请求头和请求体。
    - 请求体（Body）：可选，包含实际的请求数据，例如POST请求中的表单数据或上传的文件内容。
2. 响应消息（Response Message）的构成：
    - 状态行：包含协议版本、状态码和状态消息。
    - 响应头部（Headers）：包含关于响应的附加信息，如Server、Content-Type、Content-Length等。
    - 空行：用于分隔响应头和响应体。
    - 响应体（Body）：实际的响应数据，如HTML页面、JSON数据等。
```python
# 请求消息
GET /index.html HTTP/1.1  # 请求行
Host: www.example.com  # 请求头部
User-Agent: Mozilla/5.0  
Accept: text/html  

# 响应消息
HTTP/1.1 200 OK  # 状态行
Date: Mon, 01 Aug 2022 12:00:00 GMT  # 响应头部
Server: Apache/2.4.18 (Ubuntu)  
Last-Modified: Tue, 15 Jun 2021 08:30:00 GMT  
Content-Length: 1234  
Content-Type: text/html  

<!DOCTYPE html>  # 响应体
<html>
<head>
    <title>Welcome to Example</title>
</head>
<body>
    <h1>Hello, World!</h1>
</body>
</html>

```
