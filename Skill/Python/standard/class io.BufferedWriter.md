##### class io.BufferedWriter
- 一个提供对可写、不可查找的 [[class io.RawIOBase]] 原始二进制流的高层级访问的缓冲二进制流。 
- 继承自 [[class io.BufferedIOBase]]
- 当写入到此对象时，数据通常会被放入到内部缓冲区中。 缓冲区将在满足某些条件的情况下被写到下层的 [[class io.RawIOBase]] 对象
```python
# 实例方法
BufferedWriter.flush()
	# 将缓冲区中保存的字节数据强制放入原始流。 如果原始流发生阻塞则应当引发 BlockingIOError。

BufferedWriter.write(b, /)
	# 写入 bytes-like object b 并返回写入的字节数。 当处于非阻塞模式时，如果缓冲区需要被写入但原始流发生阻塞则将引发 BlockingIOError。
```
