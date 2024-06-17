##### json 库
- 编码解码函数
- 编码解码器 
```python
# 编码解码函数
# 编码 Python -> JSON
json.dump(obj, fp, *, indent=4, ensure_ascii=True, cls=None)
	# 将python数据类型obj转换并保存到json格式的文件路径fp内
	# indent 缩进的空格数
	# ensure_ascii=True 非 ASCII 字符会被转义
json.dumps(obj, *, indent=4, ensure_ascii=True, cls=None)
	# 将python数据类型转换为json格式的字符串

# 解码 JSON -> Python
json.load(fp, *, cls=None)
	# 从json格式的文件中读取数据并转换为python的类型
json.load(s, *, cls=None)
	# 将json格式的字符串转换为python的类型
	
# cls默认使用json.JSONEncoder和json.JSONDecoder编码解码器，也可指定自定义编码解码器

# 编码解码器
# 使用回调函数自定义编码解码器规则
# 使用子类继承编码解码器并实现方法
class json.JSONEncoder(*, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, sort_keys=False, indent=None, separators=None, default=None)
	# 编码器

class json.JSONDecoder(*, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, strict=True, object_pairs_hook=None)
	# 解码器
```
##### 示例
```python
import json

# 定义一个 Python 字典
data = {
    "name": "Alice",
    "age": 30,
    "is_student": False,
    "grades": [85, 90, 78]
}

# 将 Python 字典转换为 JSON 格式字符串
json_data = json.dumps(data, indent=4)  # 使用缩进增强可读性
print("JSON data:")
print(json_data)

# 将 JSON 格式字符串解析为 Python 数据
parsed_data = json.loads(json_data)
print("\nParsed data:")
print(parsed_data)

```

