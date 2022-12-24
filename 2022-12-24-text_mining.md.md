 텍스트 마이닝(Text Mining)

문자 데이터를 활용해서, 필요한 정보를 얻어내는 분석을 텍스트 마이닝(Text Mining)이라고 합니다. 단어의 빈도를 한눈에 파악 할 때 굉장히 유용한 기법입니다.

텍스트 마이닝 기법을 사용하기 위해서, 먼저 패키지를 설치해야 합니다


```python
! pip install jpype1
```

    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Requirement already satisfied: jpype1 in /usr/local/lib/python3.8/dist-packages (1.4.1)
    Requirement already satisfied: packaging in /usr/local/lib/python3.8/dist-packages (from jpype1) (21.3)
    Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /usr/local/lib/python3.8/dist-packages (from packaging->jpype1) (3.0.9)



```python
! pip install konlpy
```

    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Requirement already satisfied: konlpy in /usr/local/lib/python3.8/dist-packages (0.6.0)
    Requirement already satisfied: JPype1>=0.7.0 in /usr/local/lib/python3.8/dist-packages (from konlpy) (1.4.1)
    Requirement already satisfied: numpy>=1.6 in /usr/local/lib/python3.8/dist-packages (from konlpy) (1.21.6)
    Requirement already satisfied: lxml>=4.1.0 in /usr/local/lib/python3.8/dist-packages (from konlpy) (4.9.2)
    Requirement already satisfied: packaging in /usr/local/lib/python3.8/dist-packages (from JPype1>=0.7.0->konlpy) (21.3)
    Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /usr/local/lib/python3.8/dist-packages (from packaging->JPype1>=0.7.0->konlpy) (3.0.9)


패키지 설치를 완료하면, Text Mining을 할 준비가 완료됩니다.


