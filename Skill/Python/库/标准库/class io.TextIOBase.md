##### class io.TextIOBase
- 文本流的基类。 该类提供了基于字符和行的流 I/O 接口
- 继承自 [[class io.IOBase]]
```python
# 实例属性与方法
TextIOBase.write(s, /)
	# 将字符串 s 写入到流并返回写入的字符数。

TextIOBase.read(size=- 1, /)
	# 从流中读取至多 size 个字符并以单个 str 的形式返回。 如果 size 为负值或 None，则读取至 EOF。

TextIOBase.readline(size=- 1, /)
	# 读取至换行符或 EOF 并返回单个 str。 如果流已经到达 EOF，则将返回一个空字符串。
	# 如果指定了 size ，最多将读取 size 个字符。

TextIOBase.encoding
	# 用于将流的字节串解码为字符串以及将字符串编码为字节串的编码格式名称。

TextIOBase.errors
	# 解码器或编码器的错误设置。

TextIOBase.newlines
	# 一个字符串、字符串元组或者 None，表示目前已经转写的新行。 根据具体实现和初始构造器旗标的不同，此属性或许会不可用。

TextIOBase.buffer
	# 由 TextIOBase 处理的下层二进制缓冲区（为一个 BufferedIOBase 的实例）。 它不是 TextIOBase API 的组成部分并且不存在于某些实现中。

TextIOBase.detach()
	# 从 TextIOBase 分离出下层二进制缓冲区并将其返回。

TextIOBase.seek(offset, whence=SEEK_SET, /)
	# 将流位置改为给定的偏移位置 offset。 具体行为取决于 whence 形参。 whence 的默认值为 SEEK_SET。
	# SEEK_SET 或 0: 从流的开始位置起查找（默认值）；offset 必须为 TextIOBase.tell() 所返回的数值或为零。 任何其他 offset 值都将导致未定义的行为。
	# SEEK_CUR 或 1: "查找" 到当前位置；offset 必须为零，表示无操作（所有其他值均不受支持）。
	# SEEK_END 或 2: 查找到流的末尾；offset 必须为零（所有其他值均不受支持）。
	# 以不透明数字形式返回新的绝对位置。

TextIOBase.tell()
	# 以不透明数字形式返回当前流的位置。 该数字通常并不代表下层二进制存储中对应的字节数。


```