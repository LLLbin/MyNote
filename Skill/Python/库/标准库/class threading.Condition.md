##### Condition 初始化
- 一个条件变量对象关联一个底层锁，允许一个或多个线程在被其它线程所通知之前进行等待
```python
threading.Condition(lock=None)
	# lock 为 Lock 或者 RLock 对象
	# 当多个条件变量需要共享同一个锁时，传入一个锁很有用
	# condition = threading.Condition()
```
##### Condition 方法
```python
with Condition:  # 上下文管理器，结束后释放
Condition.acquire(*args)  # lock参数的方法
Condition.release()  # lock参数的方法

Condition.wait(timeout=None)  # 等待，直到其他线程通知
Condition.notify(n=1)  # 唤醒n个等待这个条件的线程
Condition.notify_all()  # 唤醒所有

Condition.wait_for(predicate, timeout=None)  
	# 等待，直到条件计算为真。 predicate 应该是一个可调用对象而且它的返回值可被解释为一个布尔值。可以提供 timeout 参数给出最大等待时间。
	# 这个实用方法会重复地调用 wait() 直到满足判断式或者发生超时。返回值是判断式最后一个返回值，而且如果方法发生超时会返回 False


```
##### 生产消费模式
```python
import threading
import time

# 缓冲区
class Buffer:
    def __init__(self, capacity):
        self.capacity = capacity  # 容量
        self.buffer = []  # 列表容器
        self.lock = threading.Lock()  # 原始锁
        self.condition = threading.Condition(lock=self.lock)  # 条件对象

    def produce(self, item):  # 生产缓冲区，存放产品
        with self.condition:
            while len(self.buffer) >= self.capacity:  # 容量满了
                print("缓冲区满了. 生产等待.")
                self.condition.wait()  # 线程阻塞，停止生产
            self.buffer.append(item)
            print(f"Produced: {item}")
            self.condition.notify()  # 通知其他等待的线程继续执行

    def consume(self):  # 消费缓冲区，消费产品
        with self.condition:
            while len(self.buffer) == 0:  # 容量为空
                print("缓冲区空了. 消费等待.")
                self.condition.wait()
            item = self.buffer.pop(0)
            print(f"Consumed: {item}")
            self.condition.notify()  # 通知其他等待的线程继续执行
            return item


def producer(buffer, items,n):  # 生产者
    for item in items:
        buffer.produce(item)  # 生产
        time.sleep(n)


def consumer(buffer, count,n):  # 消费者
    for _ in range(count):
        item = buffer.consume()  # 消费
        time.sleep(n)


buffer = Buffer(capacity=5)
# pn, cn = 1, 1  # 相同速度 消费容易等待
# pn, cn = 1, 0.1  # 消费快 消费容易等待
pn, cn = 0.1, 1  # 生产快 生产容易等待

# 生产者线程，生产10个产品，间隔pn秒
producer_thread = threading.Thread(target=producer, args=(buffer, range(10), pn))
# 消费者线程，消费10个产品，间隔cn秒
consumer_thread = threading.Thread(target=consumer, args=(buffer, 10, cn))

producer_thread.start()
consumer_thread.start()

producer_thread.join()
consumer_thread.join()

print("All threads have finished")

```