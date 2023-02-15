---
layout: single
title: 지도 시각화(Map Visualization)
categories: Data Analysis
---

![map1](https://user-images.githubusercontent.com/107829554/210232395-3c7833b5-8553-44f6-a74a-9da62bd765dd.jpg)
<br>지도를 그리기 위해, json 파일을 불러왔습니다. 데이터는 서울시의 구역코드, 지역이름, 위도, 경도의 정보를 담고 있습니다.
<br>
<br>
<br> ![map2](https://user-images.githubusercontent.com/107829554/210232662-40ef79a9-0c95-44c4-af2c-09147a140244.jpg)
<br> 간단하게 데이터를 살펴보았습니다.

<br> ![map3](https://user-images.githubusercontent.com/107829554/210232927-63ad1fbf-6c43-4fe5-abd6-09b3f86d6dfe.jpg)
<br> 외국인 데이터 입니다. 서울시의 코드, 지역, 인구정보가 담겨있는 csv 파일 입니다.

<br> ![map4](https://user-images.githubusercontent.com/107829554/210233147-31cfa472-08fe-4018-be98-2766e2c256f0.jpg)
<br> 데이터의 형태를 살펴보았습니다. 지도를 그리는데 code가 int형 입니다.

<br> ![map5](https://user-images.githubusercontent.com/107829554/210233322-f923c416-4a6a-4d53-bce7-1ddf64dbe1ec.jpg)
<br> 편리한 사용을 위해 string 형태로 바꿔주었습니다.

<br> ![map6](https://user-images.githubusercontent.com/107829554/210233492-70876262-5dee-4e4c-96c2-a2718e92fb0d.jpg)
<br> 각 지역을 8개의 단계로 구분 짓고,

<br> ![map7](https://user-images.githubusercontent.com/107829554/210233641-8d0d539a-c12a-4a06-bf13-334f9eedac5e.jpg)
<br> ![map8](https://user-images.githubusercontent.com/107829554/210233782-41150599-3ad5-4648-99ca-fce32bd90612.jpg) 
<br> ![map9](https://user-images.githubusercontent.com/107829554/210233926-391dcfeb-21f9-490a-a7b7-9b2195b53f62.jpg)
<br> 배경 지도를 만든 후에, 외국인 데이터 정보가 담긴 지도가 그렸습니다. 파란색의 농도로 서울시 내부의 인구 밀도를 구분지었고, 여러 설정값이 있는데, 이것은 기호에 맞춰서 변경하면 됩니다.

<br> ![map10](https://user-images.githubusercontent.com/107829554/210234250-84975bae-62f0-49b5-b9c6-63ce8e326c86.jpg)
<br> 부족한 감이 있어서, 지역 경계 정보를 담은 데이터를 불러왔습니다.

<br> ![map11](https://user-images.githubusercontent.com/107829554/210234400-b18bd26e-9121-426a-8b1e-fb19a4983b4f.jpg)
<br> ![image](https://user-images.githubusercontent.com/107829554/210234500-38ca1231-c2ad-456e-bc0a-de13512d1e92.png)
<br> 경계선을 추가해준 그림입니다.
<br>
<br> 이제 마커를 추가하도록 하겠습니다. 마커의 데이터는 서울 열린데이터 광장에서 가져온 장난감 도서관 위치 데이터 입니다.
<br>
<br> ![image](https://user-images.githubusercontent.com/107829554/210234784-4a125cab-2c82-4b62-8d29-a0edb8c80342.png)

<br> ![image](https://user-images.githubusercontent.com/107829554/210234858-4040a590-75f2-4bd9-ba13-748d13a5286b.png)
<br> 지도 그리는데 필요한 데이터만 따로 추출해오고,

<br> ![image](https://user-images.githubusercontent.com/107829554/210234916-5ab1c430-fbf1-419f-8ff1-28c7b0a5076a.png)
<br> 결측치가 존재하는지 확인합니다. 다행히 결측치는 존재하지 않아서, 따로 제거해야하는 번거로움은 없어 보입니다.

<br> ![image](https://user-images.githubusercontent.com/107829554/210235011-bb196b36-e890-454b-89ad-e687d243f25e.png)
<br> 마커를 설정한 후 기존 데이터에 추가해주었습니다.

<br> ![image](https://user-images.githubusercontent.com/107829554/210235117-71b8faf7-3cfd-4f0e-b5c8-1ff8bdec39e5.png)

<br> 후기: 색깔, 테마 등 변경 가능한 설정값들이 무수히 많습니다. 데이터 분석을 이렇게 화려한 시각화를 통해 할 수 있다는 것이 굉장히 흥미 넘칩니다.




