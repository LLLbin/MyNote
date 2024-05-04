##### class asyncio.TaskGroup
- 持有一个任务分组的 [[异步上下文管理器]]
- 可以使用 `TaskGroup.create_task()` 将任务添加到分组中
- 当该上下文管理器退出时所有任务都将被等待
```python
import asyncio

async def worker(task_group, i):
    await asyncio.sleep(i)
    await task_group.status("Task {} completed".format(i))

async def main():
    async with asyncio.TaskGroup() as tg:
        for i in range(3):
            tg.create_task(worker(tg, i))

    print("All tasks completed")

asyncio.run(main())

```

