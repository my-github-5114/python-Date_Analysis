```python
# import numpy as np
# import pandas as pd
# PREVIOUE_MAX_ROWS=pd.options.display.max_rows
# pd.options.display.max_rows=20
# np.random.seed(12345)
# import matplotlib.pyplot as plt
# plt.rc('figure',figsize=(10,6))
# np.set_printoptions(precision=4,suppress=True)
```


```python
# 7.1 处理缺失值 Handling Missing Data
# NaN:Not a Number   NA:Not available   None
# string_data=pd.Series(['aardvark','artichoke',np.nan,'avocado'])
# string_data.isnull()
# # 0    False
# # 1    False
# # 2     True
# # 3    False
# # dtype: bool
# string_data[0]=None
# string_data
# # 0         None
# # 1    artichoke
# # 2          NaN
# # 3      avocado
# # dtype: object
```


```python
# 7.1.1 过滤缺失值 Filtering Out Missing Data
# from numpy import nan as NA
# data=pd.Series([1,NA,3.5,NA,7])
# data
# # 0    1.0
# # 1    NaN
# # 2    3.5
# # 3    NaN
# # 4    7.0
# # dtype: float64


# # 删除缺失值
# data.dropna()
# # 0    1.0
# # 2    3.5
# # 4    7.0
# # dtype: float64
# # 等价于 data[data.notnull()]


# DataFrame对象
# data=pd.DataFrame([[1,6.5,3],[1,NA,NA],[NA,NA,NA],[NA,6.5,3]])
# # data
# #     0	  1    2
# # 0	1.0	 6.5  3.0
# # 1	1.0	 NaN  NaN
# # 2	NaN	 NaN  NaN
# # 3	NaN	 6.5  3.0

# data.dropna()删除包含缺失值的行或列
# cleaned=data.dropna()
# cleaned
# # 	 0	 1	 2
# # 0	1.0	6.5	3.0

# how='all'表示删除全部为缺失值的行
# data.dropna(how='all')
# #      0 	 1	 2
# # 0	1.0	6.5	3.0
# # 1	1.0	NaN	NaN
# # 3	NaN	6.5	3.0


# data[3]=NA
# data
# # 	0	 1 	 2	 3
# # 0	1.0	6.5	3.0	NaN
# # 1	1.0	NaN	NaN	NaN
# # 2	NaN	NaN	NaN	NaN
# # 3	NaN	6.5	3.0	NaN


# 删除全为缺失值的列 传入参数axis=1
# data.dropna(axis=1,how='all')
# # 	0	 1	 2
# # 0	1.0	6.5	3.0
# # 1	1.0	NaN	NaN
# # 2	NaN	NaN	NaN
# # 3	NaN	6.5	3.0


# 删除包含两个缺失值以上的行
# import numpy as np
# df=pd.DataFrame(np.random.randn(7,3))
# df.iloc[:4,1]=NA
# df.iloc[:2,2]=NA
# df
# # 	     0  	   1	      2
# # 0	-0.204708	  NaN 	     NaN
# # 1	-0.555730	  NaN	     NaN
# # 2	0.092908	  NaN	     0.769023
# # 3	1.246435	  NaN     	-1.296221
# # 4	0.274992	0.228913	1.352917
# # 5	0.886429	-2.001637	-0.371843
# # 6	1.669025	-0.438570	-0.539741

# df.dropna(thresh=2)
# # 2	0.331286	NaN	        0.069877
# # 3	0.246674	NaN	        1.004812
# # 4	1.327195	-0.919262	-1.549106
# # 5	0.022185	0.758363	-0.660524
# # 6	0.862580	-0.010032	0.050009
```


