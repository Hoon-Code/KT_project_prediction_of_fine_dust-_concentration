# 미세먼지 농도 예측 모델 
---
## ✔️프로젝트 개요
- 주제 : 공공데이터를 활용한 미세먼지 농도 예측
- 데이터 출처

  > 미세먼지 : <https://www.airkorea.or.kr/web/pastSearch?pMENU_NO=123>

  > 날씨데이터 : <https://data.kma.go.kr/data/grnd/selectAsosRltmList.do?pgmNo=36>
- 중점사항 : 시계열 데이터 전처리, 단변량/이변량 분석/ ML 모델링
- 프로젝트 목표 : 데이터를 전처리 후 머신러닝 모델 완성해 미세먼지 농도 데이터에 대해 예측, 평가
![image](https://github.com/user-attachments/assets/ce9d8fa5-81b2-45f2-b796-e9d110b8de85)

---

## ✔️도메인 이해
![image](https://github.com/user-attachments/assets/ff0f13db-95fe-41cc-bb1d-6d3ec42ef98f)
![image](https://github.com/user-attachments/assets/2b5a41d0-e831-4e57-956a-ead7e6c1848c)

## ✔️사례 
![image](https://github.com/user-attachments/assets/21f60bb2-34cd-450e-8c14-ba0a134e1ef4)
![image](https://github.com/user-attachments/assets/e1aa7f95-9533-46c3-919c-37fddf477252)
---
## ✔️데이터 소개 
![image](https://github.com/user-attachments/assets/073a62a5-1fd3-4334-9367-c288671f0856)
![image](https://github.com/user-attachments/assets/1fe49261-280b-42e0-a1bf-dda6a03dcc3e)
---

## ✔️데이터 분석 및 전처리 
![image](https://github.com/user-attachments/assets/d705cf2b-2de9-4270-9be7-be3e81284f85)
- QC 플래그 : 대부분의 값이 NaN값이고 결측치가 아닌 값들도 결측을 의미하는 9에 해당하므로  QC플래그 변수들은 모두 drop 처리
- 강수량, 강설 : 결측값들은 비 또는 눈이 오지 않은 날일 것이라고 예상, 0으로 대체
- 온도 : 시간 단위로 나뉘어지는 결과의 결측치값들을 앞에 값으로 대체하여 분석
- 이 외의 결측값들은 시계열 데이터임을 고려해서 선형보간을 이용하여 처리
- t - 24, t + 1시점 :충분히 많은 데이터가 있다고 판단하여, 시작 부분 24개의 데이터 행과 끝 부분 1개의 데이터 행을 삭제하여 결측치를 제거

---
### **풍향**
  
![image](https://github.com/user-attachments/assets/e7dd7f92-c7dc-491e-96b2-8edd52384075)
- 북쪽을 기준으로 90(동), 180(남), 270(서), 360(북) 을 나타냄
- 가장 자주 바람이 부는 곳은 서쪽으로, 중국 쪽에서 부는 것으로 예상됨
- 편서풍이 자주 부는 봄 철에 미세먼지 농도가 높을 것이라 추정
---

## ✔️머신러닝 모델링 
### LinearRegression

![image](https://github.com/user-attachments/assets/cabe3a06-2027-4a31-8524-50e03def3bf1)
- 스케일링 후, 영향을 미치는 요인은 PM10(369), 해면기압(150), 현지기압(-147)

---
## feature_importance 비교 
### RandomForest
![image](https://github.com/user-attachments/assets/3d0a867a-79fe-4eb8-bb34-37641af508e0)

### GradientBoosting
![image](https://github.com/user-attachments/assets/dfc697ed-e798-4e20-b469-9e4e3800984b)

### LightGBM
![image](https://github.com/user-attachments/assets/6b8707ef-e222-487d-8deb-7e828672acd9)

- **해당 자료들을 통해 PM10이 예측시 가장 중요한 feature라는 점 확인**
---
## ✔️종합결과 
- **모델 성능 비교**

![image](https://github.com/user-attachments/assets/de4a0193-01eb-4504-96a3-5d8ef7048687)
- 모든 모델이 r2 score이 0.93이상임
- 모델을 선택할시에 mse가 가장 낮은 LinearRegression모델 선택
