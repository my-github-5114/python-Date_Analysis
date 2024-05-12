```python
# Numpy 可以直接进行复杂的运算，不需要自己写python循环，运算速度快
# 与python对比运行时间
# import numpy as np
# my_arr=np.arange(1000000)
# my_list=list(range(1000000))
# %time for _ in range(10):my_arr_1=my_arr*2
# %time for _ in range(10):my_list_1=[x*2 for x in my_list]

# CPU times: total: 15.6 ms
# Wall time: 16.6 ms
# CPU times: total: 328 ms
# Wall time: 644 ms
```


```python
# 4.1 Numpy ndarry: A Multidimensional Array（数组） Object 多维数组对象
# import numpy as np
# # 尽量这样引入，因为numpy里的函数与python内建函数大量重名
# data=np.random.randn(2,3)  # 随机数生成两行三列的数组
# print(data)

# [[-0.28305634 -1.07706883  1.85082125]
#  [ 0.0564664   0.4473467   1.37622744]]

# data_1=data*10
# print(data_1)
# 数组每个元素都×10，相加同理
# [[ -2.83056339 -10.77068835  18.50821248]
#  [  0.56466404   4.47346697  13.76227436]]


# 查看数组维度
# data.ndim   # 2
# 查看数组形状 即几乘几
# data.shape  # (2, 3)
# 查看类型
# data.dtype  # dtype('float64') 64位浮点型
```


```python
# 4.1.1 Creating ndarrays 生成
# 1 array接受序列型对象，生成数组
# import numpy as np
# data1=[[6,7.5,8,0,1],[1,2,3,4,5]]
# arr1=np.array(data1)
# print(arr1)

# [[6.  7.5 8.  0.  1. ]
#  [1.  2.  3.  4.  5. ]]

# 2 zeros 生成都是0的数组
# arr2=np.zeros(10)
# print(arr2)

# [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]

# arr3=np.zeros((2,3))
# print(arr3)

# [[0. 0. 0.]
#  [0. 0. 0.]]

# 3 empty 未初始化的数组
# arr4=np.empty((2,3,2))
# print(arr4)

# [[[1.01855798e-312 1.10343781e-312]
#   [1.01855798e-312 9.54898106e-313]
#   [1.12465777e-312 1.03977794e-312]]

#  [[1.23075756e-312 1.12465777e-312]
#   [1.06099790e-312 9.76118064e-313]
#   [1.10343781e-312 1.90979621e-312]]]


# 4 arange 未初始化的数组
# arr5=np.arange(4)
# print(arr5)

# [0 1 2 3]
```


```python
# 数组生成的函数
# array 接受：列表元组数组等序列，复制
# asarray 如果已经是ndarray则不再复制
# arange python内建函数range的数组版
# ones接受形状，生成形状全是一样的数组 全是1
# ones_like 接受数组，生成形状一样的 全是1
# zeros全是0
# zeros_like 接受数组，生成形状一样的全是0
# empty接受形状，未初始化
# empty_like
# full指定数值，指定类型
# full_like
# eye，identity n*n,对角线为1，其余位置为0

# import numpy as np
# data1=[[6,7.5,8,0,1],[1,2,3,4,5]]
# arr1=np.identity (2*2)   # eye同理
# print(arr1)

# [[1. 0. 0. 0.]
#  [0. 1. 0. 0.]
#  [0. 0. 1. 0.]
#  [0. 0. 0. 1.]]
```


```python
# 4.1.2 Data Types for ndarrays数据类型
# dtype 定义数据类型
# import numpy as np
# arr1=np.array([1,2,3],dtype=np.float64)
# print(arr1.dtype)
# # float64
# arr2=np.array([1,2,3],dtype=np.int32)
# print(arr2.dtype)
# # int32


# astype 转换数据类型
# arr3=np.array([1,2,3,4,5])
# print(arr3.dtype)   # int32
# float_arr3=arr3.astype(np.float64)
# print(float_arr3.dtype)   # float64


# arr4=np.array([1.1,3.1,-1.6,0.5])
# arr_int=arr4.astype(np.int32)
# print(arr_int)  # [ 1  3 -1  0]


# arr5=np.array(['1.25','-3.8','36'],dtype=np.string_)
# arr5_float=arr5.astype(np.float64)
# print(arr5_float)  # [ 1.25 -3.8  36.  ]


# int_array=np.arange(10)
# calibers=np.array([0.22,0.27,0.12])
# arr6=int_array.astype(calibers.dtype)
# print(arr6)   # [0. 1. 2. 3. 4. 5. 6. 7. 8. 9.]


# empty_unit32=np.empty(8,dtype='u4')
# print(empty_unit32)

# [2576980378 1072798105  858993459 1072902963 2576980378 1073322393
#  3435973837 1073532108]
```


