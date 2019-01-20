---
title: 数据分析-pandas
date: 2018-12-25 08:21:06
tags: 数据分析
---

# 数据分析----pandas

## 核心数据结构 Series & DataFrame


```python
import pandas as pd
import numpy as np
from pandas import Series, DataFrame
```

### **Series是一个定长的字典序列**，它有两个基本属性**index 、 value** index 默认是 0 ,1,2,3 递增的，也可以自己指定索引 index=['a', 'b', 'c']

###  创建Series的三种方式


```python
x1 = Series([1,2,3,4])
x2 = Series(data=[1,2,3,4],index=['a','b','c','d'])
dic = {'a':1,'b':2,'c':3,'d':4}
x3 = Series(dic)
print(x1)
print(x2)
print(x3)
```

    0    1
    1    2
    2    3
    3    4
    dtype: int64
    a    1
    b    2
    c    3
    d    4
    dtype: int64
    a    1
    b    2
    c    3
    d    4
    dtype: int64


### DataFrame类似数据库中的表，可以将其看成是由有相同的索引的Series组成

### 创建DataFra几种方式


```python
data = {"chinese":[90,80,70,60,50],'math':[70,80,70,90,60],'english':[30,50,70,80,60]}
df1 = DataFrame(data=data,index=['zhangfei','guanyu','zhaoyun','huangzhong','machao'])
print(df)
```

                chinese  english  math
    zhangfei         90       30    70
    guanyu           80       50    80
    zhaoyun          70       70    70
    huangzhong       60       80    90
    machao           50       60    60



```python
import xlrd
df2 = DataFrame(pd.read_excel('datas/grades.xlsx'))
df2 = df2.drop_duplicates()
```


```python
print(df2)
```

         姓名   高数  英语  C++
    0   蒋广佳   43  69   61
    1    廖菲   80  64   62
    2   沈秀玲   68  74   98
    3    韦丹   48  53   64
    4   张梦雅   72  73   96
    5   赵雅欣   60  63   70
    6   曹海广   74  60   20
    7   陈泽灿   38  21   92
    8    邓杰   88  67   84
    9   高海亮   86  74   96
    10  顾晓冬   84  60   90
    11  侯星宇   64  69   96
    12  江宜哲   60  33   70
    13  李洪汀   76  56   84
    14  梁杨杨   68  54   94
    15   刘辉   68  63   98
    16  罗嘉豪   39  44   56
    17  施亚君   90  63   90
    18   孙添   64  63   78
    19   王杰   74  60   76
    20   王泽   52  48   94
    21  徐孟圆   60  69   74
    22  杨福程   70  49   76
    23  尤澳晨   91  67   86
    24   翟佳   78  73   88
    25   张旭  100  60   98
    26  支星哲   80  63  100
    27  邹湘涛   54  40   90


## 数据清洗

### 删除不必要的行或列


```python
#删除行
df2 = df2.drop(columns=['姓名'])
print(df2)
```

         高数  英语  C++
    0    43  69   61
    1    80  64   62
    2    68  74   98
    3    48  53   64
    4    72  73   96
    5    60  63   70
    6    74  60   20
    7    38  21   92
    8    88  67   84
    9    86  74   96
    10   84  60   90
    11   64  69   96
    12   60  33   70
    13   76  56   84
    14   68  54   94
    15   68  63   98
    16   39  44   56
    17   90  63   90
    18   64  63   78
    19   74  60   76
    20   52  48   94
    21   60  69   74
    22   70  49   76
    23   91  67   86
    24   78  73   88
    25  100  60   98
    26   80  63  100
    27   54  40   90



```python
#删除列
df2 = df2.drop(index = [27])
print(df2)
```

         高数  英语  C++
    0    43  69   61
    1    80  64   62
    2    68  74   98
    3    48  53   64
    4    72  73   96
    5    60  63   70
    6    74  60   20
    7    38  21   92
    8    88  67   84
    9    86  74   96
    10   84  60   90
    11   64  69   96
    12   60  33   70
    13   76  56   84
    14   68  54   94
    15   68  63   98
    16   39  44   56
    17   90  63   90
    18   64  63   78
    19   74  60   76
    20   52  48   94
    21   60  69   74
    22   70  49   76
    23   91  67   86
    24   78  73   88
    25  100  60   98
    26   80  63  100


### 重命名列名