```python
data = open('/content/drive/MyDrive/dj.txt.txt', encoding = 'UTF-8').read()
data
```




    '존경하는 내외 국민 여러분!\n \n다시 한번 여러분의 축하에 감사드립니다. 특히 외국에서 오신 귀빈 여러분께서는 공사간 매우 다망하신데도 불구하고, 이렇게 먼 길 오셔서 축하해 주시니 무어라 감사의 말씀을 드려야 할지 모르겠습니다.\n\n여러분께서는 이 나라에서 50년 만에 여야 간의 평화적 정권교체가 이루어진 데 대해 민주주의의 큰 승리로 생각하고, 축하하고 격려하기 위해 오신 것으로 믿습니다. 또한 여러분께서는 우리가 지금 금융과 외환위기에 처해서 이를 극복하고자 국민과 정부가 하나가 되어 힘쓰고 있는 데 대해, 격려와 성원을 아끼지 않는 심정에서 오신 것으로 믿고 있습니다. 우리는 민주주의와 시장경제를 같이 발전시켜서 여러분 나라에서와 같이 훌륭한 성공을 거둠으로써 여러분의 성원에 보답할 것을 굳게 다짐하고자 합니다.\n\n저는 오랜 군사통치와 권위주의 정치 아래에서 수많은 박해를 받았습니다. 다섯 번에 걸쳐 죽음의 고비를 맞아야 했고, 6년간 감옥살이를 했으며, 10년을 망명과 연금생활 속에 살아야만 했습니다. 그러나 저는 이러한 고통스러운 생활 속에서도 민주주의와 정의는 필승한다는 사실을 한 번도 의심해 본 일이 없습니다. 설사 제 당대에서는 성공하지 못하더라도, 국민의 마음과 역사 속에서 저를 박해한 그들은 반드시 패자가 되고 저는 승자가 될 것이라는 점을 확신해 마지않았습니다. 그런데 저는 살아서 승리의 영광을 차재하게 된 것입니다. 얼마나 감사한 일이겠습니까.\n\n그러나 저를 시험하는 힘든 과정은 결코 끝나지 않았습니다. 대통령에 당선된 그날부터 외환위기의 극복과 IMF와의 힘겨운 협력체제 확립에 몰두하지 않을 수 없었습니다. 우리는 너무도 심각하고 너무도 긴박한 상황 속에 놓여 있습니다. 저는 취임 전인 지난 2개월간 실질적인 대통령 역할을 하지 않으면 안되었습니다. 다행히 국가적인 파국은 일단 모면했습니다. 그러나 위기는 아직도 계속되고 있습니다. 우리는 이 위기를 극복하기 위해 앞으로도 최선을 다하고, IMF와의 협약을 충실히 지켜 나갈 것입니다. 여러분의 계속된 성원을 바라 마지않습니다.\n\n저는 오늘의 난국을, 어렵지만 반드시 해결해 나가겠습니다. 무엇보다 시장경제 원리에 입각한 과감한 경제개혁을 관철시키겠습니다. 이 개혁은 노사정 3자의 고통 분담과 공동의 노력을 통해 이루어질 수 있습니다. 그리고 무엇보다 국민의 땀과 눈물이 요구되고 있습니다. 우리 국민이 나라를 살리기 위해 적극 협력할 것임을 굳게 믿습니다.\n\n또한 이 난국을 극복하기 위해서는 세계 각국과 관계 국제기관의 협력이 절실히 필요합니다. 하늘은 스스로 돕는 자를 돕는다고 했습니다. 우리가 모든 희생을 무릅쓰고 위기극복에 노력한다면, 세계의 친구들도 지원을 아끼지 않을 것을 믿어 의심치 않습니다.\n\n우리는 결코 일방적으로 세계의 지원에 의존하지는 않을 것입니다. WTO체제가 요구하는 개방과 협력의 자세를 견지할 것입니다. 교역과 투자에 있어서 가장 믿음직하고 이득을 줄수 있는 파트너가 되도록 힘쓰겠습니다. 우리는 세계로 나아가고 세계는 우리에게 진출하는, 그러한 상호협력의 시대를 열고자 합니다.\n\n한반도 평화는 우리의 지상과제입니다. 우리는 확고한 안보체제 위에 남북한 평화를 실현하고 가능한 교류, 협력을 증진시켜 남북이 서로 공존하고 공영하는 내일을 열어 나가겠습니다. 그리하여 7,000만 우리 민족이 전쟁의 두려움 없이 서로 왕래하고 협력하는 그러한 내일을 하루속히 실현하고자 합니다. 이것이야말로 민족의 완전한 통일을 위한 지름길이라 생각합니다.\n\n저는 우리 국민의 애국심을 믿습니다. 그들의 능력을 믿습니다. 높은 교육수준과 문화적 전통을 가진 우리 민족을 자랑스럽게 생각합니다. 역사가 증명하듯 우리는 이웃 나라와 선린우호에 힘써 왔으며 문화적 교류, 협력을 통해 서로를 살찌게 해 왔습니다. 이제 세계 각국과의 문화교류를 통해 문화한국의 내일을 크게 개척해 나가고자 합니다. 여러분의 나라와 더 많은 교류, 협력이 이루어질 수 있도록 도와주시기 바랍니다. 한국에 계시는 동안 즐거운 시간이 되시길 바랍니다.\n\n내외 국민 여러분!\n\n다시 한번 깊은 감사를 드립니다.\n'



먼저 텍스트 데이터를 불러왔습니다. 데이터는 김대중 전 대통령의 연설문 입니다. 불필요한 문자가 보이는 것을 알 수 있습니다.