```python
# 4.1.3 Arithmetic with Numpy Arrays 数组计算
# import numpy as np
# arr=np.array([[1,2,3],[4,5,6]])
# print(arr)
# [[1 2 3]
#  [4 5 6]]
# arr1=arr*arr  # 元素逐个相乘，相加相减相除，幂乘同理
# print(arr1)
# [[ 1  4  9]
#  [16 25 36]]

# arr2=np.array([[0,4,1],[5,3,8]])
# arr2>arr
# 对应位置比较大小
# array([[False,  True, False],
#        [ True, False,  True]])
```


```python
# 4.1.4 Basic Indexing and Slicing 基础索引与切片
# 不是复制，是取其中一部分视图，所有的改变会改变原列表
# import numpy as np
# arr3=np.arange(10)
# print(arr3)   # [0 1 2 3 4 5 6 7 8 9]


# # arr3[5]   # 5
# # arr3[5:8]  # array([5, 6, 7]) 左闭右开
# arr3[5:7]=21
# print(arr3)   # [ 0  1  2  3  4 21 21  7  8  9]

# arr3_slice=arr3[5:7]
# arr3_slice   # # array([21, 21])

# arr3_slice[1]=128
# arr3   # array([  0,   1,   2,   3,   4,  21, 128,   7,   8,   9])  原列表改变，改一个值就复制会引起内存问题
# 要想复制，要使用arr[5:7].copy()
```


```python
# arr2d=np.array([[1,2,3],[4,5,6],[7,8,9]])
# # 多维数组取其中一个元素
# arr2d[2]   # array([7, 8, 9])  
# 取某个单个元素
# arr2d[2][2]   # 9
# arr3d=np.array([[[1,2,3],[4,5,6],[7,8,9]],[[10,11,12],[13,14,15],[16,17,18]]])
# # arr3d[0]
# # array([[1, 2, 3],
# #        [4, 5, 6],
# #        [7, 8, 9]])
# old_value=arr3d[0].copy()
# arr3d[0]=12
# arr3d
# # array([[[12, 12, 12],
# #         [12, 12, 12],
# #         [12, 12, 12]],

# #        [[10, 11, 12],
# #         [13, 14, 15],
# #         [16, 17, 18]]])

# arr3d[0]=old_value
# arr3d
# 原列表不改变
# array([[[ 1,  2,  3],
#         [ 4,  5,  6],
#         [ 7,  8,  9]],

#        [[10, 11, 12],
#         [13, 14, 15],
#         [16, 17, 18]]])
```


```python
# 4.1.4.1 Indexing with slices 切片索引
# import numpy as np
# arr=np.array([[1,2,3],[4,5,6],[7,8,9]])
# arr[0:2]
# # array([[1, 2, 3],
# #        [4, 5, 6]])


# arr[:2,1:]
# # array([[2, 3],
# #        [5, 6]])
```


```python
# 4.1.5 布尔索引
# import numpy as np
# names=np.array(['Bob','Joe','Will','Bob','Will','Joe','Joe'])
# data=np.random.randn(7,4)  # 7×4随机数
# print(data)
# # [[ 0.64261385  1.25452291 -1.42908772  0.0354356 ]
# #  [ 0.17381709  1.66950844 -1.70403017 -0.01042558]
# #  [-0.2905558   0.0490229   0.25250497  0.75914893]
# #  [-1.27447327  1.04342158  0.10780604 -0.85593072]
# #  [ 1.37248857  1.55612077 -0.5245691   2.45482182]
# #  [ 1.26811595 -0.47000541  0.2360635   0.14577894]
# #  [-1.54247941  0.22195753  0.1154015   0.90983937]]

# 将这组布尔值传入data，作为索引取出数组的值
# names=='Bob'  # array([ True, False, False,  True, False, False, False])
# data[names=='Bob']
# # array([[ 0.64261385,  1.25452291, -1.42908772,  0.0354356 ],
# #        [-1.27447327,  1.04342158,  0.10780604, -0.85593072



# |或，&和
# mask=(names=='Bob')|(names=='Will')
# print(mask)   # [ True False  True  True  True False False]
# data[mask]
```


