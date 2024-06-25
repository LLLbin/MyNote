##### pandas 索引示例
```python
import pandas as pd

# 创建一个示例的 DataFrame
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 22],
    'Country': ['USA', 'Canada', 'UK']
}
df = pd.DataFrame(data)

# 使用默认整数索引
# RangeIndex(start=0, stop=3, step=1)
print("Default Index:")
print(df)

# 使用自定义标签索引
# Index(['a', 'b', 'c'], dtype='object')
df.index = ['a', 'b', 'c']
print("\nCustom Label Index:")
print(df)

# 使用列作为索引  
# Index(['Alice', 'Bob', 'Charlie'], dtype='object', name='Name')
df.set_index('Name', inplace=True)
print("\nColumn 'Name' as Index:")
print(df)

# 重置索引为默认整数索引
# RangeIndex(start=0, stop=3, step=1)
df.reset_index(inplace=True)
print("\nReset Index:")
print(df)

# 使用 MultiIndex 创建多级索引
# MultiIndex([('USA', 25), ('Canada', 30), ('UK', 22)], names=['Country', 'Age'])
df.set_index(['Country', 'Age'], inplace=True)
print("\nMultiIndex:")
print(df)

# 使用 date_range 创建时间索引
# DatetimeIndex(['2023-08-01', '2023-08-02', '2023-08-03'], dtype='datetime64[ns]', freq='D')
df.index = pd.date_range(start='2023-08-01', end='2023-08-3', freq='D')
```