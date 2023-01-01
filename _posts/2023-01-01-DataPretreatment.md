---
layout: single
title: 데이터 전처리(Data Pretreatment)
---

<br> 특정 데이터로 분석을 할 때, 정리가 잘 되어 있는 데이터를 받아와서 활용할 수 있으나, 현실은 그렇지 않은 경우가 많습니다.
<br> 실무 데이터는 정리가 잘 되어있지 않으며, 오류 또한 포함하고 있는 경우가 많습니다. 이러한 값을 결측치(Missing Value)라고 합니다.
<br>
<br> 위와 같은 결측치(Missing Value)를 가지고 있는 데이터로 분석을 하게 되면, 결과가 왜곡되는 문제가 발생합니다.
<br> 
<br> 이러한 문제를 방지하기 위해 사전 처리 작업을 하게 되는데, 이러한 작업을 데이터 전처리(Data Pretreatment)라고 합니다.

<br> 데이터 전처리(Data Pretreatment) 작업은, 크게 2단계를 거치게 됩니다.

<br> 첫번째 단계는 pd.isna().sum()을 사용해서, 결측치(Missing Value)가 존재하는지 확인합니다.
<br> 두번째 단계는 dropna()를 사용해서 결측치(Missing Value) 값을 제거해 줍니다.

<br> 다음은 데이터 분석 전, 데이터 전처리(Data Pretreatment) 과정을 거치는 코드 입니다.


```python
import pandas as pd
import numpy as np
```

필요한 모듈을 import 해줍니다.


```python
data = pd.DataFrame({'sex' : ['F', 'M', 'F', np.nan, 'M', 'F', 'M'],
                     'score' : [5, 4, np.nan, 3, 4, np.nan, 5]})
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
      <th>sex</th>
      <th>score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>F</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>F</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>F</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



실습을 위해, 간단한 DataFrame을 만들었습니다.


```python
data[['score']] + 1
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
      <th>score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6.0</td>
    </tr>
  </tbody>
</table>
</div>



위와같이 결측치(NaN)는 연산자가 먹히지 않습니다.


```python
pd.isna(data)
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
      <th>sex</th>
      <th>score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



data에 결측치가 존재하는지 True, False 형태로 나타납니다.


```python
pd.isna(data).sum()
```




    sex      1
    score    2
    dtype: int64



하지만 방대한 양의 데이터라면, 위와같이 True, False 형태로 모든것을 직접 확인하는 것은 불가능하기 때문에, sum()함수를 통해 NaN값을 확인합니다.


```python
data = data.dropna(subset = ['sex','score'])
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
      <th>sex</th>
      <th>score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>F</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



결측치(Nan)값 제거 후의 데이터 입니다.


```python
pd.isna(data).sum()
```




    sex      0
    score    0
    dtype: int64



실제로 결측치(NaN)값이 사라진 것을 알 수 있습니다.


```python
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
      <th>sex</th>
      <th>score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>F</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



결측치 값이 사라지는 것은 맞지만, 위와같이 3행과 5행의 값이 전부 사라지게 되었습니다. 필요한 데이터까지 전부 사라지게 할 수 있기 때문에, 철저하게 데이터를 분석한 다음, 결측치를 제거하는 것이 바람직합니다.

후기: 데이터 전처리 과정은 정말 중요한 과정입니다. 어떠한 데이터든, 전처리 과정을 거친 다음에 분석 하는것이 습관화될 필요가 있습니다.