```python
# 7.1.2 补全缺失值 Filling In Missing Data
# fillna()可以使用常数来代替缺失值
# df.fillna(0)
# # 	0	           1	       2
# # 0	-1.541996	0.000000	0.000000
# # 1	0.286350	0.000000	0.000000
# # 2	0.331286	0.000000	0.069877
# # 3	0.246674	0.000000	1.004812
# # 4	1.327195	-0.919262	-1.549106
# # 5	0.022185	0.758363	-0.660524
# # 6	0.862580	-0.010032	0.050009


# 填充缺失值时使用字典，可以指定不同列用不同的值填充
# df.fillna({1:0.5,2:0})
# #     	0	       1	      2
# # 0	-1.541996	0.500000	0.000000
# # 1	0.286350	0.500000	0.000000
# # 2	0.331286	0.500000	0.069877
# # 3	0.246674	0.500000	1.004812
# # 4	1.327195	-0.919262	-1.549106
# # 5	0.022185	0.758363	-0.660524
# # 6	0.862580	-0.010032	0.050009


# fillna 返回的是一个新对象，但是也可以修改已存在的对象，改变df本身
# df.fillna(0,inplace=True)
# df
# #          0	         1	      2
# # 0	-1.541996	0.000000	0.000000
# # 1	0.286350	0.000000	0.000000
# # 2	0.331286	0.000000	0.069877
# # 3	0.246674	0.000000	1.004812
# # 4	1.327195	-0.919262	-1.549106
# # 5	0.022185	0.758363	-0.660524
# # 6	0.862580	-0.010032	0.050009



# method='ffill'默认是前项填充
# df=pd.DataFrame(np.random.randn(6,3))
# df.iloc[2:,1]=NA
# df.iloc[4:,2]=NA
# df
# # 	 0	            1	      2
# # 0	0.670216	0.852965	-0.955869
# # 1	-0.023493	-2.304234	-0.652469
# # 2	-1.218302	NaN	        1.074623
# # 3	0.723642	NaN	        1.001543
# # 4	-0.503087	NaN	        NaN
# # 5	-0.726213	NaN	        NaN

# df.fillna(method='ffill')
# #     	0        	1	      2
# # 0	-1.157719	0.816707	0.433610
# # 1	1.010737	1.824875	-0.997518
# # 2	0.850591	1.824875	0.912414
# # 3	0.188211	1.824875	-0.114928
# # 4	2.003697	1.824875	-0.114928
# # 5	0.118110	1.824875	-0.114928


# 参数limit，设置最大填充范围
# df.fillna(method='ffill',limit=2)
# #          0	         1	        2
# # 0	0.152677	-1.565657	-0.562540
# # 1	-0.032664	-0.929006	-0.482573
# # 2	-0.036264	-0.929006	0.980928
# # 3	-0.589488	-0.929006	-0.528735
# # 4	0.457002	NaN	        -0.528735
# # 5	-1.022487	NaN	        -0.528735


# data=pd.Series([1,NA,3.5,NA,7])
# data
# # 0    1.0
# # 1    NaN
# # 2    3.5
# # 3    NaN
# # 4    7.0
# # dtype: float64

# 用均值填充
# data.fillna(data.mean())
# # 0    1.000000
# # 1    3.833333
# # 2    3.500000
# # 3    3.833333
# # 4    7.000000
# # dtype: float64
```


