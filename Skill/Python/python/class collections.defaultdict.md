```python
# 构造方法
defaultdict(default_factory)
    # default_factory: 一个返回默认值的可调用对象。当访问不存在的键时，将调用此对象并为键设置值。
	# defaultdict 是 dict 的子类。它的主要特点是在访问不存在的键时，可以自动初始化为默认值。
	# 默认值是通过传递给构造器的第一个参数（一个无参的可调用对象）来指定的。
	# 如果不指定默认值，则默认值为 None。

# 实例方法
defaultdict.get(key, default=None) # 返回键对应的值。如果键不存在，则返回 default 指定的值，如果未指定 default，则返回 None。
defaultdict.setdefault(key, default=None) # 如果键在字典中，返回其值。如果不在，则插入键并将值设为 default，然后返回 default。
defaultdict.update([other]) # 更新字典，可以是另一个字典对象或者可迭代的键值对。
defaultdict.copy() # 返回一个浅拷贝。
```
##### 示例
```python
from collections import defaultdict

# 使用list作为default_factory，当访问的键不存在时，自动初始化为一个空list
dd = defaultdict(list)

# 添加元素到键对应的list中
dd['dogs'].append('Rufus')
dd['dogs'].append('Kathrin')
dd['cats'].append('Mr Whiskers')

print(dd)  
# defaultdict(<class 'list'>, {'dogs': ['Rufus', 'Kathrin'], 'cats': ['Mr Whiskers']})
```