```python
import re
data = re.sub('[^가-힣]',' ', data)
data
```




    '존경하는 내외 국민 여러분    다시 한번 여러분의 축하에 감사드립니다  특히 외국에서 오신 귀빈 여러분께서는 공사간 매우 다망하신데도 불구하고  이렇게 먼 길 오셔서 축하해 주시니 무어라 감사의 말씀을 드려야 할지 모르겠습니다   여러분께서는 이 나라에서   년 만에 여야 간의 평화적 정권교체가 이루어진 데 대해 민주주의의 큰 승리로 생각하고  축하하고 격려하기 위해 오신 것으로 믿습니다  또한 여러분께서는 우리가 지금 금융과 외환위기에 처해서 이를 극복하고자 국민과 정부가 하나가 되어 힘쓰고 있는 데 대해  격려와 성원을 아끼지 않는 심정에서 오신 것으로 믿고 있습니다  우리는 민주주의와 시장경제를 같이 발전시켜서 여러분 나라에서와 같이 훌륭한 성공을 거둠으로써 여러분의 성원에 보답할 것을 굳게 다짐하고자 합니다   저는 오랜 군사통치와 권위주의 정치 아래에서 수많은 박해를 받았습니다  다섯 번에 걸쳐 죽음의 고비를 맞아야 했고   년간 감옥살이를 했으며    년을 망명과 연금생활 속에 살아야만 했습니다  그러나 저는 이러한 고통스러운 생활 속에서도 민주주의와 정의는 필승한다는 사실을 한 번도 의심해 본 일이 없습니다  설사 제 당대에서는 성공하지 못하더라도  국민의 마음과 역사 속에서 저를 박해한 그들은 반드시 패자가 되고 저는 승자가 될 것이라는 점을 확신해 마지않았습니다  그런데 저는 살아서 승리의 영광을 차재하게 된 것입니다  얼마나 감사한 일이겠습니까   그러나 저를 시험하는 힘든 과정은 결코 끝나지 않았습니다  대통령에 당선된 그날부터 외환위기의 극복과    와의 힘겨운 협력체제 확립에 몰두하지 않을 수 없었습니다  우리는 너무도 심각하고 너무도 긴박한 상황 속에 놓여 있습니다  저는 취임 전인 지난  개월간 실질적인 대통령 역할을 하지 않으면 안되었습니다  다행히 국가적인 파국은 일단 모면했습니다  그러나 위기는 아직도 계속되고 있습니다  우리는 이 위기를 극복하기 위해 앞으로도 최선을 다하고     와의 협약을 충실히 지켜 나갈 것입니다  여러분의 계속된 성원을 바라 마지않습니다   저는 오늘의 난국을  어렵지만 반드시 해결해 나가겠습니다  무엇보다 시장경제 원리에 입각한 과감한 경제개혁을 관철시키겠습니다  이 개혁은 노사정  자의 고통 분담과 공동의 노력을 통해 이루어질 수 있습니다  그리고 무엇보다 국민의 땀과 눈물이 요구되고 있습니다  우리 국민이 나라를 살리기 위해 적극 협력할 것임을 굳게 믿습니다   또한 이 난국을 극복하기 위해서는 세계 각국과 관계 국제기관의 협력이 절실히 필요합니다  하늘은 스스로 돕는 자를 돕는다고 했습니다  우리가 모든 희생을 무릅쓰고 위기극복에 노력한다면  세계의 친구들도 지원을 아끼지 않을 것을 믿어 의심치 않습니다   우리는 결코 일방적으로 세계의 지원에 의존하지는 않을 것입니다     체제가 요구하는 개방과 협력의 자세를 견지할 것입니다  교역과 투자에 있어서 가장 믿음직하고 이득을 줄수 있는 파트너가 되도록 힘쓰겠습니다  우리는 세계로 나아가고 세계는 우리에게 진출하는  그러한 상호협력의 시대를 열고자 합니다   한반도 평화는 우리의 지상과제입니다  우리는 확고한 안보체제 위에 남북한 평화를 실현하고 가능한 교류  협력을 증진시켜 남북이 서로 공존하고 공영하는 내일을 열어 나가겠습니다  그리하여      만 우리 민족이 전쟁의 두려움 없이 서로 왕래하고 협력하는 그러한 내일을 하루속히 실현하고자 합니다  이것이야말로 민족의 완전한 통일을 위한 지름길이라 생각합니다   저는 우리 국민의 애국심을 믿습니다  그들의 능력을 믿습니다  높은 교육수준과 문화적 전통을 가진 우리 민족을 자랑스럽게 생각합니다  역사가 증명하듯 우리는 이웃 나라와 선린우호에 힘써 왔으며 문화적 교류  협력을 통해 서로를 살찌게 해 왔습니다  이제 세계 각국과의 문화교류를 통해 문화한국의 내일을 크게 개척해 나가고자 합니다  여러분의 나라와 더 많은 교류  협력이 이루어질 수 있도록 도와주시기 바랍니다  한국에 계시는 동안 즐거운 시간이 되시길 바랍니다   내외 국민 여러분   다시 한번 깊은 감사를 드립니다  '



re 패키지를 import 해서 한글이 아닌 데이터를 제거해 주었습니다.


