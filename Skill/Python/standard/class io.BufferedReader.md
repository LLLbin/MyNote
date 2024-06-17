##### class io.BufferedReader
- 一个提供对可读、不可查找的 [[class io.RawIOBase]] 原始二进制流的高层级访问的缓冲二进制流。 
- 继承自 [[class io.BufferedIOBase]]
```python
# 实例方法
BufferedReader.peek(size=0, /)
	# 从流返回字节数据而不前移位置。 完成此调用将至多读取一次原始流。 返回的字节数量可能少于或多于请求的数量。

BufferedReader.read(size=- 1, /)
	# 读取并返回 size 个字节，如果 size 未给定或为负值，则读取至 EOF 或是在非阻塞模式下读取调用将会阻塞。

BufferedReader.read1(size=- 1, /)
	# 在原始流上通过单次调用读取并返回至多 size 个字节。 如果至少缓冲了一个字节，则只返回缓冲的字节。 在其他情况下，将执行一次原始流读取。
```

