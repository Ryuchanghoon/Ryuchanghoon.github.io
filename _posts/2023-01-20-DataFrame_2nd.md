---
layout: single
title: 데이터 분석 2nd(Data Analysis)
categories: Data-Analysis
---


이번 포스팅은 데이터 분석에 있어서 자주 사용하는 함수를 실습한 코드 입니다. 

저번 포스팅에 이어서 실습한 코드 입니다.



pandas 패키지에는 여러 함수가 존재합니다. 데이터 분석에 있어서 조금 복잡해 보이는 부분이 있어도, pandas 패키지 안에 있는 함수 몇가지를 조합하면, 간단히 해결할 수 있었습니다.

자주 사용하는 pandas 함수를 정리하자면, query( ), assign( ), groupby( ), agg( ), sort_values( ), head( ), tail( ) 등이 있습니다.

query( )함수는 사용할 데이터만 따로 추출하는 것이고, assign( )은 변수 생성, groupby( )는 분리, 구분지어줄 때 사용합니다.

또한 agg( )함수는 agg()함수 안에 또 다른 함수를 조합해서 사용하게 되는데, mean(), sum(), median(), min(), max(), count()를 같이 사용하게 되며, 계산 값을 생성한 변수에 넣어줄 때 사용합니다.

이어서 sort_values( )는 내림차순, 오름차순 정렬할 때 사용하고, head( ), tail( )함수는 전의 포스팅 내용과 동일합니다.

실습을 위해 데이터를 불러오겠습니다. 데이터는 ggplot2 패키지에 들어있는 mpg 데이터 입니다.


```python
import pandas as pd
```


```python
data = pd.read_csv('mpg.csv')
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 11 columns</p>
</div>



위 데이터의 'manufacturer'별로 'compact' 자동차의 연비 평균을 구한 다음, 연비가 높은 차량 5위 까지 출력하는 과정을 거치겠습니다.


```python
data1 = data.query('category == "compact"')
data1
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>5</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>6</th>
      <td>audi</td>
      <td>a4</td>
      <td>3.1</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>18</td>
      <td>27</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>7</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>4</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>8</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>4</td>
      <td>16</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>9</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>4</td>
      <td>20</td>
      <td>28</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>10</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>4</td>
      <td>19</td>
      <td>27</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>11</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>4</td>
      <td>15</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>12</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>4</td>
      <td>17</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>13</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>3.1</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>4</td>
      <td>17</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>14</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>3.1</td>
      <td>2008</td>
      <td>6</td>
      <td>manual(m6)</td>
      <td>4</td>
      <td>15</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>141</th>
      <td>nissan</td>
      <td>altima</td>
      <td>2.4</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>142</th>
      <td>nissan</td>
      <td>altima</td>
      <td>2.4</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>19</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>169</th>
      <td>subaru</td>
      <td>impreza awd</td>
      <td>2.5</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s4)</td>
      <td>4</td>
      <td>20</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>170</th>
      <td>subaru</td>
      <td>impreza awd</td>
      <td>2.5</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s4)</td>
      <td>4</td>
      <td>20</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>171</th>
      <td>subaru</td>
      <td>impreza awd</td>
      <td>2.5</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>4</td>
      <td>19</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>172</th>
      <td>subaru</td>
      <td>impreza awd</td>
      <td>2.5</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>4</td>
      <td>20</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>186</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>2.2</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>21</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>187</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>2.2</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>188</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>2.4</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>31</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>189</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>2.4</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s5)</td>
      <td>f</td>
      <td>22</td>
      <td>31</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>190</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>3.0</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>191</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>3.0</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>192</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>3.3</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s5)</td>
      <td>f</td>
      <td>18</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>193</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l3)</td>
      <td>f</td>
      <td>24</td>
      <td>30</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>194</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>24</td>
      <td>33</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>195</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>26</td>
      <td>35</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>196</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>28</td>
      <td>37</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>197</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>26</td>
      <td>35</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>207</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.0</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>208</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.0</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>19</td>
      <td>26</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>209</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>210</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>22</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>211</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>17</td>
      <td>24</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>212</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>1.9</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>33</td>
      <td>44</td>
      <td>d</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>213</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.0</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>214</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.0</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>19</td>
      <td>26</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>215</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>22</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>216</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>217</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.5</td>
      <td>2008</td>
      <td>5</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>218</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.5</td>
      <td>2008</td>
      <td>5</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>219</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>16</td>
      <td>23</td>
      <td>r</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>220</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>17</td>
      <td>24</td>
      <td>r</td>
      <td>compact</td>
    </tr>
  </tbody>