```python
# 4.1.6 Fancy Indexing 神奇索引
# arr=np.empty((8,4))
# for i in range(8):
#     arr[i]=i
# arr
# # array([[0., 0., 0., 0.],
# #        [1., 1., 1., 1.],
# #        [2., 2., 2., 2.],
# #        [3., 3., 3., 3.],
# #        [4., 4., 4., 4.],
# #        [5., 5., 5., 5.],
# #        [6., 6., 6., 6.],
# #        [7., 7., 7., 7.]])


# 用列表或数组做索引取出的就是相应的行，负数是从后往前数
# arr[[4,3,0,2]]
# # array([[4., 4., 4., 4.],
# #        [3., 3., 3., 3.],
# #        [0., 0., 0., 0.],
# #        [2., 2., 2., 2.]])
```


```python
# reshape 重新设定形状
# import numpy as np
# arr=np.arange(32).reshape((8,4))
# arr
# # array([[ 0,  1,  2,  3],
# #        [ 4,  5,  6,  7],
# #        [ 8,  9, 10, 11],
# #        [12, 13, 14, 15],
# #        [16, 17, 18, 19],
# #        [20, 21, 22, 23],
# #        [24, 25, 26, 27],
# #        [28, 29, 30, 31]])

# arr[[1,5,7,2],[0,3,1,2]]  # array([ 4, 23, 29, 10])
# # 取第1行的0号元素，第5行的3号元素，（7，1），（2，2）

# arr[[1,5,7,2]][:,[0,3,1,2]]
# # 取出第1，5，7，2行，冒号代表元素全部取出，[0，3，1，2]代表排列顺序
# # array([[ 4,  7,  5,  6],
# #        [20, 23, 21, 22],
# #        [28, 31, 29, 30],
# #        [ 8, 11,  9, 10]])
```


```python
# 4.1.7 Transposing Arrays and Swapping Axes 数组转置和换轴
# import numpy as np 
# arr=np.arange(15).reshape((3,5))
# arr
# # array([[ 0,  1,  2,  3,  4],
# #        [ 5,  6,  7,  8,  9],
# #        [10, 11, 12, 13, 14]])


# 转置
# arr.T
# # array([[ 0,  5, 10],
# #        [ 1,  6, 11],
# #        [ 2,  7, 12],
# #        [ 3,  8, 13],
# #        [ 4,  9, 14]])


# dot矩阵内积，每行×每列得到对应元素
# arr1=np.dot(arr,arr.T)
# arr1
# # array([[ 30,  80, 130],
# #        [ 80, 255, 430],
# #        [130, 430, 730]])
```


```python
# arr=np.arange(24).reshape((2,3,4))
# arr
# # array([[[ 0,  1,  2,  3],
# #         [ 4,  5,  6,  7],
# #         [ 8,  9, 10, 11]],

# #        [[12, 13, 14, 15],
# #         [16, 17, 18, 19],
# #         [20, 21, 22, 23]]])


# arr1=arr.transpose(1,0,2)  # 上方（2，3，4）的顺序变为（3，2，4），0号轴与1号轴换位置
# arr1
# # array([[[ 0,  1,  2,  3],
# #         [12, 13, 14, 15]],

# #        [[ 4,  5,  6,  7],
# #         [16, 17, 18, 19]],

# #        [[ 8,  9, 10, 11],
# #         [20, 21, 22, 23]]])


# arr2=arr.swapaxes(1,2)  # (2，3，4)变为（2，4，3） 0号轴不变，1号和2号轴换位置
# arr2
# # array([[[ 0,  4,  8],
# #         [ 1,  5,  9],
# #         [ 2,  6, 10],
# #         [ 3,  7, 11]],

# #        [[12, 16, 20],
# #         [13, 17, 21],
# #         [14, 18, 22],
# #         [15, 19, 23]]])
```


