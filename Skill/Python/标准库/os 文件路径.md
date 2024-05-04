##### os
```python
os.chdir(path)  # 改变当前工作目录

os.stat(path) # 获取文件或目录的状态。Path.stat()
os.getcwd()  # 返回表示当前工作目录的字符串。Path.cwd()
os.listdir(path='.')  # 目录中文件和子目录。Path.iterdir()
os.remove(path)  # 删除文件。Path.unlink()
os.rmdir(path)  # 删除空目录。Path.rmdir()
os.rename(src, dst)  # 重命名文件或目录路径。Path.rename()

os.mkdir(path, mode=0o777, *, dir_fd=None)  
	# 创建一个新目录。Path.mkdir()
os.makedirs(name, mode=0o777, exist_ok=False)  
	# 递归地创建多级目录。Path.mkdir()
```
##### os.path
```python
os.path.realpath(path)  # 绝对路径 Path.resolve()
os.path.exists(path)  # 存在判断 Path.exists()
os.path.isfile(path)  # 文件判断 Path.is_file()
os.path.isdir(path)  # 目录判断 Path.is_dir()
os.path.join(path, *paths)  # 路径拼接 PurePath.joinpath()
os.path.basename(path)  # 名字 PurePath.name

os.path.split(path) # 拆分路径为目录和文件名的元组。PurePath.parts
os.path.splitext(path) # 分离路径的扩展名。PurePath.suffix 
os.path.getsize(path) # 获取文件大小。Path.stat().st_size 
os.path.abspath(path) # 返回绝对路径。PurePath.resolve()

os.path.dirname(path) # 获取路径的目录部分。PurePath.parent 
os.path.realpath(path) # 获取绝对路径。PurePath.resolve() 
os.path.abspath(path) # 获取绝对路径。PurePath.resolve() 
os.path.expanduser(path) # 将path中包含的"~"和"~user"转换成用户目录。
PurePath.expanduser()
```