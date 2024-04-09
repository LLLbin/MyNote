##### Queue 类初始化
```python
class multiprocessing.Queue([maxsize])
	# 线程和进程安全队列
```
##### Queue 类方法
```python
Queue.put()
Queue.get()
Queue.empty()
Queue.full()
```
##### 示例
```python
import multiprocessing  
  
def producer(queue):  
    for i in range(5):  
        queue.put(i)  
        print(f'Produced: {i}')  
  
def consumer(queue):  
    while True:  
        item = queue.get()  
        if item is None:  # 如果项目为None退出
            break  
        print(f'Consumed: {item}')  
  
if __name__ == '__main__':  
    queue = multiprocessing.Queue()  
  
    producer_process = multiprocessing.Process(target=producer, args=(queue,))  
    consumer_process = multiprocessing.Process(target=consumer, args=(queue,))  
  
    producer_process.start()  
    consumer_process.start()  
  
    producer_process.join()  
    queue.put(None)  # 生产结束后放入None
    consumer_process.join()
```