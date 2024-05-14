```python
# pandas、Numpy、matplotlib经常一起使用，Numpy适合处理同质性数组，pandas适合处理表格型、异质性数据
```


```python
# import pandas as pd     # 默认导入模式
# from pandas import Series,DataFrame     # 常用的两个工具
```


```python
# 5.1 Introduction to pandas Data Structures 
# pandas数据结构介绍
# 5.1.1 Series  值+index索引
# import pandas as pd
# import numpy as np
# obj=pd.Series([4,7,-5,3])
# obj
# print(obj)
# # 0    4
# # 1    7
# # 2   -5
# # 3    3
# # dtype: int64


# 得到单独的值
# obj1=obj.values
# print(obj1)    # [ 4  7 -5  3]


# 单独得到索引
# obj2=obj.index
# print(obj2)   # RangeIndex(start=0, stop=4, step=1)


# 自定义索引
# obj3=pd.Series([4,7,-5,3],index=['d','b','a','c'])
# print(obj3)
# # d    4
# # b    7
# # a   -5
# # c    3
# # dtype: int64


# 用索引查看
# obj3['b']   # 7
# 用索引更改值
# obj3['a']=9
# print(obj3[['a','c']])
# # a    9
# # c    3
# # dtype: int64


# 布尔值索引
# obj4=obj3[obj3>0]
# print(obj4)
# # d    4
# # b    7
# # c    3
# # dtype: int64


# 数值运算
# obj5=obj3*3
# print(obj5)
# # d    12
# # b    21
# # a   -15
# # c     9
# # dtype: int64


# exp:Exponential 以e为底的指数曲线
# np.exp(obj3)
# d      54.598150
# b    1096.633158
# a       0.006738
# c      20.085537
# dtype: float64 


# 长度固定且有序的字典，可以刷新
# 'b' in obj3   # True
```


```python
# 可以用字典生成 serise，默认的 index就是字典的 key
# sdata={'Ohio':35000,'Texas':71000,'Oregon':16000,'Utah':5000}
# obj=pd.Series(sdata)
# # print(obj)
# type(obj)    # pandas.core.series.Series
# # Ohio      35000
# # Texas     71000
# # Oregon    16000
# # Utah       5000
# # dtype: int64


# 字典生成series，自定义index
# states=['California','Ohio','Oregon','Texas']
# obj1=pd.Series(sdata,index=states)
# print(obj1)
# # California        NaN
# # Ohio          35000.0
# # Oregon        16000.0
# # Texas         71000.0
# # dtype: float64

# index在原来字典的key值里，就取对应值，index的 California不在key值里，就取NaN
# 自定义的index里没有Utah，这个值会被丢弃
```


```python
# 如何判断有没有数据丢失
# 是NaN 返回 True
# pd.isnull(obj1)
# # California     True
# # Ohio          False
# # Oregon        False
# # Texas         False
# # dtype: bool


# 不是NaN 返回True
# pd.notnull(obj1)
# # California    False
# # Ohio           True
# # Oregon         True
# # Texas          True
# # dtype: bool
```


```python
# sdata={'Ohio':35000,'Texas':71000,'Oregon':16000,'Utah':5000}
# obj=pd.Series(sdata)
# states=['California','Ohio','Oregon','Texas']
# obj1=pd.Series(sdata,index=states)
# 相加
# obj+obj1
# # California         NaN
# # Ohio           70000.0
# # Oregon         32000.0
# # Texas         142000.0
# # Utah               NaN
# # dtype: float64
# 相加之后所有index值都被保留，共有的三个index对应value数值相加，非共同的index变为NaN


# index和value都有name属性
# obj1.name='population'
# obj1.index.name='state'
# obj1
# # state
# # California        NaN
# # Ohio          35000.0
# # Oregon        16000.0
# # Texas         71000.0
# # Name: population, dtype: float64
```


```python
# 改变索引
# obj=pd.Series([4,7,-5,3])
# obj.index=['Bob','Steve','Jeff','Ryan']
# print(obj)
# # Bob      4
# # Steve    7
# # Jeff    -5
# # Ryan     3
# # dtype: int64
```


