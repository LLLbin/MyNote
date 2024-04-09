##### client.HTTPConnection 类
```python
client.HTTPConnection(host, port=None, [timeout, ]source_address=None, blocksize=8192)
	# 创建一个HTTP连接到指定的主机和端口。

# 实例方法
HTTPConnection.request(method, url, body=None, headers={}, *, encode_chunked=False)
	# 发送HTTP请求
HTTPConnection.getresponse()
	# 获得响应，返回一个 HTTPResponse 的实例
```