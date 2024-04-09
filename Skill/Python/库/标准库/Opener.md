##### Opener
- Opener 是一个更高级的概念，它是一个自定义的请求处理器，就是打开 URL 的对象，可以由多个不同的 Handler 组成，用于处理复杂的 HTTP 请求场景。通过构建 Opener，你可以添加多个不同功能的 Handler，比如处理 Cookie、处理代理、自动处理重定向等。Opener 提供了更大的灵活性，适用于需要自定义请求处理逻辑的情况。
- [[request.urlopen()]] 函数和 OpenerDirector 有着密切的关系。实际上，urlopen() 函数是在背后创建了一个默认的 OpenerDirector 实例并使用它来打开 URL。这个默认的 Opener 包含了一些默认的处理器，比如 ProxyHandler、HTTPHandler 等，用于处理不同类型的请求。

```python
request.install_opener(opener)
	# 设置request.OpenerDirector 对象为全局默认的 Opener
	# 安装一个 OpenerDirector 实例，作为默认的全局打开函数。仅当 urlopen 用到该打开函数时才需要安装
request.build_opener([handler, ...])
	# 创建request.OpenerDirector 类
	# 返回一个 OpenerDirector 实例，以给定顺序把处理函数串联起来

# request.OpenerDirector 类实例方法
OpenerDirector.add_handler(handler)
	# 添加handler
OpenerDirector.open(url, data=None[, timeout])
	# 打开给定的 url (可以是一个请求对象或一个字符串），可以选择传入给定的 data。 参数、返回值和被引发的异常均与 urlopen() 的相同
OpenerDirector.error(proto, *args)
	# 处理给定协议的错误
```
##### 案例
```python
import urllib.request
# 创建一个自定义的 Opener
opener = urllib.request.build_opener(urllib.request.HTTPHandler())
# 设置 Opener 作为全局默认 Opener
urllib.request.install_opener(opener)
# 定义请求的 URL
url = 'https://www.example.com'
# 发送请求并获取响应
response = urllib.request.urlopen(url)
# 读取响应内容
content = response.read()
# 打印响应内容
print(content.decode('utf-8'))
```