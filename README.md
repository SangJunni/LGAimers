# LGAimers
LGAimers Dacon 경진대회 참여
## 대회 유의사항(Data Leakage)
- 2023년 4월 5일 ~ 2023년 4월 25일의 판매량을 에측하기 때문에 관련된 해당 기간의 이력을 활용하는 것은 데이터 유출로 규정
- 단, 규칙성이 있는 이벤트에 대해서는 활용이 가능
- 외부 데이터 사용 금지 (해커톤 제공 학습 데이터만 활용 가능)
- 법적 제약이 없으며 논문으로 공개된 베이스의 사전 학습 모델만 사용 가능(본인이 외부 데이터로 사전 학습한 모델을 추가 학습시켜 사용하는 것은 불가능)

## 평가방식
1. 1차 평가  
    : LB Private Score 100%(대회 종류 후 일괄 채점하여 공개)
2. 2차 평가  
    : Private 상위 30팀의 경우 코드 및 PPT 제출 대상  
    -> 검증을 통과한 상위 30팀의 경우 오프라인 해커톤 진출(100명 미달 시, 추가 선발 가능)

## 온라인 채널 제품 판매량 예측 AI 온라인 해커톤
### Metric -> Pseudo SFA (PSFA)
![image](https://github.com/SangJunni/LGAimers/assets/79644050/7d0b8cfa-c425-4698-81c1-20fa88951c1d)

### 학습 플랫폼
|플랫폼|WINDOW_SIZE 30|WINDOW_SIZE 60|WINDOW_SIZE 90|사유|VRAM|RAM|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|Elice Cloud|가능|불가능|불가능| RAM 부족 |2.7/15.0|12.1/12.7|
|Colaboratory|가능|불가능|불가능| RAM 부족 |1.098/9.728|13.04/16|

-> 많은 데이터 적재를 위해서는 RAM이 커야함
### 학습 결과
|일자|모델|성능|옵션|
|:--:|:--:|:--:|:--:|
|2023.08.07|LSTM|0.49186|Baseline -> window size 30, batch 64|
|2023.08.09|LSTM|~ing|Baseline -> window size 30|
## 참고자료
- [Predict Future Sales - 1st](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales/discussion/374500)
- [Predict Future Sales - 2nd](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales/discussion/190784)
- [Store sales - Time Series Forecasting](https://www.kaggle.com/code/ferdinandberr/darts-forecasting-deep-learning-global-models#4.5.-Model-Comparison)
