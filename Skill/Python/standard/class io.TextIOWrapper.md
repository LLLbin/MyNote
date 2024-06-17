##### class io.TextIOWrapper
- 一个提供对 [[class io.BufferedIOBase]] 缓冲二进制流的高层级访问的缓冲文本流
- 继承自[[class io.TextIOBase]]
```python
# 实例属性和方法
TextIOWrapper.line_buffering
	# 是否启用行缓冲

TextIOWrapper.write_through
	# 写入是否要立即传给下层的二进制缓冲。

TextIOWrapper.reconfigure(*, encoding=None, errors=None, newline=None, line_buffering=None, write_through=None)
	# 使用 encoding, errors, newline, line_buffering 和 write_through 的新设置来重新配置此文本流。
```