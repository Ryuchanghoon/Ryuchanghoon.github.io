---
layout: single
title: 데이터프레임(DataFrame)
---


이 글은 데이터 분석에 있어서 기본적인 함수 활용법을 실습한 코드 입니다.

a = 1, b = 1 이라는 변수에 여러가지 연산자를 사용할 수 있습니다. +,-,*,/,//,% 등 이 있습니다. 결과는 차례로 2,0,1,1,1,1 입니다.

변수에 여러 값을 넣은 형태를 볼 수 있습니다. 이것은 '리스트' 라고 부르며, 형태는 [ ] 형태로 나타납니다.


```python
a = [1,2,3,4,5]
b = [6,7,8,9]
a+b
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
a_str = ['hello', 'this']
b_str = ['is', 'python']
a_str + b_str
```




    ['hello', 'this', 'is', 'python']



위와 같이, 리스트에는 숫자 뿐만 아니라 문자 또한 넣을 수 있습니다.

또한 리스트에는 함수를 적용할 수 있는데, 대표적으로 sum(), max(), min() 등이 있습니다.



이제부터 본격적으로 데이터프레임에 대해서 알아보겠습니다.

데이터프레임은 직사각형의 모양으로 나타납니다. 세로 열은 'column', '변수'라고 부르며, 그 데이터프레임의 속성을 파악할 수 있습니다.
가로열은 'case', '행' 이라고 부르며, 각 데이터의 정보를 담고 있습니다. 즉 데이터가 크다 라는 말은 행, 혹은 열이 많다는 말과 같습니다.

파이썬은 기본적으로 여러 패키지를 불러오기 용이합니다. 대표적인 패키지로 pandas, numpy, 그래프를 그릴때는 matplotlib, seaborn 등 여러 패키지가 존재합니다.


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

보통 import해서 쓰기 위해서는, 따로 패키지 설치가 필요로 합니다.

실습을 위해 데이터프레임을 생성하겠습니다.


```python
data = pd.DataFrame({'name' : ['a','b','c','d','e','f','g','h','i','j','k','l','z'],
                     'age' : [5,6,1,7,8,23,5,6,7,8,4,3,16],
                     'height': [150,140,160,130,178,987,765,456,2345,1234,67,234,890],
                     'weight':[15,14,13,17,18,129,123,345,678,345,123,345,456],
                     'class': [1,3,2,3,1,2,4,3,2,1,2,3,1],
                     'grade': ['A','B','C','F','A','A','D','B','C','C','B','A','C']})
data                    
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
      <th>name</th>
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>class</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>5</td>
      <td>150</td>
      <td>15</td>
      <td>1</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>6</td>
      <td>140</td>
      <td>14</td>
      <td>3</td>
      <td>B</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>1</td>
      <td>160</td>
      <td>13</td>
      <td>2</td>
      <td>C</td>
    </tr>
    <tr>
      <th>3</th>
      <td>d</td>
      <td>7</td>
      <td>130</td>
      <td>17</td>
      <td>3</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>e</td>
      <td>8</td>
      <td>178</td>
      <td>18</td>
      <td>1</td>
      <td>A</td>
    </tr>
    <tr>
      <th>5</th>
      <td>f</td>
      <td>23</td>
      <td>987</td>
      <td>129</td>
      <td>2</td>
      <td>A</td>
    </tr>
    <tr>
      <th>6</th>
      <td>g</td>
      <td>5</td>
      <td>765</td>
      <td>123</td>
      <td>4</td>
      <td>D</td>
    </tr>
    <tr>
      <th>7</th>
      <td>h</td>
      <td>6</td>
      <td>456</td>
      <td>345</td>
      <td>3</td>
      <td>B</td>
    </tr>
    <tr>
      <th>8</th>
      <td>i</td>
      <td>7</td>
      <td>2345</td>
      <td>678</td>
      <td>2</td>
      <td>C</td>
    </tr>
    <tr>
      <th>9</th>
      <td>j</td>
      <td>8</td>
      <td>1234</td>
      <td>345</td>
      <td>1</td>
      <td>C</td>
    </tr>
    <tr>
      <th>10</th>
      <td>k</td>
      <td>4</td>
      <td>67</td>
      <td>123</td>
      <td>2</td>
      <td>B</td>
    </tr>
    <tr>
      <th>11</th>
      <td>l</td>
      <td>3</td>
      <td>234</td>
      <td>345</td>
      <td>3</td>
      <td>A</td>
    </tr>
    <tr>
      <th>12</th>
      <td>z</td>
      <td>16</td>
      <td>890</td>
      <td>456</td>
      <td>1</td>
      <td>C</td>
    </tr>
  </tbody>
</table>
</div>



실습을 위해 무작위로 데이터프레임을 생성했습니다.

이제부터 데이터에 함수를 적용하도록 하겠습니다.


```python
sum(data['age'])//13
```




    7




```python
max(data['height'])
```




    2345



위의 결과와 같이, 'age'의 평균값은 7, 'height'의 최댓값은 2345입니다. 물론 이 외에도 파이썬에서 사용하는 여러함수 적용이 가능합니다.

하지만 위처럼 작은 데이터라면 어렵지 않게 데이터 형태 파악이 가능하지만, 보통 excel, json, csv 등 비교적 크기가 큰 데이터를 다뤄야할 경우가 더 많습니다. 그때, 원활한 파악을 위해서 사용하는 함수로 head(), tail(), shape, info(), describe()가 있습니다.


```python
data.head()
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
      <th>name</th>
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>class</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>5</td>
      <td>150</td>
      <td>15</td>
      <td>1</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>6</td>
      <td>140</td>
      <td>14</td>
      <td>3</td>
      <td>B</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>1</td>
      <td>160</td>
      <td>13</td>
      <td>2</td>
      <td>C</td>
    </tr>
    <tr>
      <th>3</th>
      <td>d</td>
      <td>7</td>
      <td>130</td>
      <td>17</td>
      <td>3</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>e</td>
      <td>8</td>
      <td>178</td>
      <td>18</td>
      <td>1</td>
      <td>A</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.tail(3)
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
      <th>name</th>
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>class</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>k</td>
      <td>4</td>
      <td>67</td>
      <td>123</td>
      <td>2</td>
      <td>B</td>
    </tr>
    <tr>
      <th>11</th>
      <td>l</td>
      <td>3</td>
      <td>234</td>
      <td>345</td>
      <td>3</td>
      <td>A</td>
    </tr>
    <tr>
      <th>12</th>
      <td>z</td>
      <td>16</td>
      <td>890</td>
      <td>456</td>
      <td>1</td>
      <td>C</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.shape
```




    (13, 6)




```python
data.describe()
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
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>13.000000</td>
      <td>13.000000</td>
      <td>13.000000</td>
      <td>13.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>7.615385</td>
      <td>595.076923</td>
      <td>201.615385</td>
      <td>2.153846</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.810027</td>
      <td>655.313215</td>
      <td>212.987299</td>
      <td>0.987096</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>67.000000</td>
      <td>13.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>5.000000</td>
      <td>150.000000</td>
      <td>17.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>6.000000</td>
      <td>234.000000</td>
      <td>123.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>8.000000</td>
      <td>890.000000</td>
      <td>345.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>23.000000</td>
      <td>2345.000000</td>
      <td>678.000000</td>
      <td>4.000000</td>
    </tr>
  </tbody>
</table>
</div>



짐작 가능하듯, head( )는 앞부분, tail( )은 뒷부분 출력, shape는 행과 열의 개수 출력, describe( )는 요약 통계량을 출력합니다. head( )와 tail( )의 기본값은 5 입니다.
```python

```