</table>
</div>



먼저 query() 함수를 사용하면 compact차량만 따로 추출 된 것을 확인 할 수 있습니다.


```python
data2 = data1.assign(total = (data['hwy'] + data['cty']) / 2)
data2
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>23.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>audi</td>
      <td>a4</td>
      <td>3.1</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>18</td>
      <td>27</td>
      <td>p</td>
      <td>compact</td>
      <td>22.5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>4</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>4</td>
      <td>16</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
      <td>20.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>4</td>
      <td>20</td>
      <td>28</td>
      <td>p</td>
      <td>compact</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>4</td>
      <td>19</td>
      <td>27</td>
      <td>p</td>
      <td>compact</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>4</td>
      <td>15</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>4</td>
      <td>17</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>3.1</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>4</td>
      <td>17</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>3.1</td>
      <td>2008</td>
      <td>6</td>
      <td>manual(m6)</td>
      <td>4</td>
      <td>15</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>141</th>
      <td>nissan</td>
      <td>altima</td>
      <td>2.4</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>142</th>
      <td>nissan</td>
      <td>altima</td>
      <td>2.4</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>19</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>169</th>
      <td>subaru</td>
      <td>impreza awd</td>
      <td>2.5</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s4)</td>
      <td>4</td>
      <td>20</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
      <td>22.5</td>
    </tr>
    <tr>
      <th>170</th>
      <td>subaru</td>
      <td>impreza awd</td>
      <td>2.5</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s4)</td>
      <td>4</td>
      <td>20</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
      <td>23.5</td>
    </tr>
    <tr>
      <th>171</th>
      <td>subaru</td>
      <td>impreza awd</td>
      <td>2.5</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>4</td>
      <td>19</td>
      <td>25</td>
      <td>p</td>
      <td>compact</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>172</th>
      <td>subaru</td>
      <td>impreza awd</td>
      <td>2.5</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>4</td>
      <td>20</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
      <td>23.5</td>
    </tr>
    <tr>
      <th>186</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>2.2</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>21</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>187</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>2.2</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>188</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>2.4</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>31</td>
      <td>r</td>
      <td>compact</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>189</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>2.4</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s5)</td>
      <td>f</td>
      <td>22</td>
      <td>31</td>
      <td>r</td>
      <td>compact</td>
      <td>26.5</td>
    </tr>
    <tr>
      <th>190</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>3.0</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>r</td>
      <td>compact</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>191</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>3.0</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>r</td>
      <td>compact</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>192</th>
      <td>toyota</td>
      <td>camry solara</td>
      <td>3.3</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s5)</td>
      <td>f</td>
      <td>18</td>
      <td>27</td>
      <td>r</td>
      <td>compact</td>
      <td>22.5</td>
    </tr>
    <tr>
      <th>193</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l3)</td>
      <td>f</td>
      <td>24</td>
      <td>30</td>
      <td>r</td>
      <td>compact</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>194</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>24</td>
      <td>33</td>
      <td>r</td>
      <td>compact</td>
      <td>28.5</td>
    </tr>
    <tr>
      <th>195</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>26</td>
      <td>35</td>
      <td>r</td>
      <td>compact</td>
      <td>30.5</td>
    </tr>
    <tr>
      <th>196</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>28</td>
      <td>37</td>
      <td>r</td>
      <td>compact</td>
      <td>32.5</td>
    </tr>
    <tr>
      <th>197</th>
      <td>toyota</td>
      <td>corolla</td>
      <td>1.8</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>26</td>
      <td>35</td>
      <td>r</td>
      <td>compact</td>
      <td>30.5</td>
    </tr>
    <tr>
      <th>207</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.0</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>208</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.0</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>19</td>
      <td>26</td>
      <td>r</td>
      <td>compact</td>
      <td>22.5</td>
    </tr>
    <tr>
      <th>209</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>210</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>22</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>211</th>
      <td>volkswagen</td>
      <td>gti</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>17</td>
      <td>24</td>
      <td>r</td>
      <td>compact</td>
      <td>20.5</td>
    </tr>
    <tr>
      <th>212</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>1.9</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>33</td>
      <td>44</td>
      <td>d</td>
      <td>compact</td>
      <td>38.5</td>
    </tr>
    <tr>
      <th>213</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.0</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>214</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.0</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>19</td>
      <td>26</td>
      <td>r</td>
      <td>compact</td>
      <td>22.5</td>
    </tr>
    <tr>
      <th>215</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>22</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>216</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>217</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.5</td>
      <td>2008</td>
      <td>5</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>218</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.5</td>
      <td>2008</td>
      <td>5</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>r</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>219</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>16</td>
      <td>23</td>
      <td>r</td>
      <td>compact</td>
      <td>19.5</td>
    </tr>
    <tr>
      <th>220</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>17</td>
      <td>24</td>
      <td>r</td>
      <td>compact</td>
      <td>20.5</td>
    </tr>
  </tbody>
</table>
</div>



연비 변수를 따로 생성했습니다.


```python
data3 = data2.groupby('manufacturer').agg(mean = ('total', 'mean'))
data3
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
      <th>mean</th>
    </tr>
    <tr>
      <th>manufacturer</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>audi</th>
      <td>22.433333</td>
    </tr>
    <tr>
      <th>nissan</th>
      <td>24.000000</td>
    </tr>
    <tr>
      <th>subaru</th>
      <td>22.875000</td>
    </tr>
    <tr>
      <th>toyota</th>
      <td>26.416667</td>
    </tr>
    <tr>
      <th>volkswagen</th>
      <td>24.642857</td>
    </tr>
  </tbody>