```python
# 4.2 Universal Functions: Fast Element-Wise Array Functions
# 通用函数，即对数组的每一个数都进行相同处理的函数
# import numpy as np
# arr=np.arange(10)
# arr   # array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

# 1 开根号，负数不能开根号，返回nan，原数组不变，如果想改变原数组将改变的值赋给arr np.sqrt(arr1,arr1)
# arr1=np.sqrt(arr)
# arr1  
# # array([0.        , 1.        , 1.41421356, 1.73205081, 2.        ,
# #        2.23606798, 2.44948974, 2.64575131, 2.82842712, 3.        ])


# 2 e的 n次方(e的0-9次方)
# arr2=np.exp(arr)
# arr2
# # array([1.00000000e+00, 2.71828183e+00, 7.38905610e+00, 2.00855369e+01,
# #        5.45981500e+01, 1.48413159e+02, 4.03428793e+02, 1.09663316e+03,
# #        2.98095799e+03, 8.10308393e+03])


# 3 生成随机数
# x=np.random.randn(4)
# x   # array([ 0.40999375, -0.65055012, -0.09639029,  0.85298594])


# 4 对应位置的比较，将较大的值取出
# x=np.random.randn(4)
# print(x)    # [ 0.99834516  0.81376888  0.51731666 -0.94062075]
# y=np.random.randn(4)
# print(y)    # [-0.37373265 -0.96751743 -0.91227346  0.343041  ]
# arr3=np.maximum(x,y)
# arr3       # array([0.99834516, 0.81376888, 0.51731666, 0.343041  ])



# 5 随机生成的每个元素都乘5
# arr4=np.random.randn(4)*5
# print(arr4)   # [-3.9109039  -0.40180584  2.34285132 -0.69509815]


# 6 将浮点数分为小数和整数的部分
# remainder,whole_part=np.modf(arr4)
# print(remainder)   # [-0.9109039  -0.40180584  0.34285132 -0.69509815]   小数部分
# print(whole_part)    # [-3. -0.  2. -0.]   整数部分


# 总结
# abs、fabs 整数或浮点数取绝对值
# sqrt 平方根
# square 平方
# exp e的n次方
# log、log10、log2、log1p
# sign 符号值，1，0，-1代表正数、0、负数
# ceil 大于等于给定数字的最小整数
# floor 小于等于给定数字的最大整数
# rint 保留整数，dtype不变
# modf 小数部分和整数部分分开，分别作为数组返回
# isnan 判断返回的东西是不是nan，nan不是数值，得到布尔值
# isfinite、isinf 判断是否有限、是否无限，得到布尔值
# cos、cosh、sin、sinh、tan、tanh 三角函数
# arccos、arccosh、arcsin、arcsinh、arctan、arctanh 反三角函数
# logical_not 对数组的元素取反，相当于~arr




# arr=np.array([[-1,-9,3],[4,5,6]])
# # arr1=~arr
# # arr1
# # array([[ 0,  8, -4],
# #        [-5, -6, -7]])



# arr2=np.logical_not(arr)
# arr2
# # array([[False, False, False],
# #        [False, False, False]])
```


```python
# 二元通用函数，即针对两个数组进行的操作
# add 数组的对应元素相加
# subtract 第二个数组中提出第一个数组中的元素
# multiply 对应元素相乘
# divide，floor_divide 除或整除
# power 得到[1,2],[3,4]得到[1^3=1，2^4=16]
# maximum，fmax 最大值，fmax忽略nan
# minimum，fmin 最小值，fmin忽略nan
# mod 除法余数
# copysign[2,1][-1,2]变成[-2,1]  取符号
# greater,greater_equal,less,less_equal,equal,not_equal 大于，大于等于，小于，小于等于，等于，不等于
# logical_and,logical_or,logical_xor  逻辑操作 和，或，抑或
```


```python
# 4.3 Array-Oriented Programming with Arrays 面向数组的 programming
# 定义一个 -5 到 5 的精度为 0.1 的数组，即100个数
# import numpy as np
# points=np.arange(-5,5,0.1)
# print(points)


# meshgrid用法 用一维数组生成二维网格
# arr1=np.array([1,2,3])
# arr2=np.array([2,3,4])
# xs,ys=np.meshgrid(arr1,arr2)   #生成3×3维矩阵
# print(xs)
# # [[1 2 3]
# #  [1 2 3]
# #  [1 2 3]]
# print(ys)
# # [[2 2 2]
# #  [3 3 3]
# #  [4 4 4]]


# arr3=np.array([1,2])
# arr4=np.array([3,4,5])
# xs,ys=np.meshgrid(arr3,arr4)    #生成 2×3 维矩阵
# print(xs)
# # [[1 2]
# #  [1 2]
# #  [1 2]]
# print(ys)
# # [[3 3]
# #  [4 4]
# #  [5 5]]
```


