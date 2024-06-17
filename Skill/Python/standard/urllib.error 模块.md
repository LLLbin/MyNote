##### urllib.error 模块
```python
urllib.error.URLError
	# 基本的异常类，用于处理 URL 相关的错误，如无法连接服务器、地址格式不正确等。
urllib.error.HTTPError
	# 继承自 URLError，用于处理 HTTP 错误状态码，如 404 Not Found、500 Internal Server Error 等
urllib.error.ContentTooShortError(msg, content)
	# 用于处理在读取响应内容时内容不足的情况。
```
##### 示例
```python
import urllib.request
import urllib.error

url = 'https://www.nonexistentwebsite.com'

try:
    # 尝试打开 URL
    response = urllib.request.urlopen(url)
except urllib.error.URLError as e:
    # 捕获 URLError 异常并输出错误信息
    print("Error:", e.reason)
except urllib.error.HTTPError as e:
    # 捕获 HTTPError 异常并输出错误信息
    print("HTTP Error:", e.code)
except urllib.error.ContentTooShortError as e:
    # 捕获 ContentTooShortError 异常并输出错误信息
    print("Content Too Short Error:", e)

```