```python
df2 = df2.rename(columns={'高数':'math','英语':'english'})
```

### 去除重复的值


```python
df2 = df2.drop_duplicates()
```

### 更改数据格式


```python
df2['math'] = df2['math'].astype('str')
#df2['math'].astype(np.int64)
```

### 清除数据间的空格


```python
df2['math'] = df2['math'].map(str.strip) #删除左右两边的空格
df2['math'] = df2['math'].map(str.lstrip) #删除左边的空格（str.rstrip 右边的空格）
```

### 删除指定字符


```python
df2['math'] = df2['math'].str.strip('$')
```

### 大小写转换


```python
df2.columns = df2.columns.str.upper() #全部大写（lower（）全部小写 title（）首字母大写）
```


```python
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MATH</th>
      <th>ENGLISH</th>
      <th>C++</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>43</td>
      <td>69</td>
      <td>61</td>
    </tr>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>64</td>
      <td>62</td>
    </tr>
    <tr>
      <th>2</th>
      <td>68</td>
      <td>74</td>
      <td>98</td>
    </tr>
    <tr>
      <th>3</th>
      <td>48</td>
      <td>53</td>
      <td>64</td>
    </tr>
    <tr>
      <th>4</th>
      <td>72</td>
      <td>73</td>
      <td>96</td>
    </tr>
    <tr>
      <th>5</th>
      <td>60</td>
      <td>63</td>
      <td>70</td>
    </tr>
    <tr>
      <th>6</th>
      <td>74</td>
      <td>60</td>
      <td>20</td>
    </tr>
    <tr>
      <th>7</th>
      <td>38</td>
      <td>21</td>
      <td>92</td>
    </tr>
    <tr>
      <th>8</th>
      <td>88</td>
      <td>67</td>
      <td>84</td>
    </tr>
    <tr>
      <th>9</th>
      <td>86</td>
      <td>74</td>
      <td>96</td>
    </tr>
    <tr>
      <th>10</th>
      <td>84</td>
      <td>60</td>
      <td>90</td>
    </tr>
    <tr>
      <th>11</th>
      <td>64</td>
      <td>69</td>
      <td>96</td>
    </tr>
    <tr>
      <th>12</th>
      <td>60</td>
      <td>33</td>
      <td>70</td>
    </tr>
    <tr>
      <th>13</th>
      <td>76</td>
      <td>56</td>
      <td>84</td>
    </tr>
    <tr>
      <th>14</th>
      <td>68</td>
      <td>54</td>
      <td>94</td>
    </tr>
    <tr>
      <th>15</th>
      <td>68</td>
      <td>63</td>
      <td>98</td>
    </tr>
    <tr>
      <th>16</th>
      <td>39</td>
      <td>44</td>
      <td>56</td>
    </tr>
    <tr>
      <th>17</th>
      <td>90</td>
      <td>63</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>64</td>
      <td>63</td>
      <td>78</td>
    </tr>
    <tr>
      <th>19</th>
      <td>74</td>
      <td>60</td>
      <td>76</td>
    </tr>
    <tr>
      <th>20</th>
      <td>52</td>
      <td>48</td>
      <td>94</td>
    </tr>
    <tr>
      <th>21</th>
      <td>60</td>
      <td>69</td>
      <td>74</td>
    </tr>
    <tr>
      <th>22</th>
      <td>70</td>
      <td>49</td>
      <td>76</td>
    </tr>
    <tr>
      <th>23</th>
      <td>91</td>
      <td>67</td>
      <td>86</td>
    </tr>
    <tr>
      <th>24</th>
      <td>78</td>
      <td>73</td>
      <td>88</td>
    </tr>
    <tr>
      <th>25</th>
      <td>100</td>
      <td>60</td>
      <td>98</td>
    </tr>
    <tr>
      <th>26</th>
      <td>80</td>
      <td>63</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>



### 使用apply函数对数据进行清洗


```python
#df2['MATH'] = df2['MATH'].apply(str.lower)
df2['MATH'] = df2['MATH'].astype(np.int64)
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MATH</th>
      <th>ENGLISH</th>
      <th>C++</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>43</td>
      <td>69</td>
      <td>61</td>
    </tr>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>64</td>
      <td>62</td>
    </tr>
    <tr>
      <th>2</th>
      <td>68</td>
      <td>74</td>
      <td>98</td>
    </tr>
    <tr>
      <th>3</th>
      <td>48</td>
      <td>53</td>
      <td>64</td>
    </tr>
    <tr>
      <th>4</th>
      <td>72</td>
      <td>73</td>
      <td>96</td>
    </tr>
    <tr>
      <th>5</th>
      <td>60</td>
      <td>63</td>
      <td>70</td>
    </tr>
    <tr>
      <th>6</th>
      <td>74</td>
      <td>60</td>
      <td>20</td>
    </tr>
    <tr>
      <th>7</th>
      <td>38</td>
      <td>21</td>
      <td>92</td>
    </tr>
    <tr>
      <th>8</th>
      <td>88</td>
      <td>67</td>
      <td>84</td>
    </tr>
    <tr>
      <th>9</th>
      <td>86</td>
      <td>74</td>
      <td>96</td>
    </tr>
    <tr>
      <th>10</th>
      <td>84</td>
      <td>60</td>
      <td>90</td>
    </tr>
    <tr>
      <th>11</th>
      <td>64</td>
      <td>69</td>
      <td>96</td>
    </tr>
    <tr>
      <th>12</th>
      <td>60</td>
      <td>33</td>
      <td>70</td>
    </tr>
    <tr>
      <th>13</th>
      <td>76</td>
      <td>56</td>
      <td>84</td>
    </tr>
    <tr>
      <th>14</th>
      <td>68</td>
      <td>54</td>
      <td>94</td>
    </tr>
    <tr>
      <th>15</th>
      <td>68</td>
      <td>63</td>
      <td>98</td>
    </tr>
    <tr>
      <th>16</th>
      <td>39</td>
      <td>44</td>
      <td>56</td>
    </tr>
    <tr>
      <th>17</th>
      <td>90</td>
      <td>63</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>64</td>
      <td>63</td>
      <td>78</td>
    </tr>
    <tr>
      <th>19</th>
      <td>74</td>
      <td>60</td>
      <td>76</td>
    </tr>
    <tr>
      <th>20</th>
      <td>52</td>
      <td>48</td>
      <td>94</td>
    </tr>
    <tr>
      <th>21</th>
      <td>60</td>
      <td>69</td>
      <td>74</td>
    </tr>
    <tr>
      <th>22</th>
      <td>70</td>
      <td>49</td>
      <td>76</td>
    </tr>
    <tr>
      <th>23</th>
      <td>91</td>
      <td>67</td>
      <td>86</td>
    </tr>
    <tr>
      <th>24</th>
      <td>78</td>
      <td>73</td>
      <td>88</td>
    </tr>
    <tr>
      <th>25</th>
      <td>100</td>
      <td>60</td>
      <td>98</td>
    </tr>
    <tr>
      <th>26</th>
      <td>80</td>
      <td>63</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>




