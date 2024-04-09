##### Handler
- Handler 是用于处理特定功能的类，它们负责在 HTTP 请求过程中执行特定的操作或处理特定的情况。Handler 可以被添加到 Opener 中，以构建自定义的请求处理逻辑。不同类型的请求可以使用不同的 Handler 来处理，例如处理代理、处理 Cookie、处理重定向等。
```python
urllib.request.HTTPHandler
	# 用于打开 HTTP URL 的 handler 类
urllib.request.HTTPSHandler(debuglevel=0, context=None, check_hostname=None)
	# 用于打开 HTTPS URL 的 handler 类
urllib.request.ProxyHandler(proxies=None)
	# 创建一个用于处理代理的处理器。
urllib.request.HTTPCookieProcessor(cookiejar=None)
	# 创建一个用于处理 Cookie 的处理器。
urllib.request.HTTPRedirectHandler
	# 一个用于处理重定向的类。
urllib.request.HTTPErrorProcessor
	# 处理出错的 HTTP 响应。
```
##### 案例
```python
import urllib.request

# 创建一个 Opener，包含多个 Handler
opener = urllib.request.build_opener(
    urllib.request.HTTPHandler(),
    urllib.request.HTTPSHandler(),
    urllib.request.ProxyHandler({'http': 'http://proxy.example.com:8080'}),
)

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