```python
!pip install konlpy
```

    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Requirement already satisfied: konlpy in /usr/local/lib/python3.8/dist-packages (0.6.0)
    Requirement already satisfied: lxml>=4.1.0 in /usr/local/lib/python3.8/dist-packages (from konlpy) (4.9.2)
    Requirement already satisfied: JPype1>=0.7.0 in /usr/local/lib/python3.8/dist-packages (from konlpy) (1.4.1)
    Requirement already satisfied: numpy>=1.6 in /usr/local/lib/python3.8/dist-packages (from konlpy) (1.21.6)
    Requirement already satisfied: packaging in /usr/local/lib/python3.8/dist-packages (from JPype1>=0.7.0->konlpy) (21.3)
    Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /usr/local/lib/python3.8/dist-packages (from packaging->JPype1>=0.7.0->konlpy) (3.0.9)



```python
import konlpy
hannanum = konlpy.tag.Hannanum()

nouns = hannanum.nouns(data)
nouns
```




    ['존경',
     '내외',
     '국민',
     '여러분',
     '한번',
     '여러분',
     '축하',
     '외국',
     '귀빈',
     '여러분',
     '공사간',
     '다망',
     '불구',
     '길',
     '축하',
     '무어',
     '감사',
     '말씀',
     '여러분',
     '나라',
     '년',
     '만',
     '여',
     '간',
     '평화적',
     '정권교체',
     '데',
     '민주주의',
     '승리',
     '생각',
     '축하',
     '격려',
     '것',
     '여러분',
     '우리',
     '금융',
     '외환위',
     '이',
     '극복',
     '국민',
     '정부',
     '하나',
     '데',
     '격려',
     '성원',
     '심정',
     '것',
     '우리',
     '민주주의',
     '시장경제',
     '발전',
     '여러분',
     '나라',
     '훌륭',
     '성공',
     '여러분',
     '성원',
     '보답',
     '것',
     '다짐',
     '저',
     '군사통치',
     '권위주의',
     '정치',
     '아래',
     '박해',
     '다섯',
     '번',
     '죽음',
     '고비',
     '년',
     '감옥살이',
     '년',
     '망명',
     '연금생활',
     '속',
     '저',
     '고통',
     '생활',
     '속',
     '민주주의',
     '정의',
     '필승',
     '사실',
     '번',
     '의심',
     '일',
     '저',
     '당대',
     '성공',
     '국민',
     '마음',
     '역사',
     '속',
     '저',
     '그',
     '패자',
     '저',
     '승자',
     '것',
     '점',
     '확신',
     '저',
     '승리',
     '영광',
     '차재하',
     '것',
     '감사',
     '일',
     '저',
     '시험',
     '과정',
     '대통령',
     '당선',
     '그날',
     '외환위기',
     '극복',
     '와',
     '협력체제',
     '확립',
     '몰두',
     '수',
     '우리',
     '심각',
     '긴박',
     '상황',
     '속',
     '저',
     '취',
     '전',
     '개월',
     '실질적',
     '대통령',
     '역할',
     '국가적',
     '파국',
     '모면',
     '위기',
     '계속',
     '우리',
     '위',
     '극복',
     '앞',
     '최선',
     '와',
     '협약',
     '것',
     '여러분',
     '계속',
     '성원',
     '저',
     '오늘',
     '난국',
     '해결',
     '무엇',
     '시장경제',
     '원리',
     '입각',
     '과감',
     '경제개혁',
     '관철',
     '개혁',
     '노사정',
     '자',
     '고통',
     '분담',
     '공동',
     '노력',
     '수',
     '무엇',
     '국민',
     '땀',
     '눈물',
     '요구',
     '우리',
     '국민',
     '나라',
     '리',
     '적극',
     '협력',
     '것',
     '난국',
     '극복',
     '세계',
     '각국',
     '관계',
     '국제기관',
     '협력',
     '필요',
     '하늘',
     '자',
     '우리',
     '희생',
     '위기극복',
     '노력',
     '세계',
     '친구들',
     '지원',
     '것',
     '의심치',
     '우리',
     '일방적',
     '세계',
     '지원',
     '의존',
     '것',
     '체제',
     '요구',
     '개방',
     '협력',
     '자세',
     '견지',
     '것',
     '교역',
     '투자',
     '이득',
     '수',
     '파트너',
     '우리',
     '세계',
     '세계',
     '우리',
     '진출',
     '상호협력',
     '시대',
     '한반',
     '평화',
     '우리',
     '지상과제',
     '우리',
     '확고',
     '안보체제',
     '위',
     '남북한',
     '평화',
     '실현',
     '가능',
     '교류',
     '협력',
     '증진',
     '남북',
     '공존',
     '공영',
     '내일',
     '우리',
     '민족',
     '전쟁',
     '두려움',
     '왕래',
     '협력',
     '내일',
     '실현',
     '이것',
     '민족',
     '완전',
     '통일',
     '지름길',
     '생각',
     '저',
     '우리',
     '국민',
     '애국심',
     '그',
     '능력',
     '교육수준',
     '문화적',
     '전통',
     '우리',
     '민족',
     '자랑',
     '생각',
     '역사',
     '증명',
     '우리',
     '이웃',
     '나라',
     '선린우호',
     '문화적',
     '교류',
     '협력',
     '서로',
     '세계',
     '각국',
     '문화교류',
     '문화한국의',
     '내일',
     '개척',
     '여러분',
     '나라',
     '교류',
     '협력',
     '수',
     '한국',
     '동안',
     '시간',
     '되시길',
     '내외',
     '국민',
     '여러분',
     '한번',
     '감사',
     '드']



