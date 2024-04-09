##### Process 初始化
```python
class multiprocessing.Process(target=None, name=None, args=(), kwargs={}, *)
	# target 是用于 run() 方法调用的可调用对象。默认是 None，表示不需要调用任何方法
	# name 是进程名称
	# args 是用于调用目标函数的参数元组
	# kwargs 是用于调用目标函数的关键字参数字典
```
##### Process 方法
```python
Process.run()
	# 表示进程活动的方法
Process.start()
	# 启动进程活动
Process.join()
	# 进程结束后才继续运行
```
##### 示例
```python
import multiprocessing  
  
  
def task(name: str, count: int):  # 累加任务  
    print(f'{name} - start\n', end='')  
    result = 0  
    for n in range(count):  
        result += n + 1  
        print(result)  
  
    print(f'{name} - end with {result}')  
  
  
def p1():  # 单子进程  
    p = multiprocessing.Process(target=task, args=['A', 1000])  
    p.start()  
    p.join()  
    print('main process over')  
  
  
def p2():  # 多子进程  
    args_list = [('A', 1000), ('B', 1000), ('C', 1000)]  
    p = [multiprocessing.Process(target=task, args=[name, count]) for name, count in args_list]  
  
    for i in p:  
        i.start()  
    for i in p:  
        i.join()  
  
  
if __name__ == '__main__':  
    p2()
```