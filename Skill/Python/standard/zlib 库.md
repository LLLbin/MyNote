##### zlib 库
- 解压缩高级接口，compress和decompress
- 解压缩对象，compressobj和decompressobj
```python
# 解压缩高级接口
zlib.compress(data, /, level=- 1, wbits=MAX_WBITS)
	# 用于将输入的数据进行压缩，返回压缩数据
	# data: 要进行压缩的数据，通常是字节类型（bytes）或字符串类型（str）
	# level: 压缩级别，可选参数，默认值为 -1。压缩级别的取值范围为 0 到 9，其中 0 表示无压缩，9 表示最高压缩率。负值表示默认压缩级别，通常为 9。
	# wbits: 可选参数，用于控制压缩算法和窗口大小的参数。默认值为 zlib.MAX_WBITS，15

zlib.decompress(data, /, wbits=MAX_WBITS, bufsize=DEF_BUF_SIZE)
	# 解压，返回解压数据

# 解压缩对象
zlib.compressobj(level=-1, method=DEFLATED, wbits=MAX_WBITS, memLevel=DEF_MEM_LEVEL, strategy=Z_DEFAULT_STRATEGY[, zdict])
	# 压缩数据流，返回一个压缩对象
	# level: 压缩级别，可选参数，默认值为 -1。
	# method: 压缩方法，可选参数，默认为 zlib.DEFLATED，表示使用 DEFLATE 压缩算法。
	# wbits: 控制压缩算法和窗口大小的参数，可选参数，默认为 zlib.MAX_WBITS。
	# memLevel: 内存使用级别，可选参数，默认为 8。
	# strategy: 压缩策略，可选参数，默认为 zlib.Z_DEFAULT_STRATEGY。

zlib.decompressobj(wbits=MAX_WBITS[, zdict])
	# 解压数据流，返回一个解压对象

# 压缩对象方法
Compress.compress(data)
	# 压缩 data 并返回 bytes 对象，这个对象含有 data 的部分或全部内容的已压缩数据。所得的对象必须拼接在上一次调用 compress() 方法所得数据的后面。缓冲区中可能留存部分输入以供下一次调用。
Compress.flush([mode])
	# 压缩所有缓冲区的数据并返回已压缩的数据。

# 解压对象方法
Decompress.decompress(data, max_length=0)
	# 解压缩 data 并返回 bytes 对象，其中包含对应于 string 中至少一部分数据的解压缩数据。 此数据应当被拼接到之前任何对 decompress() 方法的调用所产生的输出。 部分输入数据可能会被保留在内部缓冲区以供后续处理。
Decompress.flush([length])
	# 所有挂起的输入会被处理，并且返回包含剩余未压缩输出的 bytes 对象。
```

##### 实例
```python
import zlib

# 压缩数据
data = b'This is some data to be compressed.'
compressor = zlib.compressobj()
compressed_data = compressor.compress(data) + compressor.flush()

# 解压数据
decompressor = zlib.decompressobj()
decompressed_data = decompressor.decompress(compressed_data) + decompressor.flush()

print("原始数据:", data)
print("压缩数据:", compressed_data)
print("解压数据:", decompressed_data)


# 通过尝试解压缩数据并捕获异常来判断数据是否能够成功解压缩
import zlib

def can_decompress(data):
    try:
        zlib.decompress(data)
        return True
    except zlib.error:
        return False

compressed_data = b'\x78\x9c\x01\x23\x45\x67\x89\xab\xcd\xef\x01\x23\x45\x67\x89\xab\xcd\xef\x01\x23\x45\x67\x89\xab\xcd\xef\x00\x00\x00\x00\xff\xff'
if can_decompress(compressed_data):
    print("The data can be decompressed with zlib.")
else:
    print("The data cannot be decompressed with zlib.")

```