```python
# 5.1.2 DataFrame
# 二维矩阵
# data={'state':['Ohio','Ohio','Ohio','Nevada','Nevada','Nevada'],
#      'year':[2000,2001,2002,2001,2002,2003],
#      'pop':[1.5,1.7,3.6,2.4,2.9,3.2]}
# frame=pd.DataFrame(data)
# print(frame)
# #     state  year  pop
# # 0    Ohio  2000  1.5
# # 1    Ohio  2001  1.7
# # 2    Ohio  2002  3.6
# # 3  Nevada  2001  2.4
# # 4  Nevada  2002  2.9
# # 5  Nevada  2003  3.2


# 只看前两行
# frame.head(2) 
# # 	state	year	pop
# # 0	Ohio	2000	1.5
# # 1	Ohio	2001	1.7


# 改变列的顺序
# frame1=pd.DataFrame(data,columns=['year','state','pop'])
# print(frame1)
# #    year   state  pop
# # 0  2000    Ohio  1.5
# # 1  2001    Ohio  1.7
# # 2  2002    Ohio  3.6
# # 3  2001  Nevada  2.4
# # 4  2002  Nevada  2.9
# # 5  2003  Nevada  3.2


# 如果列不在DataFrame里，会显示缺失值
# frame2=pd.DataFrame(data,columns=['year','state','pop','debt'],index=['one','two','three','four','five','six'])
# print(frame2)
# #        year   state  pop debt
# # one    2000    Ohio  1.5  NaN
# # two    2001    Ohio  1.7  NaN
# # three  2002    Ohio  3.6  NaN
# # four   2001  Nevada  2.4  NaN
# # five   2002  Nevada  2.9  NaN
# # six    2003  Nevada  3.2  NaN


# 查看列名称
# frame2.columns   # Index(['year', 'state', 'pop', 'debt'], dtype='object')


# 查看某列
# frame2['state']
# # one        Ohio
# # two        Ohio
# # three      Ohio
# # four     Nevada
# # five     Nevada
# # six      Nevada
# # Name: state, dtype: object


# 查看行
# frame2.loc['three']
# # year     2002
# # state    Ohio
# # pop       3.6
# # debt      NaN
# # Name: three, dtype: object


# 给一列赋值，给一个数，默认所有的值都是这个
# frame2['debt']=16.5
# print(frame2)
# #        year   state  pop  debt
# # one    2000    Ohio  1.5  16.5
# # two    2001    Ohio  1.7  16.5
# # three  2002    Ohio  3.6  16.5
# # four   2001  Nevada  2.4  16.5
# # five   2002  Nevada  2.9  16.5
# # six    2003  Nevada  3.2  16.5

# 如果给一个array，按顺序赋值
# frame2['debt']=np.arange(6)
# print(frame2)
# #        year   state  pop  debt
# # one    2000    Ohio  1.5     0
# # two    2001    Ohio  1.7     1
# # three  2002    Ohio  3.6     2
# # four   2001  Nevada  2.4     3
# # five   2002  Nevada  2.9     4
# # six    2003  Nevada  3.2     5
```


```python
# 通过series给列赋值，先定义一个，然后部分index相同
# val=pd.Series([-1.2,-1.5,-1.7],index=['two','four','five'])
# val
# frame2['debt']=val
# print(frame2)
# # index 相同的部分会赋值
# #       year   state  pop  debt
# # one    2000    Ohio  1.5   NaN
# # two    2001    Ohio  1.7  -1.2
# # three  2002    Ohio  3.6   NaN
# # four   2001  Nevada  2.4  -1.5
# # five   2002  Nevada  2.9  -1.7
# # six    2003  Nevada  3.2   NaN



# 新添加一个列，eastern，state值为Ohio则为True，反之赋值为False
# frame2['eastern']=frame2.state=='Ohio'
# print(frame2)
# #        year   state  pop debt  eastern
# # one    2000    Ohio  1.5  NaN     True
# # two    2001    Ohio  1.7  NaN     True
# # three  2002    Ohio  3.6  NaN     True
# # four   2001  Nevada  2.4  NaN    False
# # five   2002  Nevada  2.9  NaN    False
# # six    2003  Nevada  3.2  NaN    False



# 删除一列，用del
# del frame2['debt']
# print(frame2)
# #        year   state  pop  eastern
# # one    2000    Ohio  1.5     True
# # two    2001    Ohio  1.7     True
# # three  2002    Ohio  3.6     True
# # four   2001  Nevada  2.4    False
# # five   2002  Nevada  2.9    False
# # six    2003  Nevada  3.2    False
```


```python
# 创建 DataFrame，用嵌套字典赋值，一级key作为列，二级key作为索引
# pop={'Nevada':{2001:2.4,2002:2.9},'Ohio':{2001:1.7,2002:3.6,2003:1.5}}
# frame=pd.DataFrame(pop)
# print(frame)
# #       Nevada  Ohio
# # 2001     2.4   1.7
# # 2002     2.9   3.6
# # 2003     NaN   1.5


# 使用numpy对DataFrame进行转置操作
# frame1=frame.T
# print(frame1)
# #         2001  2002  2003
# # Nevada   2.4   2.9   NaN
# # Ohio     1.7   3.6   1.5


# 自定义索引
# frame1=pd.DataFrame(pop,index=[2002,2003,2004])
# print(frame1)
# # 2003被创建，2000被舍弃，没有值的地方默认NaN
# #       Nevada  Ohio
# # 2002     2.9   3.6
# # 2003     NaN   1.5
# # 2004     NaN   NaN
```


