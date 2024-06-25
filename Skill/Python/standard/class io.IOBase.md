##### class io.IOBase
- 所有 I/O 类的抽象基类。
- 此类为许多方法提供了空的抽象实现，派生类可以有选择地重写。默认实现代表一个无法读取、写入或查找的文件。
```python
# 实例属性与方法
IOBase.close()
	# 刷新并关闭此流。如果文件已经关闭，则此方法无效。文件关闭后，对文件的任何操作（例如读取或写入）都会引发 ValueError 。

IOBase.closed
	# 如果流已关闭，则返回 True。

IOBase.fileno()
	# 返回流的底层文件描述符（整数）---如果存在。如果 IO 对象不使用文件描述符，则会引发 OSError 。

IOBase.flush()
	# 刷新流的写入缓冲区（如果适用）。这对只读和非阻塞流不起作用。

IOBase.isatty()
	# 如果流是交互式的（即连接到终端/tty设备），则返回 True 。

IOBase.readable()
	# 如果可以读取流，则返回 True 。否则为 False ，且 read() 将引发 OSError 错误。

IOBase.readline(size=- 1, /)
	# 从流中读取并返回一行。如果指定了 size，将至多读取 size 个字节。
	# 对于二进制文件行结束符总是 b'\n'；对于文本文件，可以用将 newline 参数传给 open() 的方式来选择要识别的行结束符。

IOBase.readlines(hint=- 1, /)
	# 从流中读取并返回包含多行的列表。可以指定 hint 来控制要读取的行数：如果（以字节/字符数表示的）所有行的总大小超出了 hint 则将不会读取更多的行。
	# 0 或更小的 hint 值以及 None，会被视为没有 hint。
	# 请注意使用 for line in file: ... 就足够对文件对象进行迭代了，可以不必调用 file.readlines()。

IOBase.seek(offset, whence=SEEK_SET, /)
	# 将流位置修改到给定的字节 offset。 offset 将相对于由 whence 指定的位置进行解析。 whence 的默认值为 SEEK_SET。 whence 的可用值有：
	# SEEK_SET 或 0 -- 流的开头（默认值）；offset 应为零或正值
	# SEEK_CUR or 1 -- 当前流位置；offset 可以为负值
	# SEEK_END or 2 -- 流的末尾；offset 通常为负值

IOBase.seekable()
	# 如果流支持随机访问则返回 True。 如为 False，则 seek(), tell() 和 truncate() 将引发 OSError。

IOBase.tell()
	# 返回当前流的位置。

IOBase.truncate(size=None, /)
	# 将流的大小调整为给定的 size 个字节（如果未指定 size 则调整至当前位置）。 当前的流位置不变。 这个调整操作可扩展或减小当前文件大小。 在扩展的情况下，新文件区域的内容取决于具体平台（在大多数系统上，额外的字节会填充为零）。 返回新的文件大小。

IOBase.writable()
	# 如果流支持写入则返回 True。 如为 False，则 write() 和 truncate() 将引发 OSError。

IOBase.writelines(lines, /)
	# 将行列表写入到流。 不会添加行分隔符，因此通常所提供的每一行都带有末尾行分隔符。

IOBase.__del__()
	# 为对象销毁进行准备。 IOBase 提供了此方法的默认实现，该实现会调用实例的 close() 方法。
```