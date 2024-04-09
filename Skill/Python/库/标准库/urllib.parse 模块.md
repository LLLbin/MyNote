##### urllib.parse 模块
- URL 解析
	- URL 解析函数用于将一个 URL 字符串分割成其组成部分，或者将 URL 的多个部分组合成一个 URL 字符串。
- URL 转码
	- URL 转码函数的功能是接收程序数据并通过对特殊字符进行转码并正确编码非 ASCII 文本来将其转为可以安全地用作 URL 组成部分的形式，还支持逆转此操作以便从作为 URL 组成部分的内容中重建原始数据
```python
# URL 解析
parse.urlparse(urlstring, scheme='', allow_fragments=True)
	# 将一个 URL 解析为六个部分，返回一个包含 6 项的 named tuple

parse.urlunparse(parts)
	# 根据 urlparse() 所返回的元组来构造一个 URL

parse.parse_qs(qs, keep_blank_values=False, strict_parsing=False, encoding='utf-8', errors='replace', max_num_fields=None, separator='&')
	# 解析以字符串给出的查询参数， 返回字典形式的数据。 结果字典的键为唯一的查询变量名而值为每个变量名对应的值列表。

# URL 转码
parse.quote(string, safe='/', encoding=None, errors=None)
	# 使用 %xx 转义符替换 string 中的特殊字符

parse.unquote(string, encoding='utf-8', errors='replace')
	# 将 %xx 转义符替换为其单字符等价物

parse.urlencode(query, doseq=False, safe='', encoding=None, errors=None, quote_via=quote_plus)
	# 用于将字典或包含键值对的可迭代对象转换为 URL 查询字符串格式
```