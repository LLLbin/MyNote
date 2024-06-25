```python 
collections.deque(iterable , maxlen)
	# 双端操作： deque 支持在两端（左侧和右侧）进行添加和删除元素操作，这些操作的时间复杂度为 O(1)。
	# 有限长度： 可以通过指定 maxlen 参数来创建一个有限长度的 deque，当 deque 达到指定的最大长度时，新添加的元素将从另一端弹出。
	# 高效队列： 由于 deque 的底层实现使用了双向链表，它在添加和删除元素方面比普通列表表现更好，特别是在首尾操作频繁的情况下。

# 实例方法
deque.append(x) # 在队列右边（尾部）插入x
deque.appendleft(x) # 在队列左边（头部）插入x
deque.extend(iterable) # 将可迭代对象扩展到队列右边
deque.extendleft(iterable) # 将可迭代对象扩展到队列左边
deque.insert(i, x) # 插入元素x到指定位置x。如果位置超出范围，抛出IndexError异常

deque.pop() # 在队列左边（尾部）出栈
deque.popleft() # 在队列右边（头部）出栈
deque.clear() # 清空队列，初始化队列长度为1

deque.index(x) # 返回元素x在队列中的位置，没有找到抛出异常ValueError
deque.remove(x) # 删除第一个找到的元素x，没有元素抛出ValueError异常

deque.reverse() # 逆序
deque.rotate(n) # 将队列向右移动n个元素，如果n为负数则向左移动n个元素
deque.copy() # 创建一个浅拷贝的队列
deque.count(x) # 计算队列中x元素的个数
deque.maxlen() # 返回队列长度（不是当前的长度），为空返回None。
```
##### 示例
```python
from collections import deque

# 创建一个空的 deque
d = deque()

# 在右侧添加元素
d.append(1)
d.append(2)
d.append(3)

# 在左侧添加元素
d.appendleft(0)

print(d)  # deque([0, 1, 2, 3])

# 弹出右侧元素
print(d.pop())  # 3

# 弹出左侧元素
print(d.popleft())  # 0

print(d)  # deque([1, 2])
```