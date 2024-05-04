##### url
- URL（Uniform Resource Locator）统一资源定位符，是一种用于标识和定位网络上资源的字符串格式。它由多个部分组成，每个部分都提供了有关资源在网络上位置和性质的信息。
1. **协议（Protocol）**：
	- URL 的协议部分指示了要使用的网络协议，如 HTTP、HTTPS、FTP、SMTP 等。
	- 协议告诉客户端和服务器之间如何通信以获取资源。
	- 示例：`http://`, `https://`, `ftp://`
2. **域名（Domain Name）或 IP 地址**：
	- 域名是人类可读的网站名称，用于标识服务器的地址。
	- IP 地址是服务器的数值标识，用于在网络上唯一标识主机。
	- 示例：`www.example.com`, `192.168.1.1`
3. **端口号（Port Number）**：
	- 端口号指定服务器上正在监听的端口，用于识别服务的具体应用。
	- 默认的端口号根据协议而不同，如 HTTP 使用 80，HTTPS 使用 443。
	- 示例：`:80`, `:443`
4. **路径（Path）**：
	- 路径表示服务器上资源的位置，用于指定资源所在的目录或文件。
	- 路径以斜杠 `/` 开头，可以包含多个层级目录。
	- 示例：`/path/to/resource`
5. **查询参数（Query Parameters）**：
	- 查询参数用于向服务器传递额外的信息，通常以键值对的形式出现。
	- 以 `?` 开头，多个参数之间使用 `&` 分隔。
	- 示例：`?key1=value1&key2=value2`
6. **片段标识符（Fragment Identifier）**：
	- 片段标识符指定资源中的特定片段，如文档中的某个章节或元素。
	- 以 `#` 开始，通常在页面内部导航时使用，不会发送给服务器。
	- 示例：`#section1`, `#element2`
```python
protocol : // hostname[:port] / path / ?key1=value1&key2=value2 #section1
	# protocol（协议）
	# hostname（主机域名或IP地址）
	# port（端口号）
	# path（路径）
	# key=value (传递参数)
	# section1 (片段标识符)

https://www.baidu.com/s?wd=python&page=1#section1
# 协议 https
# 域名 www.baidu.com
# 路径 /s
# 传递参数 ?wd=python&page=1 关键词搜索python第一页内容
# 片段部分是 #section1
```

