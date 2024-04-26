```python
# 内省：？
# ？：显示信息
# ？：函数，显示文档字符串（注释）
# ？？：显示函数源代码
# *名称*？ 显示numpy顶层函数中包含名称的函数列表
```


```python
# b=[1,2,3]
# b?
```


```python
# def add_numbers(a,b):
#     """
#     add two numbers together ## 把两个数相加
#     Return ## 返回值为
#     the_sum : type of arguments ## 加和，类型为输入变量类型
#     """
#     return a+b
```


```python
# add_numbers?
```


```python
# add_numbers??
```


```python
# import numpy as ny
# np.*load*?
```


```python
# isinstance检查对象的类型
```


```python
# a=5
# b=4.5
```


```python
# isinstance(a,int)
```


```python
# isinstance(b,float)
```


```python
# 属性和方法
```


```python
# c='foo'
```


```python
# c.isupper
```


```python
# 验证是否可迭代
```


```python
# def isiterable(obj):
#     try:
#         iter(obj)
#         return True
#     except TypeError:  # 类型错误，不可遍历
#         return False
```


```python
# isiterable('a string')
```


```python
# 数值类型
# 整型和浮点型
# 整型可以储存任意大小的数字
```


```python
# intvariable=20020117
# intvariable**10
```


```python
# 浮点型float，每个浮点数都是双精度64位数
```


```python
# faval=3.141592653579
```


```python
# faval=314159.2653579e-5
# faval+1
# # 4.141592653579
```


```python
# 整数除法自动转型为浮点数
```


```python
# 3/2
```


```python
# //整数除完还是整数
```


```python
# 3//2
```


```python
# 多行字符串，用三引号
```


```python
# c="""
# 一顿火锅
# 两顿烧烤
# 三杯啤酒
# 四块蛋糕
# 五个猪蹄
# 六个烤鸭
# 七根烤肠
# 八斤榴莲
# 九足饭饱
# 食不我待
# """
```


```python
# c.count('\n')
```


```python
# print('I\'m a good girl')  # 字符串内部使用单引号 添加\后能正常输出 反斜杠视作转义字符
# print('\a')
# print('\\')
```


```python
# raw 原生的  加r'可以将\直接看作字符串形式输出
```


```python
# s=r'人\生\不\易，且\行\且\珍\惜'   
# print(s)
```


```python
# 字节与 Unicode
# 字符串，字节与 Unicode的转换
```


```python
# val='Joyeux Noël'   # 字符串类型
```


```python
# encode 将 Unicode字符串转换为UTF-8字符
```


```python
# val_utf8=val.encode('utf-8')  # 或者用 b'Joyeux Noël'定义字符文本为 bytes类型
```


```python
# val_utf8  # b'Joyeux No\xc3\xabl'   Bytes的类型
```


```python
# decode，对 Unicode 解码
```


```python
# val_utf8.decode('utf-8')
```


```python
# 类型转化
# str\bool\int\float
# s='3.141592653579'
```


```python
# float(s)
```


```python
# int(fs)
```


```python
# bool(fs)
```


```python
# bool(0)  # 0的布尔值是False
```


```python
# bool(s)  # 字符串的布尔值是True，空字符串的布尔值是False
```


```python
# None 可以作为一个常用的参数默认值  None不仅是一个关键字，还是NoneType类型的唯一实例
```


```python
# def add_and_maybe_multiply(a,b,c=None):
#     result=a+b
#     if c is not None:
#         result=result*c
#     else:
#         return result
```


```python
# type(None)
```


```python
# 日期和时间
# datetime.datetime 是不可变类型
# 格式说明  %Y 四位年份，%y 两位年份，%m 两位月份，%d 两位天数，%H 24小时制，%I 12小时制，%M 两位分钟，%S 两位秒值
# %w 星期[0，6] 0指星期天  
# %U 一年中第几个星期，星期天是每周第一天，第一个星期天前的一周为第0周
# %W 一年中第几个星期，星期一是每周第一天，第一个星期一前的一周为第0周
# %z UTC时区偏差,格式为+HHMM 或-HHMM
# %F %Y-%m-%d的简写  2024-4-26
# %d %m/%d/%y的简写  24/4/26
```


```python
# from datetime import datetime,date,time
# dt=datetime(2024,4,26,18,28,45)
# dt.day
```


```python
# dt.minute
```


```python
# dt.hour
```


```python
# dt.month
```


```python
# dt.year
```


```python
# dt.strftime('%Y/%m/%d %H:%M')   # '2024/04/26 18:28'
```


```python
# dt.strptime('20240426','%Y%m%d')  # 将字符串转换为datetime的对象 datetime.datetime(2024, 4, 26, 0, 0)
```


```python
# dt.replace(minute=0,second=0)  # 替换时间中的数值  datetime.datetime(2024, 4, 26, 18, 0)
```


```python
# 计算两个时间点之间隔了多长时间
```


```python
# from datetime import datetime,date,time
# dt1=datetime(2024,6,8,9,45,35)
# dt2=datetime(2024,4,26,18,35,24)
# delta  # delta 是产生一种新的类型   datetime.timedelta(days=42, seconds=54611)
```


```python
# dt1+delta   # datetime.datetime(2024, 7, 21, 0, 55, 46)
```
