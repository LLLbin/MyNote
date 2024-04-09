##### class io.BytesIO
- 内存中二进制流流
- 继承自[[class io.BufferedIOBase]]
```python
# 实例化方法
class io.BytesIO(initial_bytes=b'')

# 实例方法
BytesIO.getbuffer()
	# 返回一个对应于缓冲区内容的可读写视图而不必拷贝其数据。 此外，改变视图将透明地更新缓冲区内容

BytesIO.getvalue()
	# 返回包含整个缓冲区内容的 bytes。

BytesIO.read1(size=- 1, /)
	# 在 BytesIO 中，这与 read() 相同。

BytesIO.readinto1(b, /)
	# 在 BytesIO 中，这与 readinto() 相同。
```
##### 示例
```python
import io

# 创建一个内存文件对象
bytes_io = io.BytesIO()

# 写入字节数据到内存文件对象
data = b'\x48\x65\x6c\x6c\x6f, BytesIO!'
bytes_io.write(data)

# 读取内存文件对象中的内容
content = bytes_io.getvalue()
print("Content:", content)

# 关闭内存文件对象
bytes_io.close()

```
