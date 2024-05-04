##### functools 库
```python
functools.wraps(wrapped[, assigned][, updated])
	# 这是一个装饰器，用于包装一个函数，并将其元数据（文档字符串、名称等）传递给包装函数。通常用于确保装饰的函数保持其原始信息。
```
##### 示例
```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("开始装饰")
        result = func(*args, **kwargs)
        print("结束装饰")
        return result
    return wrapper

@my_decorator
def my_function():
    """这是我的函数"""
    print("**** 我的函数功能 ****")

# 调用被装饰的函数
my_function()

# 打印函数名和文档字符串
print("Function name:", my_function.__name__)
print("Docstring:", my_function.__doc__)

```