```python
# 7.2 数据转换 Data Transformation
# 7.2.1 删除重复值 Removing Duplicates
# 由于某些原因，DataFrame中会出现重复行
# import numpy as np
# import pandas as pd
# data=pd.DataFrame({'k1':['one','two']*3+['two'],
#                   'k2':[1,1,2,3,3,4,4]})
# data
# #      k1   k2
# # 0	  one   1
# # 1	  two   1
# # 2	  one   2
# # 3	  two   3
# # 4	  one   3
# # 5	  two   4
# # 6	  two   4

# 判断该行之前是否出现过
# data.duplicated()
# # 0    False
# # 1    False
# # 2    False
# # 3    False
# # 4    False
# # 5    False
# # 6     True
# # dtype: bool


# 删除重复的行
# data.drop_duplicates()
# # 	k1	 k2
# # 0	one	 1
# # 1	two	 1
# # 2	one	 2
# # 3	two	 3
# # 4	one	 3
# # 5	two	 4


# 对于某列的重复值
# data['val']=range(7)
# data
# # 	k1	 k2	 val
# # 0	one	 1	 0
# # 1	two	 1	 1
# # 2	one	 2	 2
# # 3	two	 3	 3
# # 4	one	 3	 4
# # 5	two	 4	 5
# # 6	two	 4	 6


# 指定删除某一列的重复值
# data.drop_duplicates(['k1'])
# # 	k1	 k2	 val
# # 0	one	 1	 0
# # 1	two	 1	 1


# 默认重复值保留第一个检测到的，传入keep='last'将会从后往前保留
# data.drop_duplicates(['k2'],keep='last')
# # 	k1	 k2	 val
# # 1	two	 1	 1
# # 2	one	 2	 2
# # 4	one	 3	 4
# # 6	two	 4	 6
```


```python
# 7.2.2 使用函数或映射进行数据转换 Transforming Data Using a Function or Mapping
# data=pd.DataFrame({'food':['bacon','pulled pork','bacon',
#                            'Pastrami','corned beef','Bacon',
#                            'pastrami','honey ham','nova lox'],
#                    'ounces':[4,3,12,6,7.5,8,3,5,6]})
# data
# #     food	    ounces
# # 0	bacon	    4.0
# # 1	pulled pork	3.0
# # 2	bacon	    12.0
# # 3	Pastrami	6.0
# # 4	corned beef	7.5
# # 5	Bacon    	8.0
# # 6	pastrami	3.0
# # 7	honey ham	5.0
# # 8	nova lox	6.0


# 对食品中肉的种类做个标签
# meat_to_animal={
#     'bacon':'pig',
#     'pulled pork':'pig',
#     'pastrami':'cow',
#     'corned beef':'cow',
#     'honey ham':'pig',
#     'nova lox':'salmon'
# }

# 将字母统一为小写
# lowercased=data['food'].str.lower()
# lowercased
# # 0          bacon
# # 1    pulled pork
# # 2          bacon
# # 3       pastrami
# # 4    corned beef
# # 5          bacon
# # 6       pastrami
# # 7      honey ham
# # 8       nova lox
# # Name: food, dtype: object

# .map()按照字典的指定进行匹配
# data['animal']=lowercased.map(meat_to_animal)
# data
# #     food	    ounces	animal
# # 0	bacon	    4.0	     pig
# # 1	pulled pork	3.0	     pig
# # 2	bacon	    12.0	 pig
# # 3	Pastrami	6.0	     cow
# # 4	corned beef	7.5	     cow
# # 5	Bacon	    8.0	     pig
# # 6	pastrami	3.0	     cow
# # 7	honey ham	5.0	     pig
# # 8	nova lox	6.0	     salmon

# 或者写成 data['food'].map(lambda x:meat_to_animal[x.lower()])
# x变量为data表格中的'food'列，输入变量进行小写，再与meat_to_animal中的值进行匹配，输出匹配结果
```


```python
# 7.2.3 替代者 Replacing Values
# data=pd.Series([1,-999,2,-999,1000,3])
# data
# # 0       1
# # 1    -999
# # 2       2
# # 3    -999
# # 4    1000
# # 5       3
# # dtype: int64

# data.replace(-999,np.nan)
# # 0       1.0
# # 1       NaN
# # 2       2.0
# # 3       NaN
# # 4    1000.0
# # 5       3.0
# # dtype: float64


# 一次替代多个值
# data.replace([-999,1000],np.nan)
# # 0    1.0
# # 1    NaN
# # 2    2.0
# # 3    NaN
# # 4    NaN
# # 5    3.0
# # dtype: float64


# 用列表替换为不同的值
# data.replace([-999,1000],[np.nan,0])

# 用字典的形式传递参数
# data.replace({-999:np.nan,1000:0})
# # 0    1.0
# # 1    NaN
# # 2    2.0
# # 3    NaN
# # 4    0.0
# # 5    3.0
# # dtype: float64
```


