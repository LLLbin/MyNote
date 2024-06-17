##### re 库
- [[认识正则表达式]]
- [[class re.RegexFlag]] 标志flags常量
- [[class re.Pattern]] 正则表达式对象
- [[class re.Match]] 匹配对象
```python
re.compile(pattern, flags=0)
	# 创建正则表达式对象

# 查找
re.search(pattern, string, flags=0)
	# 只返回一个匹配对象
re.match(pattern, string, flags=0)
	# 只返回一个匹配对象，只在字符串的开头位置检测匹配
	# 等于 search 设置 '^pattern'
re.findall(pattern, string, flags=0)
	# 返回所有非重叠匹配，返回列表
re.finditer(pattern, string, flags=0)
	# 返回所有迭代器

# 替换
re.sub(pattern, repl, string, count=0, flags=0)
	# 返回通过使用 repl 替换在 string 最左边非重叠出现的 pattern 而获得的字符串
	# repl 可以是一个函数，对每个非重复的 pattern 的情况调用，只接受匹配对象，并返回替换字符串
	# count 是要替换的最大次数
re.subn(pattern, repl, string, count=0, flags=0)
	# 行为与 sub() 相同，返回一个元组 (字符串, 替换次数)

# 分割
re.split(pattern, string, maxsplit=0, flags=0)
	# 用 pattern 分开 string 
	# pattern 有括号，那么所有的组里的文字也会包含在列表里
	# maxsplit 非零， 最多进行 maxsplit 次分隔， 剩下的字符全部返回到列表的最后一个元素
```
##### 实例
```python
re.search('^\w+ ',"Hello 世界\nHi 你好")  # 第一个匹配的单词
	# <re.Match object; span=(0, 6), match='Hello '>

re.search(' \w+',"Hello 世界\nHi 你好")  # 匹配空格接一个单词
	# <re.Match object; span=(5, 8), match=' 世界'>
re.match(' \w+',"Hello 世界\nHi 你好")  # 从头匹配到 '^ \w+'
	# None

re.findall(' \w+',"Hello 世界\nHi 你好")
	# [' 世界', ' 你好']

re.sub(' \w+', ' 您好', "Hello 世界\nHi 你好")
	# 'Hello 您好\nHi 您好'
re.sub(' \w+', ' 您好', "Hello 世界\nHi 你好")
	# ('Hello 您好\nHi 您好', 2)

re.split(' \w+', "Hello 世界\nHi 你好")
	# ['Hello', '\nHi', '']
re.split('\w+ ', "Hello 世界\nHi 你好")
	# ['', '世界\n', '你好']
```
##### 分组匹配
```python
re.findall('(\w+) (\w+)', "Hello 世界\nHi 你好")  # 匹配内容按括号的内容分组
	# [('Hello', '世界'), ('Hi', '你好')]

re.findall('(?:\w+) (?:\w+)', "Hello 世界\nHi 你好")  # 不分组
	# ['Hello 世界', 'Hi 你好']

re.findall('\w+ \w+', "Hello 世界\nHi 你好")  # 同不分组效果
	# ['Hello 世界', 'Hi 你好']
```
