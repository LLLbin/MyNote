##### http.client 模块
- [[class client.HTTPConnection]]
- [[class client.HTTPSConnection]]
- [[class client.HTTPResponse]]
- client.HTTP_PORT 常量 HTTP 协议默认的端口号 (总是 80)
- client.HTTPS_PORT 常量 HTTPS 协议默认的端口号 (总是 443)
##### 示例
```python
# 访问百度
import http.client
# 创建连接
conn = http.client.HTTPConnection("www.baidu.com")
# 发送GET请求
conn.request("GET", "/")  # 根目录 根相对文件路径
# 获取响应
response = conn.getresponse()
# 打印状态码和响应头部
print("Status:", response.status)
print("Headers:", response.getheaders())
# 读取响应内容
content = response.read().decode('utf-8')
# 打印响应内容（前100个字符）
print("Response Content:")
print(content[:100])
# 关闭连接
conn.close()
```