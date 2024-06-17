##### datetime 库
- [[class datetime.time]]  时间
- [[class datetime.date]] 日期
- [[class datetime.datetime]]  日期时间
- [[class datetime.timedelta]]  时间间隔
- [[class datetime.tzinfo]]  时区抽象基类
- [[class datetime.timezone]] 与UTC固定时差的时区
```python
# 继承关系
time
date
datetime(date)
timedelta
tzinfo
timezone(tzinfo)
    
# 感知型和简单型
# 感知型和简单型的区别在于是否包含时区信息
date 类型的对象都是简单型的
time 或 datetime 类型的对象可以是感知型或者简单型
感知型和简单型之间的区别不适用于 timedelta 对象
```
##### 示例
- [[strftime() 和 strptime() 的格式化]]
- [[fromisoformat() 和 isoformat() 的格式化]]