</table>
</div>



manufacturer별로 구분짓고, manufacturer별 연비 평균값을 내주었습니다.


```python
data4 = data3.sort_values('mean', ascending = False)
data4
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
      <th>mean</th>
    </tr>
    <tr>
      <th>manufacturer</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>toyota</th>
      <td>26.416667</td>
    </tr>
    <tr>
      <th>volkswagen</th>
      <td>24.642857</td>
    </tr>
    <tr>
      <th>nissan</th>
      <td>24.000000</td>
    </tr>
    <tr>
      <th>subaru</th>
      <td>22.875000</td>
    </tr>
    <tr>
      <th>audi</th>
      <td>22.433333</td>
    </tr>
  </tbody>
</table>
</div>



상위 값을 추출하기 위해, 먼저 'mean' 기준 내림차순 정렬을 했습니다


```python
data5 = data4.head()
data5
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
      <th>mean</th>
    </tr>
    <tr>
      <th>manufacturer</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>toyota</th>
      <td>26.416667</td>
    </tr>
    <tr>
      <th>volkswagen</th>
      <td>24.642857</td>
    </tr>
    <tr>
      <th>nissan</th>
      <td>24.000000</td>
    </tr>
    <tr>
      <th>subaru</th>
      <td>22.875000</td>
    </tr>
    <tr>
      <th>audi</th>
      <td>22.433333</td>
    </tr>
  </tbody>
</table>
</div>



이제 마지막 과정인 제조사별 compact차량 상위 5개 연비를 구했습니다.

하지만 이 모든 과정은 하나의 코드로 추출 가능합니다.


```python
data.query('category == "compact"')\
     .assign(total = (data['hwy'] + data['cty']) / 2)\
     .groupby('manufacturer').agg(mean = ('total', 'mean'))\
        .sort_values('mean', ascending = False)\
        .head()
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
      <th>mean</th>
    </tr>
    <tr>
      <th>manufacturer</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>toyota</th>
      <td>26.416667</td>
    </tr>
    <tr>
      <th>volkswagen</th>
      <td>24.642857</td>
    </tr>
    <tr>
      <th>nissan</th>
      <td>24.000000</td>
    </tr>
    <tr>
      <th>subaru</th>
      <td>22.875000</td>
    </tr>
    <tr>
      <th>audi</th>
      <td>22.433333</td>
    </tr>
  </tbody>
</table>
</div>



이와 같이 동일한 결과가 나오게 됩니다.

후기: 한 코드당 한 함수 쓰는 것은 참 쉽지만, 한 코드에 함수 다 몰아 쓰는건 아직도 어려운 듯 합니다. 손과 머리에 익숙해질 때 까지 반복 숙달 해야겠습니다.
