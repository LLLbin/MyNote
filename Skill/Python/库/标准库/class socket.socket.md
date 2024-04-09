##### class socket.socket 实例化方法
```python
socket.socket(family=AF_INET, type=SOCK_STREAM, proto=0, fileno=None)
	# family 地址族
	# type 套接字类型
```
##### socket.socket 实例方法
```python
# 服务端
socket.bind(address)
	# 将套接字绑定到指定的地址和端口。
socket.listen(backlog)
	# 开始监听传入的连接请求，backlog 指定在等待队列中最多可以排队的连接数
socket.accept()
	# 接受一个传入的连接，返回一个新的套接字对象和连接的客户端地址。

# 客户端
socket.connect(address)
	# 连接到 address 处的远程套接字。（ address 的格式取决于地址簇 ）

# 通用
socket.recv(bufsize)
	# 从套接字接收数据。返回值是一个字节对象，表示接收到的数据。bufsize 指定一次接收的最大数据量。 为了最佳匹配硬件和网络的实际情况，bufsize 的值应为 2 的相对较小的幂，如 4096。
socket.send(bytes)
	# 发送数据给套接字。本套接字必须已连接到远程套接字
socket.close()
	# 将套接字标记为关闭。
```
