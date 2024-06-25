##### 基础常量
```python
# 地址（和协议）簇
socket.AF_UNIX  # 用于创建 Unix 域套接字，用于在同一台计算机上的进程之间进行通信的机制
socket.AF_INET  # 表示使用 IPv4 地址族  address = (host, port)
socket.AF_INET6  # 表示使用 IPv6 地址族   address = (address, port, flowinfo, scope_id)

# 套接字类型
socket.SOCK_STREAM  # 表示使用 TCP 协议，提供面向连接的、可靠的数据流。
socket.SOCK_DGRAM  # 表示使用 UDP 协议，提供无连接的数据报文传输。
socket.SOCK_RAW  # 表示使用原始套接字，可用于访问网络层以下的数据。
socket.SOCK_RDM  # 表示使用可靠数据报协议，是面向无连接的
socket.SOCK_SEQPACKET  # 表示使用顺序数据包协议，提供面向连接的可靠的数据传输。
```