텍스트에서 명사 추출을 위해, konlpy.tag.Hannanum()의 nouns()를 이용했습니다.

위와 같이 명사만 추출된 것을 볼 수 있습니다.


```python
import pandas as pd
word = pd.DataFrame({'word' : nouns})
word
```





  <div id="df-c0794545-6a28-4fad-bcd6-3dca3cf6d115">
    <div class="colab-df-container">
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
      <th>word</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>존경</td>
    </tr>
    <tr>
      <th>1</th>
      <td>내외</td>
    </tr>
    <tr>
      <th>2</th>
      <td>국민</td>
    </tr>
    <tr>
      <th>3</th>
      <td>여러분</td>
    </tr>
    <tr>
      <th>4</th>
      <td>한번</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>297</th>
      <td>국민</td>
    </tr>
    <tr>
      <th>298</th>
      <td>여러분</td>
    </tr>
    <tr>
      <th>299</th>
      <td>한번</td>
    </tr>
    <tr>
      <th>300</th>
      <td>감사</td>
    </tr>
    <tr>
      <th>301</th>
      <td>드</td>
    </tr>
  </tbody>
</table>
<p>302 rows × 1 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-c0794545-6a28-4fad-bcd6-3dca3cf6d115')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-c0794545-6a28-4fad-bcd6-3dca3cf6d115 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c0794545-6a28-4fad-bcd6-3dca3cf6d115');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
word['count'] = word['word'].str.len()
word
```





  <div id="df-5e15eb90-ea8e-47db-9b9e-b39f80bc30b2">
    <div class="colab-df-container">
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
      <th>word</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>존경</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>내외</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>국민</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>여러분</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>한번</td>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>297</th>
      <td>국민</td>
      <td>2</td>
    </tr>
    <tr>
      <th>298</th>
      <td>여러분</td>
      <td>3</td>
    </tr>
    <tr>
      <th>299</th>
      <td>한번</td>
      <td>2</td>
    </tr>
    <tr>
      <th>300</th>
      <td>감사</td>
      <td>2</td>
    </tr>
    <tr>
      <th>301</th>
      <td>드</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>302 rows × 2 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-5e15eb90-ea8e-47db-9b9e-b39f80bc30b2')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-5e15eb90-ea8e-47db-9b9e-b39f80bc30b2 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-5e15eb90-ea8e-47db-9b9e-b39f80bc30b2');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
word = word.query('count >= 2' and 'count < 4')
word = word.sort_values('count', ascending = True)
word
```





  <div id="df-44010bd1-5715-403a-b748-bbc0d25227ec">
    <div class="colab-df-container">
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
      <th>word</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>150</th>
      <td>저</td>
      <td>1</td>
    </tr>
    <tr>
      <th>109</th>
      <td>저</td>
      <td>1</td>
    </tr>
    <tr>
      <th>108</th>
      <td>일</td>
      <td>1</td>
    </tr>
    <tr>
      <th>106</th>
      <td>것</td>
      <td>1</td>
    </tr>
    <tr>
      <th>102</th>
      <td>저</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>134</th>
      <td>국가적</td>
      <td>3</td>
    </tr>
    <tr>
      <th>277</th>
      <td>문화적</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>여러분</td>
      <td>3</td>
    </tr>
    <tr>
      <th>147</th>
      <td>여러분</td>
      <td>3</td>
    </tr>
    <tr>
      <th>51</th>
      <td>여러분</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
