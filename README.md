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
|Elice Cloud Free|가능|불가능|불가능| RAM 부족 |1.098/9.728|13.04/16|
|Elice Cloud Basic|가능|가능|가능| - |6.1/9.728|24.81/32|
|Colaboratory|가능|불가능|불가능| RAM 부족 |2.7/15.0|12.1/12.7|

-> 많은 데이터 적재를 위해서는 RAM이 커야함
### TODO
1. Lagged Feature 추가 테스트
2. 여분의 CSV의 정보 활용하여 학습 테스트
3. 주말, 공휴일, 라이브 방송을 통한 혜택 등 매출을 올릴 수 있었던 Event의 추가
4. 데이터 시각화를 통해 너무 매출이 크거나 작은 케이스가 있다면 제거하여 학습 진행
5. Fold dataset 만들어서 Ensemble 진행하기 
-> CFG에 Fold number 옵션을 추가, make_train_data 함수 이후 각 데이터셋을 5개의 구간으로 나눔, CFG Fold option에 따라서 train,valid 데이터 생성하기
6. PSFA를 진행하기 위해 별도의 변환 식 추가
-> len(data.columns) - (train_window_size + test_window_size) + 1 설정, valid 길이를 5분할하여 시작 idx 저장하여 PSFA를 바로 적용

### 학습 결과
|일자|모델|성능(LB)|옵션|final_train_loss|final_val_loss|final_PSFA_val|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|2023.08.07|LSTM|0.49186|Baseline -> window size 30, batch 64|0.1815|0.01751|-|
|2023.08.09|LSTM|0.50387|Baseline -> window size 30|0.01817|0.01793|-|
|2023.08.09|LSTM|0.45893|Baseline -> window size 30, batch 4096|0.01854|0.1909|-|
|2023.08.10|LSTM|0.48783|Baseline|0.01768|-|0.54361(PSFA non inverse-scaling)|
|2023.08.10|LSTM|0.51388|Baseline|0.01768|-|0.59079(PSFA)|
|2023.08.11|LSTM|**0.52605**|Baseline -> 20 epoch|0.01730|-|0.66161(PSFA)|
|2023.08.11|LSTM|0.48705|Baseline -> 30 epoch|0.01702|-|0.58401(PSFA)|
|2023.08.11|LSTM|0.51699|Baseline -> 40 epoch|0.01683|-|0.61648(PSFA)|
|2023.08.12|LSTM|0.50905|Baseline -> 40 epoch|-|-|0.63(PSFA)|
|2023.08.12|LSTM|0.50061|Baseline -> 50 epoch|-|-|0.63(PSFA)|
|2023.08.18|LSTM|0.50353|Baseline -> 20 epoch + 1 feature|0.01967|-|0.58(PSFA)|
### 학습 결과

## 참고자료
- [Predict Future Sales - 1st](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales/discussion/374500)
- [Predict Future Sales - 2nd](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales/discussion/190784)
- [Store sales - Time Series Forecasting](https://www.kaggle.com/code/ferdinandberr/darts-forecasting-deep-learning-global-models#4.5.-Model-Comparison)
- [Supercharging with LightGBM](https://www.kaggle.com/code/masterofdeception/supercharging-with-lightgbm)
- [Cracking the Walmart Sales Forecasting challenge](https://www.kaggle.com/code/masterofdeception/supercharging-with-lightgbm)
- [S3E19 : Time Series = LSTM on residuals](https://www.kaggle.com/code/thomasmeiner/s3e19-time-series-lstm-on-residuals)
