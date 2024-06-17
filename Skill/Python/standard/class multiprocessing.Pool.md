##### Pool 类初始化
```python
class multiprocessing.pool.Pool(processes=12)
```
##### Pool 类方法
```python
Pool.apply(func, args, kwds)  
# 执行函数func
# 阻塞主进程，直到函数执行完成并返回结果

Pool.apply_async(func, args, kwds, callback, error_callback)  
# 执行函数func
# 非阻塞的，会立即返回一个 AsyncResult
# 当执行成功时， callback 会被用于处理执行后的返回结果，否则，调用 error_callback 

Pool.map(func, iterable, chunksize)  
# 内置 map() 函数的并行版本，将一个函数应用到一个可迭代对象的每个元素上
# 这个方法会将可迭代对象分割为许多块，然后提交给进程池
# 可以将 chunksize 设置为一个正整数从而（近似）指定每个块的大小可以
# 阻塞主进程，直到函数执行完成并返回结果

Pool.map_async(func, iterable, chunksize=None, callback=None):
# Pool.map() 变种，非阻塞的，会立即返回一个 AsyncResult
# 当执行成功时， callback 会被用于处理执行后的返回结果，否则，调用 error_callback 
```
##### 示例
```python
import multiprocessing


# 计算平方的函数
def square(x):
    return x * x


if __name__ == "__main__":
    # 创建一个包含4个进程的进程池
    with multiprocessing.Pool(processes=4) as pool:
        # 要处理的数字列表
        numbers = [i for i in range(100)]

        # 使用map_async方法并行计算每个数字的平方
        result = pool.map_async(square, numbers)

        # 等待计算完成
        result.wait()

        # 获取结果列表
        squared_numbers = result.get()

        # 计算平方和
        total = sum(squared_numbers)

        print("平方和:", total)

```