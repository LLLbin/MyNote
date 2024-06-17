##### DataFrame
```python
df = pd.DataFrame({
	'one': pd.Series([1,2,3], index=['a','b','c']), 
	'two': pd.Series([1,2,3,4], index=['a','b','c','d'])
})

'''
   one  two
a  1.0    1
b  2.0    2
c  3.0    3
d  NaN    4
'''

df['one']  # one 列
df[['one','two']]  # one,two 列

df['one']['c']  # one 列 c 行
df['one'][2]  # one 列 2 行

df.loc['a']  # a 行
df.loc[['a','b']]  # a b 行
df.loc['a', 'one']  # a 行 one 列

df.iloc[0]  # 第 0 行
df.iloc[[0, 1]]  # 第 0 1 行
df.iloc[0, 0]  # 第 0 行 0 列
```