<p>280 rows × 2 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-44010bd1-5715-403a-b748-bbc0d25227ec')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-44010bd1-5715-403a-b748-bbc0d25227ec button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-44010bd1-5715-403a-b748-bbc0d25227ec');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




편리하게 사용하기 위해서 데이터 프레임 형태로 변환 후, 글자 수 2~4개 까지의 단어만 남긴 후 다 날렸습니다. 
query()로 count 2개에서 4개 사이 추출. sort_values()로 오름차순 정렬.


```python
word = word.groupby('word', as_index = False).agg(n = ('word', 'count')).sort_values('n', ascending = False).head(20)
word
```





  <div id="df-9dee5d0e-abc8-4c92-9ad4-9eab8dc9a5a3">
    <div class="colab-df-container">
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
      <th>word</th>
      <th>n</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>107</th>
      <td>우리</td>
      <td>15</td>
    </tr>
    <tr>
      <th>96</th>
      <td>여러분</td>
      <td>10</td>
    </tr>
    <tr>
      <th>124</th>
      <td>저</td>
      <td>10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>것</td>
      <td>10</td>
    </tr>
    <tr>
      <th>25</th>
      <td>국민</td>
      <td>7</td>
    </tr>
    <tr>
      <th>161</th>
      <td>협력</td>
      <td>7</td>
    </tr>
    <tr>
      <th>80</th>
      <td>세계</td>
      <td>6</td>
    </tr>
    <tr>
      <th>33</th>
      <td>나라</td>
      <td>5</td>
    </tr>
    <tr>
      <th>29</th>
      <td>극복</td>
      <td>4</td>
    </tr>
    <tr>
      <th>81</th>
      <td>속</td>
      <td>4</td>
    </tr>
    <tr>
      <th>82</th>
      <td>수</td>
      <td>4</td>
    </tr>
    <tr>
      <th>22</th>
      <td>교류</td>
      <td>3</td>
    </tr>
    <tr>
      <th>143</th>
      <td>축하</td>
      <td>3</td>
    </tr>
    <tr>
      <th>79</th>
      <td>성원</td>
      <td>3</td>
    </tr>
    <tr>
      <th>75</th>
      <td>생각</td>
      <td>3</td>
    </tr>
    <tr>
      <th>39</th>
      <td>년</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>감사</td>
      <td>3</td>
    </tr>
    <tr>
      <th>38</th>
      <td>내일</td>
      <td>3</td>
    </tr>
    <tr>
      <th>66</th>
      <td>민족</td>
      <td>3</td>
    </tr>
    <tr>
      <th>65</th>
      <td>문화적</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-9dee5d0e-abc8-4c92-9ad4-9eab8dc9a5a3')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-9dee5d0e-abc8-4c92-9ad4-9eab8dc9a5a3 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-9dee5d0e-abc8-4c92-9ad4-9eab8dc9a5a3');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




head로 글자빈도 상위 15개만 따로 추출했습니다.


```python
!sudo apt-get install -y fonts-nanum

!sudo fc-cache -fv

!rm ~/.cache/matplotlib -rf
```

    Reading package lists... Done
    Building dependency tree       
    Reading state information... Done
    fonts-nanum is already the newest version (20170925-1).
    The following package was automatically installed and is no longer required:
      libnvidia-common-460
    Use 'sudo apt autoremove' to remove it.
    0 upgraded, 0 newly installed, 0 to remove and 20 not upgraded.
    /usr/share/fonts: caching, new cache contents: 0 fonts, 1 dirs
    /usr/share/fonts/truetype: caching, new cache contents: 0 fonts, 3 dirs
    /usr/share/fonts/truetype/humor-sans: caching, new cache contents: 1 fonts, 0 dirs
    /usr/share/fonts/truetype/liberation: caching, new cache contents: 16 fonts, 0 dirs
    /usr/share/fonts/truetype/nanum: caching, new cache contents: 10 fonts, 0 dirs
    /usr/local/share/fonts: caching, new cache contents: 0 fonts, 0 dirs
    /root/.local/share/fonts: skipping, no such directory
    /root/.fonts: skipping, no such directory
    /var/cache/fontconfig: cleaning cache directory
    /root/.cache/fontconfig: not cleaning non-existent cache directory
    /root/.fontconfig: not cleaning non-existent cache directory
    fc-cache: succeeded