```python
# 用frame的series创建frame
# pop={'Nevada':{2001:2.4,2002:2.9},'Ohio':{2001:1.7,2002:3.6,2003:1.5}}
# frame=pd.DataFrame(pop)
# frame
# #       Nevada  Ohio
# # 2001     2.4   1.7
# # 2002     2.9   3.6
# # 2003     NaN   1.5


# pdata={'Ohio':frame['Ohio'][:-1],'Nevada':frame['Nevada'][:2]}
# frame1=pd.DataFrame(pdata)
# print(frame1)
# #       Ohio  Nevada
# # 2001   1.7     2.4
# # 2002   3.6     2.9



# index和colusmn有name属性
# frame1.index.name='year'
# frame1.columns.name='state'
# print(frame1)
# # state  Ohio  Nevada
# # year               
# # 2001    1.7     2.4
# # 2002    3.6     2.9



#  与series相似，values值以二维nadarray返回
# frame1.values
# # array([[1.7, 2.4],
# #        [3.6, 2.9]])
```


```python
# DataFrame 可接受的参数类型包括：
# 2D ndarray 二维数据矩阵
# Numpy 结构化数组
# Series构成的字典
# 字典：字典、数组、列表、元组构成的都行
# 列表：字典、Series、列表、元组构成的
# 其他DataFrame
# Numpy MaskedArray 
```


```python
# 5.1.3 Ixdex Objects 索引对象
# 索引是一种对象类型，和列表元组相似，数组或标签序列可以转换出索引类型，特点：不可变，可重复
# import pandas as pd
# from pandas import Series,DataFrame
# import numpy as np
# import matplotlib.pyplot as plt


# obj=pd.Series(range(3),index=['a','b','c'])
# print(obj)
# # a    0
# # b    1
# # c    2
# # dtype: int64


# index1=obj.index 
# print(index1)     # Index(['a', 'b', 'c'], dtype='object')


# 切片功能
# index1[1:]    # Index(['b', 'c'], dtype='object')


# 不可以修改
# index1[1]='d'   # 报错 TypeError: Index does not support mutable operations
```


```python
# 生成一个索引对象
# labels=pd.Index(np.arange(3))
# print(labels)     # Index([0, 1, 2], dtype='int32')


# 用上方定义的索引生成一个序列
# obj2=pd.Series([1.5,-2.5,0],index=labels)
# print(obj2)
# # 0    1.5
# # 1   -2.5
# # 2    0.0
# # dtype: float64


# 判断对象的索引是不是之前定义的索引
# obj2.index==labels   # array([ True,  True,  True])
```


```python
# 定义一个表格
# pop={'Nevada':{2001:2.4,2002:2.9},'Ohio':{2001:1.7,2002:3.6,2000:1.5}}
# frame3=pd.DataFrame(pop)
# frame3
# print(frame3)
# #       Nevada  Ohio
# # 2001     2.4   1.7
# # 2002     2.9   3.6
# # 2000     NaN   1.5



# 列名称也是Index类型对象
# frame3.columns   # Index(['Nevada', 'Ohio'], dtype='object')



# 判断'Ohio'是否在index的对象里
# 'Ohio' in frame3.columns    # True
# 2003 in frame3.index      # False



# 可以重复定义
# dup_labels=pd.Index(['foo','foo','bar','bar'])
# dup_labels     # Index(['foo', 'foo', 'bar', 'bar'], dtype='object')
```


```python
# index对象的方法和属性
# append 增加
# difference 差集
# intersection 交集
# union 并集
# is in判断
# delete 删除
# drop 删除指定索引值,并产生新的索引
# insert 插入
# is_monotonic 如果索引序列递增返回True
# is_unique 如果索引序列唯一返回True
# unique 计算索引的唯一值序列
```


