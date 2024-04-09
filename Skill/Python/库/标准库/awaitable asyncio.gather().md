**功能用途：**
- `asyncio.gather()` 函数用于同时运行多个可等待对象（awaitable objects），并等待它们全部完成。它返回一个包含所有可等待对象的结果的列表。这些可等待对象可以是协程、任务（`asyncio.Task` 对象）、Future 对象等。
**参数说明：**
- `*aws`：一个可变数量的可等待对象（协程、任务等）。你可以传递一个或多个可等待对象作为参数。
- `return_exceptions`：一个可选参数，如果设置为 `True`，则在等待期间抛出的异常将被收集并放在结果列表中；如果设置为 `False`（默认值），则遇到异常时整个 `asyncio.gather()` 调用将被中断。

**返回值：**
- 该函数返回一个协程（`coroutine`），在调用这个协程时，它会并发地运行传递的可等待对象，并等待它们全部完成。最终返回一个包含所有可等待对象的结果的列表。

**示例：**
- 以下是一个示例，展示了如何使用 `asyncio.gather()` 函数来同时运行多个协程，并等待它们完成：

```python
import asyncio

async def task1():
    await asyncio.sleep(1)
    return "Task 1 result"

async def task2():
    await asyncio.sleep(2)
    return "Task 2 result"

async def main():
    results = await asyncio.gather(task1(), task2())
    print("Results:", results)

asyncio.run(main())
```

- 在这个示例中，我们定义了两个协程函数 `task1()` 和 `task2()`，它们分别休眠一段时间后返回结果。在 `main()` 协程中，我们使用 `asyncio.gather()` 同时运行这两个协程，并等待它们完成。最终，我们打印出结果列表。

**注意事项：**
- `asyncio.gather()` 在同时运行多个可等待对象时非常有用，特别是当你需要等待多个异步操作完成后才继续进行其他处理时。
- 如果设置了 `return_exceptions=True`，则函数不会在遇到异常时中断，而是将异常收集到结果列表中。这可以帮助你在一次调用中收集多个可等待对象的结果和异常。