```python
# Expressing Conditinal Logic as Array Operations
# 将条件逻辑作为数组操作
# xarr=np.array([1.1,1.2,1.3,1.4,1.5])
# yarr=np.array([2.1,2.2,2.3,2.4,2.5])
# cond=np.array([True,False,True,True,False])
# if满足时取 x，if不满足时取 y
# result=[(x if c else y) for x,y,c in zip(xarr,yarr,cond)]
# result   # [1.1, 2.2, 1.3, 1.4, 2.5]

# 局限：数组大的话会很慢，因为用的是python中的函数，如果是多维数组就不行了，所以引入 where

# result1=np.where(cond,xarr,yarr)  # 如果是则取xarr，不是则取yarr
# result1   # array([1.1, 2.2, 1.3, 1.4, 2.5])

# arr1=np.random.randn(2,2)
# print(arr1)
# # [[-0.84054603 -0.53822705]
# #  [ 0.28500213 -1.14870127]]
# arr2=arr1>0
# print(arr2)
# # [[False False]
# #  [ True False]]
# result2=np.where(arr1>0,2,-2)
# result2
# # array([[-2, -2],
# #        [ 2, -2]])
```


```python
# 4.3.2 Mathematical and Statistical Methods 数学和统计学方法
# import numpy as np
# arr=np.arange(20).reshape((5,4))   # 5是 axis=0，4是 axis=1
# print(arr)

# # 求平均数
# arr1=arr.mean()  
# print(arr1)   # 9.5

# # 求和
# arr2=arr.sum()
# print(arr2)   # 190

#  # 每一行求平均数，求和
# arr3=arr.mean(axis=1)  
# print(arr3)   # [ 1.5  5.5  9.5 13.5 17.5]

# # 每一列求平均，求和
# arr4=arr.mean(axis=0)  
# print(arr4)   # [ 8.  9. 10. 11.]

# 累积和
# arr5=np.array([0,1,2,3,4,5,6,7])
# arr6=arr5.cumsum()
# print(arr6)  # [ 0  1  3  6 10 15 21 28]  0，0+1，0+1+2……


# 纵向相加
# arr7=np.array([[0,1,2],[3,4,5],[6,7,8]])
# arr8=arr7.cumsum(axis=0)   
# print(arr8)
# # [[ 0  1  2]
# #  [ 3  5  7]
# #  [ 9 12 15]]


# 横向相加
# arr9=arr7.cumsum(axis=1)   
# print(arr9)
# # [[ 0  1  3]
# #  [ 3  7 12]
# #  [ 6 13 21]]


# axis不给值默认为一维数组
# arr10=arr7.cumsum()   
# print(arr10)   # [ 0  1  3  6 10 15 21 28 36]



# 从第一位开始横向乘积
# arr11=arr7.cumprod(axis=1)
# print(arr11)
# # [[  0   0   0]
# #  [  3  12  60]
# #  [  6  42 336]]


# 纵向乘积
# arr12=arr7.cumprod(axis=0)
# print(arr12)
# # [[ 0  1  2]
# #  [ 0  4 10]
# #  [ 0 28 80]]


# axis不给值默认为一维数组
# arr13=arr7.cumprod()
# print(arr13)   # [0 0 0 0 0 0 0 0 0]
```


```python
# 基础数组统计方法
# sum 沿着轴方向计算所有元素的累和，0长度的数组累积和为0
# mean 数学平均，0长度的数组平均值为NaN
# std、var 标准差和方差，可以选择自由调整度，默认字母是n
# min、max 最小值和最大值
# argmin、argmax 最小值和最大值的位置
# cumsum 从0开始元素累积和
# cumprod 从1开始元素累积积
```


```python
# Methods for Boolean Arrays 布尔值数组的方法


# arr=np.random.randn(5)
# 大于 0的加起来
# arr1=(arr>0).sum()
# print(arr1)


# bools=np.array([False,False,True,False])
# # 有一个True，输出值就为True
# bools1=bools.any()
# bools1   # True

# # 全部为True，输出值为True
# bools2=bools.all()
# print(bools2)   # False
```


