##### 字符串
- 字符串（String）是一种有序的不可变（immutable）数据类型，用于存储文本信息。字符串由一系列字符组成，可以包含字母、数字、符号等字符。字符串在编程中非常常见，用于处理文本数据和字符串操作。
- [[字符编码]]
- [[字符串前缀]]
##### 创建字符串
- 引号字面值，[[符号#转义符|转义符]]
- [[str()]]
```python
# 创建
my_string = 'Hello, World!' 
my_string = "Hello, World!" 
my_string = "A" * 5 # "AAAAA" 

my_string = "Hello, %s!" % "World" 
my_string = "Hello, {}!".format("World") 
my_string = f"Hello, {world}!" # world是个变量, 推荐这个写法

# 引号字面值
'字符串'
"字符串"
'''多行字符串'''
"""多行字符串"""
a = '\x41'  # A
a = '\x41\x42\x43'  # ABC

# str()
# 将整数转换为字符串
num = 42
num_str = str(num)
print(num_str)  # 输出："42"

# 将浮点数转换为字符串
float_num = 3.14
float_str = str(float_num)
print(float_str)  # 输出："3.14"

# 将布尔值转换为字符串
bool_val = True
bool_str = str(bool_val)
print(bool_str)  # 输出："True"

# 将列表转换为字符串
my_list = [1, 2, 3]
list_str = str(my_list)
print(list_str)  # 输出："[1, 2, 3]"
```
##### ![[序列方法]]
##### ![[字符串方法]]