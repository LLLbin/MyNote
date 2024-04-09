##### Thread 初始化
- Thread 类代表在独立控制线程运行的活动。有两种方式指定活动：传递一个可调用对象给构造函数或者在子类重载 run() 方法。
```python
threading.Thread(target=None, name=None, args=(), kwargs={}, daemon=None)
	# target 是用于 run() 方法调用的可调用对象。默认是 None，表示不需要调用任何方法
	# name 是线程名称
	# args 是用于调用目标函数的参数元组
	# kwargs 是用于调用目标函数的关键字参数字典
	# daemon 守护线程，主线程结束，守护线程立刻结束
```
##### Thread 实例方法
```python
Thread.start()  # 开始线程活动
Thread.run()  # 代表线程活动的方法
Thread.join()  # 等待，直到线程终结
Thread.is_alive()  # 返回线程是否存活
``` 
##### 示例
```python
import threading
from time import sleep
# 实例化方式
def my_function(n):  # 定义线程任务，睡n秒
    print("线程运行")
    sleep(n)
    print("线程结束")

print("代码运行")
my_thread = threading.Thread(target=my_function, args=(5,))  # 创建Thread类实例，传参睡5秒
my_thread.start()  # 启动线程
my_thread.join()  # 等待线程完成，5秒后才能继续执行代码
print("代码结束")

# 子类继承方式
class MyThread(threading.Thread):
    def __init__(self, name: str, count: int):
        super().__init__()
        self.name = name  # 线程名
        self.daemon = True  # 守护线程
        self.count = count
    def run(self) -> None:  # 定义线程任务，打印range(self.count)
        for n in range(self.count):
            print(f'{self.getName()} - {n}\n', end='')
            sleep(1)

t_1 = MyThread('A', 10)  # 实例化
t_2 = MyThread('B', 10)  # 实例化
t_1.start()
t_2.start()
```