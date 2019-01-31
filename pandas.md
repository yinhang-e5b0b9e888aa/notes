# pandas

```python
#pandas

df.dtypes
df.get_dtype_counts()

df.values

df.columns
df.index

#using the dot notation to access columns should be avoided with production code.

aaa.to_frame()

#某个series对应的可能的值的记录数（非常有用）
bbb.value_counts()
bbb.value_counts(normalize=True)  #返回频率，而不是个数
bbb.count()   #获取的是非nan的记录数

bbb.hasnans

bbb.describe()  #有用的统计信息

bbb.fillna(0)
bbb.dropna()

#计算nan的记录个数
bbb.isnull().sum()

df.isnull().sum()  #dataframe每一列对应的nan个数

bbb.astype(int)


#默认index是RangeIndex
# 读取时指定某个列的值为index：
pd.read_csv('data.csv', index_col='title')

#或者之后来set:
df.set_index('title)


#column或index重命名
df.rename(......)


#series sort
sort_values(ascending=False)


#查看是否所有的值都为True:
bbb.all()

#删除某个column
df.drop('''', axis='columns')
del movie['athat']

  >>> profit_index = movie.columns.get_loc('gross') + 1
   >>> profit_index
   9
   >>> movie.insert(loc=profit_index,
                    column='profit',
                    value=movie['gross'] - movie['budget'])
                    

#传入字符串返回series
#传入list是返回dataframe
df[['a','b']]  #选择a,b列


#选择所有数字行！！！！！：
df.select_dtypes(include=['number'])

#regex选择行！！
df.filter(regex='....')

#reorder column names
#检查是否有遗漏：
 set(columns) == set(new_columns)
 
 The correct way to compare two entire DataFrames with one another is not with the equals operator but with the equals method:
 
 
 
 df.loc[[....]]  通过index来选择行
 
 
 
-----------------
df.info()
df.describe(include=[np.number]).T
df.describe(include=[np.object, pd.Categorical]).T



#查看每一列的内存使用
df.memory_usage(deep=True)
#转换类型以减少内存使用
bbb = bbb.astype(np.int8)


df.select_dtypes(include=['object']).nunique()
#cardinality比较少的object，可以考虑转换为category类型：
#object可以是任意混合类型的python object，不一定是string
df[''] = df[''].astype('category')

new_mem / original_mem

#如果有nan，pandas会自动转换为float

movie2.nlargets(100, 'imdb_score').nsmallest(5, 'budget')


movie_top_year = movie3.drop_duplicates(subset='title_year') #drop_duplicate是考虑每一行是否相等，subset可以指定只考虑某些列

#iloc传入数字index，loc传入字符串label index
df.iloc[rows, columns]   #同时过滤行和列   ：代表全部

# college.columns.get_loc('UGDS_WHITE')

#如果要选一个cell，iat和at比iloc和loc性能更好

df.loc[boolean_searis, [columns]]

#boolean series的非操作： ~


#Series where操作，默认不满足条件被置为nan，可以通过other参数指定

#只检查series元素的值，而不检查类型：
from pandas.testing import assert_frame_equal
assert_frame_equal(a, b, check_dtype=False)

#Boolean indexing may be accomplished with both the .iloc and .loc indexers with the caveat that .iloc cannot be passed a Series but the underlying ndarray

c1.union(c2) # or `c1 | c2`
c1.symmetric_difference(c2) # or `c1 ^ c2`

a.copy()

flights.groupby('AIRLINE').agg({'ARR_DELAY':'mean'}).head()

#in 操作：：：
values = [...]
df[df['col1'].isin(values)]


df = df.sort_index()
df.index.is_unique


#removing the multiindex after grouping 249/534

#自定义的agg function传入的参数是一个group对应的series, 这个函数需要返回一个scalar
#可以增加自定义参数：
def cu_function(s, arg1, arg2):
    return ...
...groupby...agg(cu_function, arg1_val, arg2_val)


closure: nested function
>>> def make_agg_func(func, name, *args, **kwargs):
           def wrapper(x):
               return func(x, *args, **kwargs)
           wrapper.__name__ = name
           return wrapper
>>> my_agg1 = make_agg_func(pct_between, 'pct_1_3k', low=1000, high=3000)
>>> my_agg2 = make_agg_func(pct_between, 'pct_10_30k', 10000, 30000)
>>> college.groupby(['STABBR', 'RELAFFIL'])['UGDS'] \

.agg(['mean', my_agg1, my_agg2]).head()
              

#Coroutines can also be used to provide simpler and lower-overhead alternatives to threading


# dict转成dataframe
pd.DataFrame.from_dict(my_map, orient='index').reset_index()

# excel中写入多个表

writer = pd.ExcelWriter('file_path',engine='xlsxwriter')   
workbook=writer.book
worksheet=workbook.add_worksheet('统计表')
writer.sheets['统计表'] = worksheet
df1.to_excel(writer,sheet_name='统计表',startrow=0 , startcol=0, index=False, encoding="gb10830")
df2.to_excel(...)
writer.close()

# series转换成dict之后，再设置key value会快很多！！！
s.to_dict()
s['a'] = 'b'

```


# feather format in pandas, java, apache spark
```python
df_raw.to_feather('tmp/raw')
df_raw = pd.read_feather('tmp/raw')
```


# 通过mapping替换cell值，例如某个字符串替换为某个整形
```python
df = df.replace({"col_name":  {"cat1": 0, "cat2": 1} })
```