```python
# 7.2.4 重命名轴索引 Renaming Axis Indexes
# data=pd.DataFrame(np.arange(12).reshape((3,4)),
#                  index=['Ohio','Colorado','New York'],
#                  columns=['one','two','three','four'])
# data
# # 	      one  two  three  four
# # Ohio	    0	1	2	   3
# # Colorado	4	5	6	   7
# # New York	8	9	10	   11


# 取出索引中0,1,2,3位置的字母 大写
# transform=lambda x:x[:4].upper()
# transform


# data的index属性中取出前四个，并执行upper函数
# data.index.map(transform)
# # Index(['OHIO', 'COLO', 'NEW '], dtype='object')


# 让原来的index等于转换为大写处理之后的
# data.index=data.index.map(transform)
# # data
# # # 	  one	two three  four
# # # OHIO	0	1	 2	    3
# # # COLO	4	5	 6	    7
# # # NEW	    8	9	 10	   11


# 或者使用rename的方法
# data.rename(index=str.title,columns=str.upper)


# 用字典指定替换方案
# data.rename(index={'OHIO':'INDIANA'},
#            columns={'three':'peekaboo'})
# # 	      one	two 	peekaboo	four
# # Ohio	    0	1	       2	     3
# # Colorado	4	5	       6	     7
# # New York	8	9	       10	     11


# 改变原有变量，传入参数inplace=True
# data.rename(index={'OHIO':'INDIANA'},inplace=True)
```


```python
# 7.2.5 离散化和分箱 Discretization and Binning
# ages=[20,22,25,27,21,23,37,31,61,45,41,32]

# 分为18-25，26-35，36-60，61-100
# bins=[18,25,35,60,100]

# pd.cut(ages,bins)进行分组，返回的对象是一个特殊的对象
# cats=pd.cut(ages,bins)
# cats
# # [(18, 25], (18, 25], (18, 25], (25, 35], (18, 25], ..., (25, 35], (60, 100], (35, 60], (35, 60], (25, 35]]
# # Length: 12
# # Categories (4, interval[int64, right]): [(18, 25] < (25, 35] < (35, 60] < (60, 100]]


# 查看里面的属性，12个数字对应分组标签
# cats.codes
# # array([0, 0, 0, 1, 0, 0, 2, 1, 3, 2, 2, 1], dtype=int8)


# 相当于x轴
# cats.categories
# # IntervalIndex([(18, 25], (25, 35], (35, 60], (60, 100]], dtype='interval[int64, right]')


# 统计每个里面的个数
# pd.value_counts(cats)
# # (18, 25]     5
# # (25, 35]     3
# # (35, 60]     3
# # (60, 100]    1
# # Name: count, dtype: int64


# 开区间与闭区间可以自己设置，传入right=False可以变为左闭右开区间
# pd.cut(ages,[18,26,36,61,100],right=False)
# # [[18, 26), [18, 26), [18, 26), [26, 36), [18, 26), ..., [26, 36), [61, 100), [36, 61), [36, 61), [26, 36)]
# # Length: 12
# # Categories (4, interval[int64, left]): [[18, 26) < [26, 36) < [36, 61) < [61, 100)]


# 可以给分类价格名称
# group_names=['Youth','YoungAdult','MiddleAged','Senior']
# pd.cut(ages,bins,labels=group_names)
# # ['Youth', 'Youth', 'Youth', 'YoungAdult', 'Youth', ..., 'YoungAdult', 'Senior', 'MiddleAged', 'MiddleAged', 'YoungAdult']
# # Length: 12
# # Categories (4, object): ['Youth' < 'YoungAdult' < 'MiddleAged' < 'Senior']


# 数据均匀分成4份 precision将十进制精度限制为两位
# data=np.random.rand(20)
# pd.cut(data,4,precision=2)
# # [(0.019, 0.26], (0.75, 1.0], (0.75, 1.0], (0.75, 1.0], (0.26, 0.51], ..., (0.51, 0.75], (0.26, 0.51], (0.019, 0.26], (0.26, 0.51], (0.51, 0.75]]
# # Length: 20
# # Categories (4, interval[float64, right]): [(0.019, 0.26] < (0.26, 0.51] < (0.51, 0.75] < (0.75, 1.0]]


# qcut基于样本的分位数分割
# data=np.random.randn(100)
# data
# cats=pd.qcut(data,4)
# # cats
# # # [(-0.573, 0.0548], (0.0548, 0.742], (0.742, 1.942], (-2.508, -0.573], (0.0548, 0.742], ..., (-0.573, 0.0548], (-2.508, -0.573], (-0.573, 0.0548],
# # (0.0548, 0.742], (0.0548, 0.742]]
# # # Length: 100
# # # Categories (4, interval[float64, right]): [(-2.508, -0.573] < (-0.573, 0.0548] < (0.0548, 0.742] < (0.742, 1.942]]


# 每个范围都是250个
# pd.value_counts(cats)
# # (-2.276, -0.734]     25
# # (-0.734, -0.0822]    25
# # (-0.0822, 0.556]     25
# # (0.556, 2.083]       25
# # Name: count, dtype: int64


# 可以传入自定义分位数，0-1之间的数组
# cats=pd.qcut(data,[0,0.1,0.5,0.9,1])
# cats
# pd.value_counts(cats)
# # (-1.35, -0.0682]                40
# # (-0.0682, 1.508]                40
# # (-2.0949999999999998, -1.35]    10
# # (1.508, 3.562]                  10
# # Name: count, dtype: int64
```