```python
# 4.3.4 Sorting 排序
# import numpy as np

# arr=np.array([1,3,6,4,8,5,7,6,9])
# 从小到大排序，改变本身
# arr.sort()
# print(arr)   # [1 3 4 5 6 6 7 8 9]



# arr1=np.array([[1,4,6,2],[3,5,2,7],[2,5,7,1]])
# 沿着横轴排序
# arr1.sort(1)
# print(arr1)
# # [[1 2 4 6]
# #  [2 3 5 7]
# #  [1 2 5 7]]


# 沿着纵轴排序
# arr1.sort(0)
# print(arr1)
# # [[1 4 2 1]
# #  [2 5 6 2]
# #  [3 5 7 7]]


# large_arr=np.random.randn(1000)
# large_arr.sort
# large_arr[int(0.05*len(large_arr))]  # 取出large_arr数组中的第1000×0.05个数，取整数
# 0.0072615009787473156 类似于 5% 分位点的概念

```


```python
# 4.3.5 Unique and Other Set Logic 唯一值和其他集合逻辑

# names=np.array(['Bob','Joe','Will','Bob','Will','Joe','Joe'])
# 去掉重复值，只取一个，并且重新排序，生成数组
# names1=np.unique(names)
# print(names1)   # ['Bob' 'Joe' 'Will']


# python则用sorted排序使用集合实现去掉重复值，集合不允许重复，生成列表
# names2=sorted(set(names))
# names2   # ['Bob', 'Joe', 'Will']  


# values=np.array([6,0,0,3,2,5,6])
# # 检查数组中的数字是否在[2，3，6]里边
# value1=np.in1d(values,[2,3,6]) 
# print(value1)   # [ True False False  True  True False  True]


# 数组的集合操作
# unique(x) 计算x的唯一值，并排序
# intersect1d(x,y) 计算x和y的交集，并排序
# union1d(x,y) 计算x和y的并集，并排序
# in1d(x,y) 计算x中的元素是否包含在y中，返回布尔值数组
# setdiff1d(x,y)差集，在x中但不在y中的x元素
# setxor1d(x,y) 在x或在y，不同时在xy中的元素
```


```python
# 4.4 File Input and Output with Arrays 使用数组进行文件输入和输出
# arr=np.arange(10)
# np.save('some_array',arr)
# np.load('some_array.npy')   # array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])


# savez默认未压缩，里边有多个数组
# np.savez('array_archive.npz',a=arr,b=arr)
# arch=np.load('array_archive.npz')    # load 读取后是字典
# print(arch)   # NpzFile 'array_archive.npz' with keys: a, b
# arch['a']   # array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])



# 存入压缩文件
# np.savez_compressed('arrays_compressed.npz',a=arr,b=arr)
# arch1=np.load('arrays_compressed.npz')       # load 读取后是字典
# arch1['a']    # array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
```


```python
# 4.5 Linear Algebra 线性函数
# diag 将矩阵的对角元素--一维数组之间转换，空白默认为0
# dot 矩阵点乘
# trace 对角元素和
# det 矩阵的行列式
# eig 特征值和特征向量
# inv 逆矩阵
# pinv 计算矩阵的Moore-Penrose伪逆向
# qr 计算QR分解
# svd 计算奇异值分解(SVD)
# slove 求解x的线性系统 Ax=b，其中A是方阵
# lstsq 计算Ax=b的最小二乘解


# import numpy as np
# x=np.array([[1,2,3],[4,5,6]])
# y=np.array([[1,2],[3,4],[5,6]])
# z=np.dot(x,y)
# print(z)
# # [[22 28]
# #  [49 64]]


# x的转置与x点积
# from numpy.linalg import inv,qr
# x=np.random.randn(3,3)   # randn是生成正态分布 0为平均值，1为方差
# mat=x.T.dot(x)   
# print(mat)


# inv逆矩阵  矩阵×本身的逆矩阵 = E 即单位矩阵，对角线为1，其余为0
# arr=np.array([[1,2],[4,5]])
# mat1=arr.dot(inv(arr))
# print(mat1)
# # # [[1. 0.]
# # #  [0. 1.]]


# QR分解
# mat2=np.random.randn(3,3)
# q,r=qr(mat)
# print(q)   # q是正规正交矩阵
# print(r)   # r是上三角矩阵
# # [[-1.61951481 -0.72164882 -1.83875647]
# #  [ 0.         -0.44458973 -1.80671822]
# #  [ 0.          0.          0.17341655]]
```