```python
# 5.2 Essential Functionality 主要功能
# import pandas as pd
# from pandas import Series,DataFrame
# import numpy as np


# 5.2.1 Reindexing 重置索引
# obj=pd.Series([4.5,7.2,-5.3,3.6],index=['d','b','a','c'])
# obj
# # d    4.5
# # b    7.2
# # a   -5.3
# # c    3.6
# # dtype: float64


# obj2=obj.reindex(['a','b','c','d','e'])
# obj2
# # a   -5.3
# # b    7.2
# # c    3.6
# # d    4.5
# # e    NaN
# # dtype: float64


# 自动填充一些值,需要用method
# method=ffill,将值向前填充
# obj3=pd.Series(['blue','purple','yellow'],index=[0,2,4])
# obj3.reindex(range(6), method='ffill')
# print(obj3)


# reindex可以改变行,也可以改变列,一个参数默认改变行的索引
# frame=pd.DataFrame(np.arange(9).reshape((3,3)),index=['a','c','d'],columns=['Ohio','Texas','California'])
# frame
# # 	Ohio	Texas	California
# # a	0	1	2
# # c	3	4	5
# # d	6	7	8


# frame2=frame.reindex(['a','b','c','d'])
# frame2
# # 	Ohio	Texas	California
# # a	0.0	1.0	2.0
# # b	NaN	NaN	NaN
# # c	3.0	4.0	5.0
# # d	6.0	7.0	8.0


# 用columns改变列索引
# states=['Texas','Utah','California']
# frame.reindex(columns=states)
# # 	Texas	Utah	California
# # a	1	NaN	2
# # c	4	NaN	5
# # d	7	NaN	8
```


```python
# reindex 方法的参数
# index 索引或其他序列型数据结构
# method ffill 向前填充,bfill 向后填充
# fill_value 缺失值的默认值
# limit 限制
# tolerance 
# level 匹配MultiIndex级别的简单索引,否则选择自己
# copy=True,复制底层数据;=False,不复制数据
```


```python
# 5.2.2 Dropping Entries from an Axis 轴向上删除条目
# obj5=pd.Series(np.arange(5),index=['a','b','c','d','e'])

# 生成一个新的对象
# new_obj=obj5.drop('c')
# new_obj
# # a    0
# # b    1
# # d    3
# # e    4
# # dtype: int32


# 原来的obj5不发生改变
# print(obj5)
# # a    0
# # b    1
# # c    2
# # d    3
# # e    4
# # dtype: int32


# data5=pd.DataFrame(np.arange(16).reshape((4,4)),index=['Ohio','Colorado','Utah','New York'],columns=['one','two','three','four'])
# data5


# 删除索引所对应的行和列
# data5.drop(['Colorado','Ohio'])
# # 	one	two	three	four
# # Utah	8	9	10	11
# # New York	12	13	14	15


# 指定哪个轴
# data5.drop('two',axis=1)
# # 	one	three	four
# # Ohio	0	2	3
# # Colorado	4	6	7
# # Utah	8	10	11
# # New York	12	14	15


# axis=column也可以
# data5.drop(['two','four'],axis='columns')
# # 	one	three
# # Ohio	0	2
# # Colorado	4	6
# # Utah	8	10
# # New York	12	14


# 如果想要删除替换原来的表格,直接用inplace=True,drop的值会被清楚,原来的表格会被改变
# obj5=pd.Series(np.arange(5),index=['a','b','c','d','e'])
# obj5.drop('c',inplace=True)
# obj5
# # a    0
# # b    1
# # d    3
# # e    4
# # dtype: int32
```


```python
# 5.2.3 Indexing,Selection,and Filtering 索引 选择 过滤
# import pandas as pd
# import numpy as np
# obj5=pd.Series(np.arange(4),index=['a','b','c','d'])
# obj5
# obj5['b']    # 1


# obj5[2:4]
# # c    2
# # d    3
# # dtype: int32


# obj5[['b','a','d']]
# # b    1
# # a    0
# # d    3
# # dtype: int32


# obj5[obj5<2]
# # a    0
# # b    1
# # dtype: int32


# obj5[[1,2]]
# # b    1
# # c    2
# # dtype: int32


# obj5['b':'c']
# # b    1
# # c    2
# # dtype: int32
```


```python
# data6=pd.DataFrame(np.arange(16).reshape((4,4)),index=['Ohio','Colorado','Utah','New York'],columns=['one','two','three','four'])
# data6
# data6['two']
# # Ohio         1
# # Colorado     5
# # Utah         9
# # New York    13
# # Name: two, dtype: int32


# data6[['one','three']]
# # 	one	three
# # Ohio	0	2
# # Colorado	4	6
# # Utah	8	10
# # New York	12	14


# data6[:2]
# # 	one	two	three	four
# # Ohio	0	1	2	3
# # Colorado	4	5	6	7


# data6[data6['three']>5]
# # 	one	two	three	four
# # Colorado	4	5	6	7
# # Utah	8	9	10	11
# # New York	12	13	14	15


# data6<5
# # 	one	two	three	four
# # Ohio	True	True	True	True
# # Colorado	True	False	False	False
# # Utah	False	False	False	False
# # New York	False	False	False	False
```


