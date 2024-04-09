##### client.HTTPResponse 类
```python
client.HTTPResponse(sock, debuglevel=0, method=None, url=None)¶
	# 在成功连接后返回类的实例，而不是由用户直接实例化。

# 实例方法
HTTPResponse.read([amt])
	# 读取并返回响应体，或后续 amt 个字节。
HTTPResponse.status
	# 由服务器返回的状态码。
HTTPResponse.getheader(name, default=None)
	# 返回响应头部名的值，如果没有匹配的头名，则为默认值
HTTPResponse.getheaders()
	# 返回 (header, value) 元组构成的列表。
```