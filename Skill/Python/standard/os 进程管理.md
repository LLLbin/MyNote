- [[Command Prompt]]
```python
os.getpid()  # 返回当前进程ID
os.system(command)  # 执行系统命令，返回0成功
os.popen(command)
```
##### 示例
```python
import os
# 执行一个简单的命令
exit_code = os.popen("chcp 65001")
exit_code = os.popen("dir")
# 检查命令的执行结果
if exit_code == 0:
    print("Command executed successfully.")
else:
    print("Command failed with exit code:", exit_code)
```