```python
# 4.6 Pseudorandom Number Generation 伪随机数生成
# numpy.random 中的部分函数列表
# seed 向随机数生成器传递随机状态种子
# permutation 返回一个序列的随机排列，或返回一个乱序的整数范围序列
# shuffle 随机排列一个序列
# rand 从均匀分布中抽取样本
# randint 根据给定的从低到高的范围抽取随机整数
# randn 从均值为0，方差为1的正态分布中抽取样本(MATLAB型接口)
# binomial 从二项分布中抽取样本
# normal 从正态分布中抽取样本
# beat 从beat分布中抽取样本
# chisqueare 从卡方分布中抽取样本
# gamma 从伽马分布中抽取样本
# uniform 从均匀[0,1)分布中抽取样本
```


```python
# import numpy as np
# samples=np.random.normal(size=(3,3))
# print(samples)
# # [[-0.02260497 -0.06496877 -1.55129649]
# #  [-0.23939642  0.2567792  -0.90787032]
# #  [ 0.73436985  0.1669227   0.08924868]]

```


```python
# 4.7 Example:Random Walks 应用举例：随机漫步
# 模拟掷硬币100次，正面为 1，反面为-1
# import numpy as np
# import random
# import matplotlib.pyplot as plt  # 引入画图工具
# position=0    # 起点
# walk=[position]   # 要走到的位置
# steps=1000 # 步数 准备实验1000次
# for i in range(1000):
#     step=1 if random.randint(0,1) else -1
#     # random.randint 取0或1，对应if False和True 对应step 1或-1
#     position+=step
#     walk.append(position)
#     # 得到的值放在walk里
# plt.figure()
# plt.plot(walk[:100])




# np.random.seed(12345)   # 随便给个起点
# nsteps=100
# draws=np.random.randint(0,2,size=nsteps)
# steps=np.where(draws>0,1,-1)
# # 大于0取1，反之取-1
# walk=steps.cumsum()  # 累积和
# print(walk.min())
# print(walk.max())
# np.abs(walk)>=10   # 判断大于10的情况
# (np.abs(walk)>=10).argmax()     # True 第一次出现的位置
```


```python
# 4.7.1 Simulating Many Random Walks at Once 同时模拟多次随机漫步
# trys=np.array([[True,False,True],[False,False,True]])


# trys.any()
# 数组看作整体，所有[]去掉，只要又True就返回True
# trys.any(0) 
# 竖着，沿axis=0方向  array([ True, False,  True])
# trys.any(1) 
# 横着，沿着axis=1方向   array([ True,  True])


# trys.sum()   # 3
# trys.sum(0)    
# 竖着，沿axis=0方向   array([1, 0, 2])
# trys.sum(1)   
# 横着，沿着axis=1方向   array([2, 1])


# import numpy as np
# trys=np.array([[1,2,3],[4,5,6]])
# print(trys.argmax())  # 整体看，6出现在第5位    5
# print(trys.argmax(0))  # 竖着看，4，5，6都出现在第一位    [1 1 1]
# print(trys.argmax(1))   # 横着看，3，6都出现在第二位   [2 2]
```


```python
# 投掷硬币1000次，5000组实验同时做

# nwalks=5000
# nsteps=1000
# draws=np.random.randint(0,2,size=(nwalks,nsteps))
# draws.shape
# steps=np.where(draws>0,1,-1)
# walks=steps.cumsum(1)  # 5000*1000的数组 ,在1000个数里边求和
# # print(walks.max())
# # print(walks.min())
# np.abs(walks>=30)   # 返回布尔值数组
# hits30=(np.abs(walks)>=30).any(1)  # 确保有大于等于30的
# hits30.sum() # 看有多少组有大于等于30的情况
# walks[hits30]   # 将5000组里有大于等于30的组选出来
# walks[hits30].shape    # (3369, 1000)
# crossing_time=(np.abs(walks[hits30])>=30).argmax(1)
# # 跨过了30的组里，第一次出现True是在什么位置
# crossing_time   # array([585, 263, 755, ..., 207, 509, 479], dtype=int64)
# crossing_time.mean() # 求平均值  平均大于30出现是在第几次
```
