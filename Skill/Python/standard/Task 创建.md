##### `asyncio.create_task(coro, *, name=None, context=None)`
**功能用途：**
- `asyncio.create_task()`函数用于创建一个任务（`asyncio.Task`对象），将一个协程（coroutine）或可等待对象转换为一个可以在事件循环中调度执行的任务。这允许你在并发环境中同时执行多个任务，从而提高程序的性能和响应性。

**参数说明：**
- `coro`：要转换为任务的协程（或可等待对象）。
- `name`：可选参数，指定任务的名称。这个名称可以在调试和日志记录时使用，以便标识任务。
- `context`：可选参数，设置任务的上下文。上下文可以是一个字典，其中包含与任务关联的上下文信息。

**返回值：**
- 该函数返回一个`asyncio.Task`对象，该对象表示一个即将或正在执行的任务。你可以通过这个对象来管理任务的状态、等待任务完成以及取消任务。

**示例：**
- 以下是一个示例，展示了如何使用`asyncio.create_task()`函数创建并发执行的任务：
```python
import asyncio  

async def f1(name: str, delay: float):  # 协程 f1
    print(f'{name} - step 1')  
    await asyncio.sleep(delay)  
    print(f'{name} - step 2')  
    
async def main():  
    print('start A coroutine')  
    task_1 = asyncio.create_task(f1('A', 3))  # 创建任务  A
    print('start B coroutine')  
    task_2 = asyncio.create_task(f1('B', 3))  # 创建任务  B
    await task_1  # 等任务完成  
    print('finished A coroutine')  
    await task_2  # 等任务完成  
    print('finished B coroutine')  
if __name__ == "__main__":  
    asyncio.run(main())
```

- 在这个示例中，我们定义了两个协程`task1()`和`task2()`，它们都通过`asyncio.create_task()`创建了任务，并添加到事件循环中。通过使用`await`关键字等待这些任务的完成，我们实现了并发执行这两个任务。

**注意事项：**
- 使用`asyncio.create_task()`可以方便地创建任务，但需要确保在协程内部使用`await`来等待任务的完成，否则任务可能会并发执行而不会等待。
- 在Python 3.7之前的版本中，可以使用`loop.create_task()`来创建任务。`asyncio.create_task()`是在Python 3.7中引入的，用于替代`loop.create_task()`。