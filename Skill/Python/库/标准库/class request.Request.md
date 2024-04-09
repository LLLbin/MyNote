##### request.Request 类
```python
request.Request(url, data=None, headers={}, origin_req_host=None, unverifiable=False, method=None):
	# 创建一个 URL 请求对象，可以设置请求头部等参数。

```
##### 案例
```python
import urllib.request
# 定义请求的 URL
url = 'https://www.example.com'
# 定义请求头
headers = {
    'User-Agent': 'Mozilla/5.0',
    'Referer': 'https://www.example.com'
}
# 定义请求数据（POST 请求时使用）
data = b'key1=value1&key2=value2'
# 构造请求对象
request = urllib.request.Request(url, headers=headers, data=data, method='POST')
# 添加请求头
request.add_header('Authorization', 'Bearer <your_token>')
# 发送请求并获取响应
response = urllib.request.urlopen(request)
# 读取响应内容
content = response.read()
# 打印响应内容
print(content.decode('utf-8'))
```