```python
# 5.2.3.1 Select with loc and iloc 使用loc和iloc选择数据
# data6=pd.DataFrame(np.arange(16).reshape((4,4)),index=['Ohio','Colorado','Utah','New York'],columns=['one','two','three','four'])
# data6


# 第一个元素一级索引确认行Colorado，第二个[]二级索引，确认列
# data6.loc['Colorado',['two','three']]
# # two      5
# # three    6
# # Name: Colorado, dtype: int32


# 按照索引取出相应的行和列
# data6.iloc[2,[3,0,1]]
# # four    11
# # one      8
# # two      9
# # Name: Utah, dtype: int32


# 把第二行都取出来
# data6.iloc[2]
# # one       8
# # two       9
# # three    10
# # four     11
# # Name: Utah, dtype: int32


# data6.iloc[[1,2],[3,0,1]]
# # 	four	one	two
# # Colorado	7	4	5
# # Utah	11	8	9


# data6.loc[:'Utah','two']
# # Ohio        1
# # Colorado    5
# # Utah        9
# # Name: two, dtype: int32


# data6.loc[['Ohio','Colorado'],['two','three']]
# # 	two	three
# # Ohio	1	2
# # Colorado	5	6


# data6.iloc[:,:3][data6.three>5]
# # 	one	two	three
# # Colorado	4	5	6
# # Utah	8	9	10
# # New York	12	13	14


# DataFrame索引选项
# def[val] 相当于data6['two'],取行或列
# df.loc[val] 根据标签名单行单列
# df.loc[:val] 根据标签，类似于切片模式多行多列
# df.loc[val1,val2] val1行，val2列
# df.iloc同理，只不过根据整数索引取
# df.at[label_i,label_j] 行列，取一个值
# df.iat[i,j] 和上边一样，用整数索引
# reindex 通过标签选择，改变行或列
# get_value,set_value方法 根据行列标签设置单个值
```


```python
# 5.2.4 Integer Indexes 整数索引
# 直接用series.[]，如果内容不是数字，就和iloc一样，如果内容是数字，就和loc一样
# ser2=pd.Series(np.arange(3),index=['a','b','c'])
# ser2
# 默认整数索引
# ser2[-1]    # 2 
# 当索引和内容都为数字是，默认为location，无法启用index，为了避免歧义发生，通常用loc和iloc声明指的是内容还是索引
```


```python
# 5.2.5 Arithmetic and Data Alignment 四则运算和数据调整
# s1=pd.Series([7.3,-2.5,3.4,1.5,0.6],index=['a','c','d','e','b'])
# s1
# s2=pd.Series([-2.1,3.6,-1.5,4,3.1],index=['a','c','e','f','g'])
# s2
# 直接相加就是索引内容相同的相加,不同的返回NaN
# s1+s2
# # a    5.2
# # b    NaN
# # c    1.1
# # d    NaN
# # e    0.0
# # f    NaN
# # g    NaN
# # dtype: float64


# 两张表相加，横轴纵轴都有所不同
# df1=pd.DataFrame(np.arange(9).reshape((3,3)),columns=list('bcd'),index=['Ohio','Texas','Colorado'])
# df1
# df2=pd.DataFrame(np.arange(12).reshape((4,3)),columns=list('bde'),index=['Utah','Ohio','Texas','Oregon'])
# df2
# df1+df2
# b,d,Texas,Ohio对应的有数，其他的都是NaN


# 横轴完全不同，都是NaN
# df1=pd.DataFrame({'A':[1,2]})
# df2=pd.DataFrame({'B':[3,4]})
# df1+df2
# # 	A	B
# # 0	NaN	NaN
# # 1	NaN	NaN
```


```python
# 5.2.5.1 Arithmetic methods with fill values
# import numpy as np
# df1=pd.DataFrame(np.arange(12).reshape(3,4),columns=list('abcd'))
# df1.loc[0,'b']=np.nan
# df1
# # 	a	b	c	d
# # 0	0	NaN	2	3
# # 1	4	5.0	6	7
# # 2	8	9.0	10	11

# df2=pd.DataFrame(np.arange(20).reshape((4,5)),columns=list('abcde'))
# df2.loc[1,'b']=np.nan
# df2.loc[1,'e']=np.nan
# df2
# # a	b	c	d	e
# # 0	0	1.0	2	3	4.0
# # 1	5	NaN	7	8	NaN
# # 2	10	11.0	12	13	14.0
# # 3	15	16.0	17	18	19.0


# 直接相加产生更多的NaN
# df1+df2
# #     a	   b	    c	    d	    e
# # 0	0.0	  NaN	   4.0     6.0	    NaN
# # 1	9.0	  NaN	  13.0	   15.0	    NaN
# # 2	18.0  20.0	  22.0	   24.0	    NaN
# # 3	NaN	  NaN	  NaN	   NaN	    NaN



# 使用add，df1里没有的值df2来补，fill_value=0先填充缺失数据，NaN=0，再求和
# df1.add(df2,fill_value=0)

# 	a	b	c	d	e
# 0	0.0	1.0	4.0	6.0	4.0
# 1	9.0	5.0	13.0	15.0	NaN
# 2	18.0	20.0	22.0	24.0	14.0
# 3	15.0	16.0	17.0	18.0	19.0


# 1/df1 所有值取倒数   等价于 1 div df1
# 1/df1 
# #     a	      b	            c         d
# # 0	inf 	NaN	        0.500000	0.333333
# # 1	0.250	0.200000	0.166667	0.142857
# # 2	0.125	0.111111	0.100000	0.090909


# 重建index时也可以用，fill_value默认为0
# df1.reindex(columns=df2.columns,fill_value=0)
# #      a	b      c	d	e
# # 0	   0	NaN	   2	3	0
# # 1	   4	5.0	   6	7	0
# # 2	   8	9.0    10	11	0


# 四则运算总结
# add,radd 加
# sub,rsub 减
# div,rdiv 除
# floorrdiv,rfloordiv 整除
# mul,rmul 乘
# pow,rpow 次方
```


