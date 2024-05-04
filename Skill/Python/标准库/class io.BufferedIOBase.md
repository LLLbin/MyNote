##### class io.BufferedIOBase
- 支持某种缓冲的二进制流的基类。
- 继承自 [[class io.IOBase]]
```python
# 实例属性与方法
BufferedIOBase.raw
	# 由 BufferedIOBase 处理的下层原始流 (RawIOBase 的实例)。 它不是 BufferedIOBase API 的组成部分并且不存在于某些实现中。

BufferedIOBase.detach()
	# 从缓冲区分离出下层原始流并将其返回。
	# 在原始流被分离之后，缓冲区将处于不可用的状态。
	# 某些缓冲区例如 BytesIO 并无可从此方法返回的单独原始流的概念。 它们将会引发 UnsupportedOperation。

BufferedIOBase.read(size=- 1, /)
	# 读取并返回最多 size 个字节。 如果此参数被省略、为 None 或为负值，则读取并返回所有数据直到 EOF。 如果流已经到达 EOF 则返回一个空的 bytes 对象。
	# 如果此参数为正值，并且下层原始流不可交互，则可能发起多个原始读取以满足字节计数（直至先遇到 EOF）。 但对于可交互原始流，则将至多发起一个原始读取，并且简短的结果并不意味着已到达 EOF。
	# BlockingIOError 会在下层原始流不处于阻塞模式，并且当前没有可用数据时被引发。

BufferedIOBase.read1(size=- 1, /)
	# 通过至多一次对下层流的 read() (或 readinto()) 方法的调用读取并返回至多 size 个字节。 这适用于在 BufferedIOBase 对象之上实现你自己的缓冲区的情况。
	# 如果 size 为 -1 (默认值)，则返回任意数量的字节（多于零字节，除非已到达 EOF）。

BufferedIOBase.readinto(b, /)
	# 将字节数据读入预先分配的可写 bytes-like object b 并返回所读取的字节数。 例如，b 可以是一个 bytearray。
	# 类似于 read()，可能对下层原始流发起多次读取，除非后者为交互式。
	# BlockingIOError 会在下层原始流不处于阻塞模式，并且当前没有可用数据时被引发。

BufferedIOBase.readinto1(b, /)
	# 将字节数据读入预先分配的可写 bytes-like object b，其中至多使用一次对下层原始流 read() (或 readinto()) 方法的调用。 返回所读取的字节数。
	# BlockingIOError 会在下层原始流不处于阻塞模式，并且当前没有可用数据时被引发。

BufferedIOBase.write(b, /)
	# 写入给定的 bytes-like object b，并返回写入的字节数 (总是等于 b 的字节长度，因为如果写入失败则会引发 OSError)。 根据具体实现的不同，这些字节可能被实际写入下层流，或是出于运行效率和冗余等考虑而暂存于缓冲区。
	# 当处于非阻塞模式时，如果需要将数据写入原始流但它无法在不阻塞的情况下接受所有数据则将引发 BlockingIOError。
	# 调用者可能会在此方法返回后释放或改变 b，因此该实现应当仅在方法调用期间访问 b。
```
