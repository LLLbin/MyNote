##### Runner 构造方法
- 对在相同上下文中 多个 异步函数调用进行简化的上下文管理器。
-  `asyncio.Runner(*, debug=None, loop_factory=None)`
```python
import asyncio

async def main():
    print("Hello")
    await asyncio.sleep(1)
    print("World")

async def run_coroutines():
    async with asyncio.Runner() as runner:
        await runner.run(main())

asyncio.run(run_coroutines())

```
##### Runner 实例方法
```python
Runner.run(coro, *, context=None)
# 在嵌入的循环中运行一个 协程 coro。

Runner.close()
# 关闭运行器。

Runner.get_loop()
# 返回关联到运行器实例的事件循环。
```

