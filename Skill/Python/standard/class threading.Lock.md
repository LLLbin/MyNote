##### Lock 初始化
- 线程锁用于协调多个线程之间的执行顺序，确保在同一时刻只有一个线程能够访问被保护的资源，从而维护数据的正确性和一致性。
```python
threading.Lock()
# lock = threading.Lock()
```
##### Lock 方法
```python
with lock:  # 上下文管理器，结束后释放
Lock.acquire()  # 获得锁，如果成功获得锁，则返回 True，否则返回 False
Lock.release()  # 释放锁
```
##### Lock 使用方式
```python
from threading import Thread, Lock  
from time import sleep  
  
task_lock = Lock()  # 实例化锁
  
def task(name: str):  # 线程任务
    global task_lock  
    for n in range(2):  # 两轮三步
        task_lock.acquire()  # 加锁，需要三步完整的被执行不能被打断
        sleep(1)  
        print(f'{name} - round {n} - step 1\n', end='')  
        sleep(1)  
        print(f'{name} - round {n} - step 2\n', end='')  
        sleep(1)  
        print(f'{name} - round {n} - step 3\n', end='')  
        print('')  
        task_lock.release()  # 释放锁

# 三个线程
t1 = Thread(target=task, args=('A',))  
t2 = Thread(target=task, args=('B',))  
t3 = Thread(target=task, args=('C',))  
t1.start()  
t2.start()  
t3.start()

# 加锁结果，每个线程每一轮完整执行
# A - round 0 - step 1
# A - round 0 - step 2
# A - round 0 - step 3
# 
# A - round 1 - step 1
# A - round 1 - step 2
# A - round 1 - step 3
# 
# C - round 0 - step 1
# C - round 0 - step 2
# C - round 0 - step 3

# 不加锁结果，每个线程每一轮互相占用
# B - round 0 - step 1
# A - round 0 - step 1
# C - round 0 - step 1
# C - round 0 - step 2
# B - round 0 - step 2
# A - round 0 - step 2
# C - round 0 - step 3
# A - round 0 - step 3

```