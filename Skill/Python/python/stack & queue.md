```python
# 0. 创建
from collections import deque
stack = deque()
queue = deque()

# 1. 使用deque作为栈
stack.append('a')  # 压栈
stack.append('b')  # 压栈
stack.pop()        # 出栈，返回 'b'

# 2. 使用deque作为队列
queue.append('a')  # 入队
queue.append('b')  # 入队
queue.popleft()    # 出队，返回 'a'
```

![[class collections.deque]]