```python
# 7.2.6 检测和过滤异常值 Detecting and Filtering Outliers
# 一个具有正态分布数据的DataFrame
# data=pd.DataFrame(np.random.randn(1000,4))
# data.describe()

# 找出一列中绝对值大于三的值
# col=data[2]
# col[np.abs(col)>3]
# # 24    -3.415046
# # 364   -3.110693
# # 468   -3.017806
# # 687    3.299053
# # 779    3.033676
# # Name: 2, dtype: float64

# 选出所有绝对值大于三的，使用any方法
# data[(np.abs(data)>3).any(1)]


# 绝对值大于3的数，变为-3或者3
# np.sign(data),数值的符号，-1或1
# data[np.abs(data)>3]=np.sign(data)*3
# data.describe()
# # 取出正负号
# np.sign(data).head()
```


```python
# 7.2.7 置换和随机抽样 Permutation and Random Sampling
# df=pd.DataFrame(np.arange(5*4).reshape((5,4)))
# df
# 生成一个长度为5的随机数组
# sampler=np.random.permutation(5)
# print(sampler)
# # array([3 0 1 2 4])


# take函数，按索引排序
# df.take(sampler)
# #     0	1	2	3
# # 3	12	13	14	15
# # 0	0	1	2	3
# # 1	4	5	6	7
# # 2	8	9	10	11
# # 4	16	17	18	19


# 生成一个随机样本，不可重复
# df.sample(n=3)
# # 	0	1	2	3
# # 1	4	5	6	7
# # 4	16	17	18	19
# # 3	12	13	14	15


# 随机抽样，可重复的话令replace=True
# choices=pd.Series([5,7,-1,6,4])
# draws=choices.sample(n=10,replace=True)
# draws
# # 1    7
# # 0    5
# # 4    4
# # 4    4
# # 2   -1
# # 1    7
# # 4    4
# # 2   -1
# # 2   -1
# # 4    4
# # dtype: int64
```


