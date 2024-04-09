##### 列表
- 是一种有序的可变数据类型，它可以存储多个值，并且允许您对这些值进行添加、修改和删除操作。列表是 Python 中最常用的数据结构之一，它用于存储一组相关的元素
##### 创建列表
- 中括号
- [[list()]]
- 列表生成式
```python
# 中括号
ls = ['cat','dog','tiger',1024]

# 一维 
my_list = [] 
my_list = [1, 2, 3, 4, 5] 
my_list = [0] * 5 # [0, 0, 0, 0, 0] 

# 二维 
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]] 
matrix = [[0 for _ in range(3)] for _ in range(3)] # 创建3x3全0矩阵 
matrix = [[0] * 3 for _ in range(3)] # 创建3x3全0矩阵

# 取矩阵的列 
for col in zip(*grid): 
	c = list(col)

# list()
ls = list('abc')
ls = list((123, 'runoob', 'google', 'abc'))

# 列表生成式
# 表达式接for循环
In : [x * x for x in range(1, 11)]
out: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
# 表达式接for循环，接if判断
In : [x * x for x in range(1, 11) if x % 2 = 0]
Out: [4, 16, 36, 64, 100]
# 可两层循环
In : [m + n for m in 'ABC' for n in 'XYZ']
Out: ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```
##### ![[序列方法]]