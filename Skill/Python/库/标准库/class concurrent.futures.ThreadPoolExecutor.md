##### class concurrent.futures.ThreadPoolExecutor
```python
class concurrent.futures.ThreadPoolExecutor(max_workers=None, thread_name_prefix='', initializer=None, initargs=())
```
##### 示例
- [[线程池下载图片]]
```python
from concurrent.futures import ThreadPoolExecutor


def task(name: str):
    print(f'{name} - step 1\n', end='')
    print(f'{name} - step 2\n', end='')
    return f'{name} complete'


with ThreadPoolExecutor() as execute:
    r1 = execute.submit(task, 'A')
    r2 = execute.submit(task, 'B')

    print(r1.result())
    print(r2.result())

with ThreadPoolExecutor() as execute:
    r3 = execute.map(task, ['C', 'D'])

    for r in r3:
        print(r)

```