```python
# 5.2.5.2 Operations between DataFrame and Series
# arr=np.arange(12).reshape((3,4))
# arr[0]
# arr-arr[0]
# 每一行都减去arr[0]
# array([[0, 0, 0, 0],
#        [4, 4, 4, 4],
#        [8, 8, 8, 8]])


# frame6=pd.DataFrame(np.arange(12).reshape((4,3)),columns=list('bde'),index=['Utah','Ohio','Texas','Oregon'])
# frame6
# series6=frame6.iloc[0]
# series6
# frame6-series6
# # 	   b	d	e
# # Utah	0	0	0
# # Ohio	3	3	3
# # Texas	6	6	6
# # Oregon	9	9	9

# series7=pd.Series(range(3),index=['b','e','f'])
# frame6-series7
# #      	b	 d	    e   	f
# # Utah	0.0	 NaN	1.0 	NaN
# # Ohio	3.0	 NaN	4.0	    NaN
# # Texas	6.0	 NaN	7.0 	NaN
# # Oregon	9.0	 NaN	10.0	NaN


# 对一列进行操作
# series8=frame6['d']
# series8   # 取出其中一列
# # 减法
# frame6.sub(series8,axis='index')
```


```python
# 5.2.6 Function Application and Mapping 函数应用和映射
# frame7=pd.DataFrame(np.random.randn(4,3),columns=list('bde'),index=['Utah','Ohio','Texas','Oregon'])
# frame7
# 取绝对值
# np.abs(frame7)


# 实现一列中的最大值-最小值，即对每一列执行同一函数操作，用apply
# f=lambda x:x.max()-x.min()
# frame7.apply(f)
# # b    2.704511
# # d    1.364052
# # e    3.316029
# # dtype: float64


# 沿着column方向横着走
# f=lambda x:x.max()-x.min()
# frame7.apply(f,axis='columns')
# # Utah      1.145669
# # Ohio      2.905529
# # Texas     0.901072
# # Oregon    1.484164
# # dtype: float64


# 返回值可以带有多个值的Series
# def f(x):
#     return pd.Series([x.min(),x.max()],index=['min','max'])

# frame7.apply(f)
# #           b          d	         e
# # min	  -0.534906	  -0.756016    -1.788792
# # max	  0.917965	  2.337259	   -0.072198


# 将frame7里边的浮点数保留两位变成字符串，用applymap，对每一列进行操作
# 保留两位小数
# format=lambda x:'%.2f' % x
# frame7.applymap(format)
# # 	      b	       d	  e
# # Utah	-0.57	-1.00	-0.62
# # Ohio	1.61	-0.87	1.65
# # Texas	-1.28	0.06	-1.30
# # Oregon	1.28	-0.95	-0.32



# 对某一特定列进行操作，用map
# frame7['e'].map(format)
# Utah      -0.86
# Ohio       1.41
# Texas      0.93
# Oregon    -1.26
# Name: e, dtype: object
```


```python
# 5.2.7 Sorting and Ranking 排序和排名
# 按索引排序用sort_index，按值排序用sort_values
# obj8=pd.Series(range(4),index=['d','a','b','c'])
# obj8
# obj8.sort_index()
# # a    1
# # b    2
# # c    3
# # d    0
# # dtype: int64



# 默认给axis=0排序
# frame=pd.DataFrame(np.arange(8).reshape((2,4)),index=['three','one'],columns=['d','a','b','c'])
# frame.sort_index()
# #      d	a	b	c
# # one   4	5	6	7
# # three	0	1	2	3


# axis=1排序需指定
# frame.sort_index(axis=1)
# # 	    a	b	c	d
# # three	1	2	3	0
# # one   	5	6	7	4


# 默认升序，想要降序令ascending=False
# frame.sort_index(axis=1,ascending=False)
# #     	d	c	b	a
# # three	0	3	2	1
# # one	    4	7	6	5
```


