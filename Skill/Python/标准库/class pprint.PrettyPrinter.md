##### class pprint.PrettyPrinter
```python
# 实例化方法
pprint.PrettyPrinter(indent=1, width=80, depth=None, 
					 stream=None, *, compact=False, 
					 sort_dicts=True, underscore_numbers=False)
	# indent（int）：控制每一级嵌套的缩进量，默认为1。
	# width（int）：每行的最大字符数，默认为80。
	# depth（int）：递归的最大深度，默认为None（表示不限制深度）。
	# stream（file-like object）：输出流，用于指定输出的目标，默认为None（表示使用标准输出）。
	# compact（bool）：设置为True时，将尽量减少输出中的空格，默认为False。
	# sort_dicts（bool）：设置为True时，字典中的键将按字母顺序排序，默认为True。
	# underscore_numbers（bool）：设置为True时，数字中的下划线将被保留并用于增强可读性，默认为False。


# 实例方法
PrettyPrinter.pprint(object)
	# 在所配置的流上打印 object 的格式化表示，并附加一个换行符。

```
##### 案例
```python
import pprint

data = {
    'name': 'Bob',
    'age': 28,
    'city': 'Los Angeles',
    'skills': ['Python', 'C++', 'Java', 'SQL'],
    'projects': {
        'project1': 'Web Development',
        'project2': 'Machine Learning'
    }
}

custom_printer = pprint.PrettyPrinter(indent=2, width=40, depth=2, compact=True, sort_dicts=False)
custom_printer.pprint(data)

```