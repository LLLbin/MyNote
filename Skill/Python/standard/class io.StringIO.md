##### class io.StringIO
- 内存中文本流
- 继承自[[class io.TextIOBase]]
```python
# 实例化方法
class io.StringIO(initial_value='', newline='\n')

# 实例方法
StringIO.getvalue()
	# 返回一个包含缓冲区全部内容的 str。 换行符会以与 read() 相同的方式被编码，但是流的位置不会被改变。
```
##### 示例
```python
import io

# 创建一个内存文件对象
string_io = io.StringIO()

# 写入字符串到内存文件对象
string_io.write("Hello, StringIO!")

# 读取内存文件对象中的内容
content = string_io.getvalue()
print("Content:", content)

# 关闭内存文件对象
string_io.close()

```