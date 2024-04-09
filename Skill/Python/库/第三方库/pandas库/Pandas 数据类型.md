##### Pandas 数据类型说明
- 对于大多数数据类型，Pandas 使用 NumPy 数组作为包含在 Index、 Series 或 DataFrame 中的具体对象。并且使用 NumPy 的数据类型
- 对于某些数据类型，Pandas 扩展了 NumPy 的类型系统, 包括扩展标量和扩展数组。
##### Pandas 数据类型对象
- [[pd.Timestamp 类]]  支持时区的日期时间
- [[pd.Timedelta 类]]  时间差
- [[pd.Period 类]]  一段时间
- [[pd.Interval 类]]  区间
- [[pd.Categorical 类]] 分类数据对象
##### dtype 参数指定字符串
```python
'datetime64[ns, <tz>]'

'category'

'period[<freq>]'

'interval', 'Interval', 'Interval[<numpy_dtype>]', 'Interval[datetime64[ns, <tz>]]', 'Interval[timedelta64[<freq>]]'

'Int8', 'Int16', 'Int32', 'Int64', 'UInt8', 'UInt16', 'UInt32', 'UInt64'

'Float32', 'Float64'

'string'

'boolean'
```