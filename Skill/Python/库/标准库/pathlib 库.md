##### pathlib 库
- [[绝对路径和相对路径]]
- [[pathlib.纯路径类]]
- [[pathlib.具体路径类]]
```python
# 继承关系
PurePath()  # 纯路径类，抽象基类，根据系统风格实例化路径，返回 PurePosixPath 或 PureWindowsPath
PurePosixPath(PurePath)  # 纯路径类
PureWindowsPath(PurePath)  # 纯路径类
Path(PurePath)  # 具体路径，抽象基类，根据系统风格实例化路径，返回 PosixPath 或 WindowsPath
PosixPath(Path, PurePosixPath)  # 具体路径
WindowsPath(Path, PureWindowsPath)  # 具体路径

# 纯路径，提供纯计算操作没有 I/O ，无论运行什么系统，都可以实例化这些类，因为操作不做任何系统调用
# 具体路径，从纯路径继承而来提供 I/O 操作，你只能实例化与当前系统风格相同的类
# POSIX 风格的路径（Unix 和 Linux 系统）
# Windows 风格的路径（Windows）
# 类路径参数都接受该库中的类

from pathlib import Path # 常用

```
