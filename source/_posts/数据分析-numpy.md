---
title: '数据分析----numpy '
date: 2018-12-23 07:21:29
tags: 数据分析
---
# 数据分析---numpy

```python
import pandas as pd
import numpy as np
```

##  创建普通数组


```python
a = np.array([1,2,3])
b = np.array([[1,2,3],[4,5,6],[7,8,9]])
```


```python
b[1,1] = 10
```


```python
print(a.shape)
print(b.shape)
print(a.dtype)
print(b)
```

    (3,)
    (3, 3)
    int64
    [[1 2 3]
     [4 5 6]
     [7 8 9]]


## 创建结构数组


```python
personalType = np.dtype({
    'names':['name','age','chinese','math','english'],
    'formats':['S25','i','i','i','f']
})
students = np.array([("huzai",22,99,99,99.5),("huzai",22,99,99,99.5)],dtype=personalType)
age = students[:]['age']
print(np.mean(age))
```

    22.0



```python
print(students)
```

    [(b'huzai', 22, 99, 99, 99.5) (b'huzai', 22, 99, 99, 99.5)]


## 创建连续数组


```python
x1 = np.arange(1,11,2) #步长为2，从1开始的等差数组(不包括终值)
x2 = np.linspace(1,9,5) #将1-9分成5块，结果如上
```


```python
print(x1)
print(x2)
```

    [1 3 5 7 9]
    [1. 3. 5. 7. 9.]


## 数组间的算数运算


```python
print(np.add(x1,x2))
print(np.subtract(x1,x2))
print(np.multiply(x1,x2))
print(np.divide(x1,x2))
```

    [ 2.  6. 10. 14. 18.]
    [0. 0. 0. 0. 0.]
    [ 1.  9. 25. 49. 81.]
    [1. 1. 1. 1. 1.]


## 统计函数

### 数组中的最值 np.amin()  amax()


```python
a = np.array([[1,3,7],[2,5,8],[6,4,9]])
print(np.amin(a))
print(np.amin(a,0)) #每一列的最小值
print(np.amin(a,1)) #每行的最小值
```

    1
    [1 3 7]
    [1 2 4]


### 统计最大值与最小值之差 ptp()


```python
print(np.ptp(a))
print(np.ptp(a,0)) #每列最大值与最小值的差
print(np.ptp(a,1)) #每行最大值与最小值的差
```

    8
    [5 2 2]
    [6 6 5]


### 统计数组的百分位数 percentile(a, p, axis)  a:数组名 p 代表百分比 axis代表是行还是列


```python
print(np.percentile(a,50))
print(np.percentile(a,50,0))
print(np.percentile(a,50,1))
```

    5.0
    [2. 4. 8.]
    [3. 5. 6.]


### 统计数组中的中位数以及平均数 median() mean()


```python
print(np.median(a))
print(np.median(a,0))
print(np.median(a,1))
```

    5.0
    [2. 4. 8.]
    [3. 5. 6.]


### 数组中的加权平均值 average(a,weights)


```python
b = np.array([1,2,3,4])
wts = np.array([1,2,3,4])
print(np.average(b))
print(np.average(b,weights=wts))
```

    2.5
    3.0


### 统计数组中的标准差（std（））与方差（var（））


```python
print(np.std(b))
print(np.var(b))
```

    1.118033988749895
    1.25


## Numpy排序


```python
print(a)
print(np.sort(a))
print(np.sort(a,0))
```

    [[1 3 7]
     [2 5 8]
     [6 4 9]]
    [[1 3 7]
     [2 5 8]
     [4 6 9]]
    [[1 3 7]
     [2 4 8]
     [6 5 9]]


# 作业题


```python
st_type = np.dtype({
    'names':['name','chinese','english','math'],
    'formats':['S25','i','i','i']
})
grades = np.array([('zhangfei',66,65,30),('guanyu',95,85,98),('zhaoyun',93,92,96),('huangzhong',90,88,77),
                  ('dianwei',80,90,90)],dtype=st_type)
```


```python
print(grades)
```

    [(b'zhangfei', 66, 65, 30) (b'guanyu', 95, 85, 98)
     (b'zhaoyun', 93, 92, 96) (b'huangzhong', 90, 88, 77)
     (b'dianwei', 80, 90, 90)]



```python
chinese = grades[:]['chinese'] 
english = grades[:]['english']
math = grades[:]['math']
total = np.add(chinese,english,math)
```


```python
print(total)
```

    [131 180 185 178 170]



```python
c_a,e_a,m_a = np.average(chinese),np.average(english),np.average(math)
```


```python
print(c_a)
```

    84.8



```python

```
