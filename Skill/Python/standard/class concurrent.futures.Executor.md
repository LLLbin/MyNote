##### class concurrent.futures.Executor
- 抽象基类提供异步执行调用方法。要通过它的子类调用，而不是直接调用。
```python
submit(fn, /, *args, **kwargs)
# 调度可调用对象 fn，以 fn(*args, **kwargs) 方式执行并返回一个代表该可调用对象的执行的 Future 对象。

map(func, *iterables, timeout=None, chunksize=1)
# 类似于 map(func, *iterables) 函数，除了以下两点：
# iterables 是立即执行而不是延迟执行的；
# func 是异步执行的，对 func 的多个调用可以并发执行。


```