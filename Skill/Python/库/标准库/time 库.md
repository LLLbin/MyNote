##### time 库
- 提供了各种与时间相关的函数
- class time.struct_time
```python
# 一般函数
time.time()  # 获取当前时间戳，浮点数
time.ctime()  # 易读时间，字符串
time.perf_counter() # 调用两次，获取差值测量时间，单位秒，浮点数
time.sleep(s)  # 让程序暂停指定秒数

# 结构化时间类相关函数
time.gmtime()  # 当前 UTC 结构化时间，time.struct_time 类
time.localtime()  # 当前 本地时区 结构化时间，time.struct_time 类
time.strptime(string, format)  # 字符串 转 结构化时间，time.struct_time 类
time.strftime(format, struct_time)  # 结构化时间 转 字符串
	# format 规则
	# 年份 %Y(2023) %y(23)
	# 月份 %m(08) %B(August) %b(Aug)
	# 日数 %d(01)
	# 星期 %A(Tuesday) %a(Tue) %w(0-6 周日-周六)
	# 小时 %H(24) %I(12)
	# 分钟 %M(59)
	# 秒 %S(59)
	# 上下午 %p(AM&PM) 
```
##### 示例
```python
# 字符串 转 结构化时间
sttime1 = time.strptime('Tue Aug 08 21:36:07 2023') # 默认解析格式为 "%a %b %d %H:%M:%S %Y"
sttime2 = time.strptime('2023/08/01 21:00:00','%Y/%m/%d %H:%M:%S') # 自定义解析格式
print("sttime1:", sttime1)
print("sttime2:", sttime2)

# 结构化时间 转 字符串
custom_format = time.strftime("%Y-%m-%d %I:%M %p", time.localtime())
print("Custom Format:", custom_format)
```