Colab 환경에서 그래프 불러올때, 한글이 깨지는 현상이 나타납니다.
위와 같이 폰트 설치를 해주어야, 한글 깨짐 현상을 해결 할 수 있습니다.
설치 후, 런타임 재시작 했습니다.


```python
import matplotlib.pyplot as plt

plt.rcParams['font.family'] = 'NanumBarunGothic' 
```


```python
plt.rcParams.update({'font.family': 'NanumBarunGothic',
                     'figure.dpi' : '120',
                     'figure.figsize':[6.5,6]})
```


```python
import seaborn as sns
sns.barplot(data = word, y = 'word', x = 'n')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f0af9b61d00>




![png](Text_Minin_files/Text_Minin_24_1.png)


추출해준 단어 빈도수를 그래프로 나타낸 겁니다. 빈도 수 상위 15개의 단어가 잘 나온것을 알 수 있습니다.

이제 설정한 단어로 워드 클라우드를 만들겠습니다.


```python
!pip install wordcloud
```

    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Requirement already satisfied: wordcloud in /usr/local/lib/python3.8/dist-packages (1.8.2.2)
    Requirement already satisfied: pillow in /usr/local/lib/python3.8/dist-packages (from wordcloud) (7.1.2)
    Requirement already satisfied: matplotlib in /usr/local/lib/python3.8/dist-packages (from wordcloud) (3.2.2)
    Requirement already satisfied: numpy>=1.6.1 in /usr/local/lib/python3.8/dist-packages (from wordcloud) (1.21.6)
    Requirement already satisfied: python-dateutil>=2.1 in /usr/local/lib/python3.8/dist-packages (from matplotlib->wordcloud) (2.8.2)
    Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in /usr/local/lib/python3.8/dist-packages (from matplotlib->wordcloud) (3.0.9)
    Requirement already satisfied: cycler>=0.10 in /usr/local/lib/python3.8/dist-packages (from matplotlib->wordcloud) (0.11.0)
    Requirement already satisfied: kiwisolver>=1.0.1 in /usr/local/lib/python3.8/dist-packages (from matplotlib->wordcloud) (1.4.4)
    Requirement already satisfied: six>=1.5 in /usr/local/lib/python3.8/dist-packages (from python-dateutil>=2.1->matplotlib->wordcloud) (1.15.0)



```python
dic_word = word.set_index('word').to_dict()['n']
dic_word
```




    {'우리': 15,
     '여러분': 10,
     '저': 10,
     '것': 10,
     '국민': 7,
     '협력': 7,
     '세계': 6,
     '나라': 5,
     '극복': 4,
     '속': 4,
     '수': 4,
     '교류': 3,
     '축하': 3,
     '성원': 3,
     '생각': 3,
     '년': 3,
     '감사': 3,
     '내일': 3,
     '민족': 3,
     '문화적': 2}



워드 클라우드를 만들기 위해서, 데이터 프레임을 딕셔너리 형태로 만들었습니다.


```python
font = '/content/drive/MyDrive/Doit_Python-main/Data/DoHyeon-Regular.ttf'
```


```python
from wordcloud import WordCloud
wc = WordCloud(random_state = 1234,
               font_path = font,
               width = 400,
               height = 400,
               background_color = 'white')
```

background_color를 'white'로 설정 했습니다.
위에 설정값은 원하는 값을 설정해주면 됩니다.


```python
img_wordcloud = wc.generate_from_frequencies(dic_word)

plt.figure(figsize = (5,5))
plt.axis('off')
plt.imshow(img_wordcloud)
```




    <matplotlib.image.AxesImage at 0x7f0af8d37520>




![png](Text_Minin_files/Text_Minin_33_1.png)


후기: 모듈을 불러오기 위해서, 초기에 다운 받아줘야 하는것이 많았습니다. 어려운 것은 아니었지만, 라이브러리를 불러오고, 원하는 데이터를 추출해오고, 그간 공부했던 것을 복습하는데 도움이 되었습니다.