```python
# sort_values()按值排序
# import pandas as pd
# import numpy as np
# obj9=pd.Series([4,7,-3,2])
# obj9
# obj9.sort_values()
# # 2   -3
# # 3    2
# # 0    4
# # 1    7
# # dtype: int64


# 缺失值会被排序在Series的尾部
# obj10=pd.Series([4,np.nan,7,np.nan,-3,2])
# obj10.sort_values()
# # 4   -3.0
# # 5    2.0
# # 0    4.0
# # 2    7.0
# # 1    NaN
# # 3    NaN
# # dtype: float64


# 给DataFrame表格排序，sort_values(by=排序的依据)
# frame10=pd.DataFrame({'b':[4,7,-3,2],'a':[0,1,0,1]})
# frame10


# 根据b列排序
# frame10.sort_values(by='b')
# # 	b	a
# # 2	-3	0
# # 3	2	1
# # 0	4	0
# # 1	7	1


# 排序优先次序，先a然后b
# frame10.sort_values(by=['a','b'])
# # 	b	a
# # 2	-3	0
# # 0	4	0
# # 3	2	1
# # 1	7	1


# obj10=pd.Series([7,-5,7,4,2,0,4])
# obj10
# obj10.rank()
# 按值从小到大的顺序输出排名结果，例如1：-5排在第一位，5：0排在第二位，并列的取排名相加除以2
# # 0    6.5
# # 1    1.0
# # 2    6.5
# # 3    4.5
# # 4    3.0
# # 5    2.0
# # 6    4.5
# # dtype: float64


# 使用method='first'是先看到的优先，如  3：4和6：4都排在第四位，但先看到3：4，所以3：4排在第四位，6：4排在第五位
# obj10.rank(method='first')
# # 0    6.0
# # 1    1.0
# # 2    7.0
# # 3    4.0
# # 4    3.0
# # 5    2.0
# # 6    5.0
# # dtype: float64
```


```python
# Assign tie values the maximum rank in the group
# obj10=pd.Series([7,-5,7,4,2,0,4])
# 先排反序，由大到小排序，method=max是取最大的数，0：7和2：7最大，在第一位和第二位，排名都取二
# obj10.rank(ascending=False,method='max')
# # 0    2.0
# # 1    7.0
# # 2    2.0
# # 3    4.0
# # 4    5.0
# # 5    6.0
# # 6    4.0
# # dtype: float64


# frame11=pd.DataFrame({'b':[4.3,7,-3,2],'a':[0,1,0,1],'c':[-2,5,8,-2.5]})
# frame11
# abc对应的三个数排名
# frame11.rank(axis='columns')
# #      b	 a 	 c
# # 0	3.0	2.0	1.0
# # 1	3.0	1.0	2.0
# # 2	1.0	2.0	3.0
# # 3	3.0	2.0	1.0
```


```python
# 排名优先级
# 如果有两个并列排名的值，如并列第四
# average(默认)，求平均
# min 都是第四
# max 都是第五
# first 先看见的是第四，后来的是第五
# dense 类似于min，但组间排名加一
```


```python
# 5.2.8 Axis Index with Duplicate Labels含有重复标签的轴索引
# import pandas as pd
# import numpy as np
# obj=pd.Series(range(5),index=['a','a','b','b','c'])
# obj
# 判断索引元素是否唯一
# obj.index.is_unique     # False

# obj['a']
# # a    0
# # a    1
# # dtype: int64
```