```python
def plus(df):
    df['Total'] = df['MATH']+df['ENGLISH']+df['C++']
    return df
df2 = df2.apply(plus,axis=1)
```


```python
print(df2)
```

        MATH  ENGLISH  C++  Total
    0     43       69   61    173
    1     80       64   62    206
    2     68       74   98    240
    3     48       53   64    165
    4     72       73   96    241
    5     60       63   70    193
    6     74       60   20    154
    7     38       21   92    151
    8     88       67   84    239
    9     86       74   96    256
    10    84       60   90    234
    11    64       69   96    229
    12    60       33   70    163
    13    76       56   84    216
    14    68       54   94    216
    15    68       63   98    229
    16    39       44   56    139
    17    90       63   90    243
    18    64       63   78    205
    19    74       60   76    210
    20    52       48   94    194
    21    60       69   74    203
    22    70       49   76    195
    23    91       67   86    244
    24    78       73   88    239
    25   100       60   98    258
    26    80       63  100    243


## pandas中常用的统计函数

![1.jpg](1.jpg)

```python
print(df2.describe())
```

                 MATH    ENGLISH         C++       Total
    count   27.000000  27.000000   27.000000   27.000000
    mean    69.444444  59.703704   81.148148  210.296296
    std     16.113380  12.406000   17.933003   34.410212
    min     38.000000  21.000000   20.000000  139.000000
    25%     60.000000  55.000000   72.000000  193.500000
    50%     70.000000  63.000000   86.000000  216.000000
    75%     80.000000  68.000000   95.000000  239.500000
    max    100.000000  74.000000  100.000000  258.000000



```python

```
