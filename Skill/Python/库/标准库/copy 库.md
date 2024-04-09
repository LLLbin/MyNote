##### copy 库
- Python 的赋值语句不复制对象，而是创建目标和对象的绑定关系，本模块提供了通用的浅层复制和深层复制操作
```python
copy.copy(x)  # 返回 x 的浅层复制。
copy.deepcopy(x)  # 返回 x 的深层复制。
```