```python
# 5.3 Summarizing and Computing Descriptive Statistics 描述性统计的概述与计算
# 主要是进行统计运算时，对缺失值的处理
# 建立一个有缺失值的表
# df=pd.DataFrame([[1.4,np.nan],[7.1,-4.5],[np.nan,np.nan],[0.75,-1.3]],index=['a','b','c','d'],columns=['one','two'])
# df

# # 默认计算axis=0的方向，竖着加，NaN默认为0
# # df.sum()
# # # one    9.25
# # # two   -5.80
# # # dtype: float64


# 计算axis=1方向，横着加
# df.sum(axis='columns')
# # a    1.40
# # b    2.60
# # c    0.00
# # d   -0.55
# # dtype: float64


# 如果要保留缺失值，则需要加入参数skipna=False，求平均值
# df.mean(axis='columns',skipna=False)
# # a      NaN
# # b    1.300
# # c      NaN
# # d   -0.275
# # dtype: float64

# 归约方法可选参数
# axis 归约轴
# skipna 排除缺失值，默认为True
# level 如果轴是多层索引MultiIndex，该参数可以缩减分组层级


# 返回最大值的索引值
# df.idxmax()
# # one    b
# # two    d
# # dtype: object


# 积累型运算
# df.cumsum()
# #      one	two
# # a	1.40	NaN
# # b	8.50	-4.5
# # c	NaN	    NaN
# # d	9.25	-5.8


# 一次性产生多个汇总统计
# df.describe()
# #            one	       two
# # count	3.000000	2.000000
# # mean	3.083333	-2.900000
# # std  	3.493685	2.262742
# # min     0.750000	-4.500000
# # 25%     1.075000	-3.700000
# # 50%     1.400000	-2.900000
# # 75%     4.250000	-2.100000
# # max     7.100000	-1.300000


# 对于非数值型数据，产生另一种汇总统计
# obj=pd.Series(['a','a','b','c']*4)
# obj
# # 0     a
# # 1     a
# # 2     b
# # 3     c
# # 4     a
# # 5     a
# # 6     b
# # 7     c
# # 8     a
# # 9     a
# # 10    b
# # 11    c
# # 12    a
# # 13    a
# # 14    b
# # 15    c
# # dtype: object

# obj.describe()
# # count     16
# # unique     3
# # top        a
# # freq       8
# # dtype: object
# 16个值，abc三个元素，a出现次数最多，重复了8次
```


```python
# 描述性统计和汇总统计
# count 非NaN值的个数
# describe 计算Series或DataFrame各列的汇总统计集合
# min，max 计算最小值，最大值
# argmin，argmax 分别计算最小值，最大值所在的索引位置（整数）
# idxmin，idxmax 分别计算最小值，最大值所在的索引标签
# quantile 计算样本的从0到1间的分位数
# sum 加和
# mean 均值
# median 中位数
# mad 平均值和平均绝对偏差
# prod 所有值的积
# var 值的样本方差
# std 值的样本标准差
# skew 样本偏度值
# kurt 样本峰度值 
# cumsum 累计值
# cumprod 值的累计积
# diff 计算第一个算数差值
# pct_change 计算百分比
```


```python
# 5.3.1 Correlation and Covariance 相关性和协方差
# returns.corr() # 返回相关性矩阵
# returns.cov()  # 返回协方差矩阵
# returns.corrwith(returns.IBM)  # 表和列之间做相关性
# returns.corrwith(volume)  # 表和表之间做相关性
```


```python
# 5.3.2 Unique Values,Value Counta,and Membership 唯一值，计数和成员属性

# import pandas as pd
# obj=pd.Series(['c','a','d','a','a','b','b','c','c'])
# obj


# 去除Series里面的重复值，每个元素留一个
# uniques=obj.unique()
# uniques   # array(['c', 'a', 'd', 'b'], dtype=object)


# 计算包含值的个数，默认按数量有多到少排序
# obj.value_counts()
# # c    3
# # a    3
# # b    2
# # d    1
# # Name: count, dtype: int64


# 判断，判断值是不是在这个位置
# mask=obj.isin(['b','c'])
# mask
# # 0     True
# # 1    False
# # 2    False
# # 3    False
# # 4    False
# # 5     True
# # 6     True
# # 7     True
# # 8     True
# # dtype: bool


# 使用布尔值索引
# obj[mask]
# # 0    c
# # 5    b
# # 6    b
# # 7    c
# # 8    c
# # dtype: object


# to_match=pd.Series(['c','a','b','b','c','a','d','e'])
# to_match
# unique_vals=pd.Series(['c','b','a'])
# unique_vals
# Index.get_indexer方法提供了一个索引数组，将可能非唯一值的数组转换为另一个唯一值数组
# pd.Index(unique_vals).get_indexer(to_match)
# # array([ 0,  2,  1,  1,  0,  2, -1, -1], dtype=int64)
```


```python
# 唯一值，计数和集合成员属性方法
# isin 值在或不在，返回布尔值
# match 计算数组每个值的索引，形成一个唯一值数组
# unique 计算Series值中唯一值数组，按照观察顺序返回
# valu_counts返回一个Series，索引是唯一值序列，值是计数个数，按照个数降序排序

# data=pd.DataFrame({'Qu1':[1,3,4,3,4],
#                    'Qu2':[2,3,1,2,3],
#                    'Qu3':[1,5,2,4,4]})
# result=data.apply(pd.value_counts).fillna(0)
# result
# # 行标签是不同的值，列标签是对应的值在不同的列出现的次数
# #     Qu1   Qu2	Qu3
# # 1	1.0   1.0	1.0
# # 2	0.0   2.0	1.0
# # 3	2.0   2.0	0.0
# # 4	2.0   0.0	2.0
# # 5	0.0   0.0	1.0
```
