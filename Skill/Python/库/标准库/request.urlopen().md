##### request.urlopen()
```python
request.urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, context=None)
	# 打开指定的 URL 或请求对象，返回一个http.client.HTTPResponse类，可以用于读取响应内容。
	# data 为post提交数据
	# timeout 为可选参数，用于指定阻塞的超时时间
	# cafile 和 capath 为可选参数，用于为 HTTPS 请求指定一组受信 CA 证书
	# context 为 ssl.SSLContext 实例



```
##### 案例
```python
import urllib.request
# 定义请求的 URL
url = 'https://www.example.com'
# 发送请求并获取响应
response = urllib.request.urlopen(url)
# 读取响应内容
content = response.read()
# 打印响应内容
print(content.decode('utf-8'))
```