```python
# 7.2.8 计算指标/虚拟变量 Computing Indicator/Dummy Variables
# df=pd.DataFrame({'key':['b','b','a','c','a','b'],'data1':range(6)})
# df
# 将abc变为三列，用1标记
# pd.get_dummies(df['key'])
# # 表明这一行是哪个属性
# # 	  a	      b	     c
# # 0	False	True	False
# # 1	False	True	False
# # 2	True	False	False
# # 3	False	False	True
# # 4	True	False	False
# # 5	False	True	False


# 列前边加上前缀key
# dummies=pd.get_dummies(df['key'],prefix='key')
# dummies
# #      key_a 	key_b	key_c
# # 0	False	True	False
# # 1	False	True	False
# # 2	True	False	False
# # 3	False	False	True
# # 4	True	False	False
# # 5	False	True	False


# 与其他列合并
# df_with_dummy=df[['data1']].join(dummies)
# df_with_dummy
# #   data1	 key_a	key_b	key_c
# # 0	0	 False	True	False
# # 1	1	 False	True	False
# # 2	2	 True	False	False
# # 3	3	 False	False	True
# # 4	4	 True	False	False
# # 5	5	 False	True	False


# 如果一行属于多个类别
# mnames=['movie_id','title','genres']
# movies=pd.read_table('datasets/movielens/movies.dat',sep='::',
#                     header=None,names=mnames)
# movies[:10]
# all_genres=[]
# for x in movies.genres:
#     all_genres.extend(x.split('|'))
# genres=pd.unique(all_genres)
```


```python
# 7.3 字符串操作 String Manipulation
# 7.3.1 字符串对象方法 String Object Methods
# 拆分
# val='a,b, guido'
# val.split(',')
# # ['a', 'b', ' guido']


# 常常和split一起使用，用于清楚空格
# pieces=[x.strip() for x in val.split(',')]
# pieces
# # ['a', 'b', 'guido']


# 加号合并字符串
# first,second,third=pieces
# first+'::'+second+'::'+third
# # 'a::b::guido'


# join方法合并字符串
# '::'.join(pieces)
# # 'a::b::guido'

# 判断
# 'guido' in val     # True

# 获取索引
# val.index('b')    # 2


# 获取索引
# val.find(':')    # -1
# 与index的区别是如果该字符不存在，index会抛出一个异常，find会返回-1


# 计数
# val.count(',')    # 2

# 替换
# val.replace(',','::')    # 'a::b:: guido'
```


```python
# 7.3.2 正则表达式 Regular Expressions
# 导入，分割和字符串操作很像，只不过是在re下的函数，使用正则表达式
# import re
# text='foo     bar\t baz  \tqux'
# re.split('\s+',text)    # ['foo', 'bar', 'baz', 'qux']


# 可以把写好的正则表达式规则存下来，之后重复使用
# regex=re.compile('\s+')
# regex.split(text)   # ['foo', 'bar', 'baz', 'qux']


# 获得匹配正则表达式内容的列表
# regex.findall(text)   # ['     ', '\t ', '  \t']
```


```python
# 7.3.3 向量化字符串函数 Vectorized String Functions in pandas
# 数据中含有缺失值使用正则表达式不方便
# data={'Dave':'dave@google.com','Steve':'steve@gmail.com',
#      'Rob':'rob@gmail.com','Wes':np.nan}
# data=pd.Series(data)
# data
# # Dave     dave@google.com
# # Steve    steve@gmail.com
# # Rob        rob@gmail.com
# # Wes                  NaN
# # dtype: object

# Series的str属性可以跳过NA值
# data.str.contains('gmails')  # 判断字符串是否含有gmail
# # Dave     False
# # Steve    False
# # Rob      False
# # Wes        NaN
# # dtype: object


# 切片
# data.str[:5]
# # Dave     dave@
# # Steve    steve
# # Rob      rob@g
# # Wes        NaN
# # dtype: object
```
