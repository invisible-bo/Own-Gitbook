---
description: 주택 가격 예측 모델 구축
---

# \*Predict Housing Price

```python
# 가상환경에서 실행
import pandas as pd

housing_df = pd.read_csv('housingdata.csv')

print(housing_df)
# 데이터셋 불러오기

```

```
# DataSet
CRIM    ZN  INDUS  CHAS    NOX     RM   AGE     DIS  RAD  TAX  \
0    0.00632  18.0   2.31   0.0  0.538  6.575  65.2  4.0900    1  296   
1    0.02731   0.0   7.07   0.0  0.469  6.421  78.9  4.9671    2  242   
2    0.02729   0.0   7.07   0.0  0.469  7.185  61.1  4.9671    2  242   
3    0.03237   0.0   2.18   0.0  0.458  6.998  45.8  6.0622    3  222   
4    0.06905   0.0   2.18   0.0  0.458  7.147  54.2  6.0622    3  222   
..       ...   ...    ...   ...    ...    ...   ...     ...  ...  ...   
501  0.06263   0.0  11.93   0.0  0.573  6.593  69.1  2.4786    1  273   
502  0.04527   0.0  11.93   0.0  0.573  6.120  76.7  2.2875    1  273   
503  0.06076   0.0  11.93   0.0  0.573  6.976  91.0  2.1675    1  273   
504  0.10959   0.0  11.93   0.0  0.573  6.794  89.3  2.3889    1  273   
505  0.04741   0.0  11.93   0.0  0.573  6.030   NaN  2.5050    1  273   

     PTRATIO       B  LSTAT  MEDV  
0       15.3  396.90   4.98  24.0  
1       17.8  396.90   9.14  21.6  
2       17.8  392.83   4.03  34.7  
3       18.7  394.63   2.94  33.4  
4       18.7  396.90    NaN  36.2  
..       ...     ...    ...   ...  
501     21.0  391.99    NaN  22.4  
502     21.0  396.90   9.08  20.6  
503     21.0  396.90   5.64  23.9  
504     21.0  393.45   6.48  22.0  
505     21.0  396.90   7.88  11.9  

[506 rows x 14 columns]
```

```
# columns explain
- CRIM - per capita crime rate by town 
(마을별 1인당 범죄율)

- ZN - proportion of residential land zoned for lots over 25,000 sq.ft. 
(25,000평방피트 이상의 부지에 대해 구획된 주거용 토지의 비율)

- INDUS - proportion of non-retail business acres per town
(INDUS - 지역별 비소매 상업 지역 비율)

- CHAS - Charles River dummy variable (1 if tract bounds river; 0 otherwise)
(찰스강 더미 변수 (구역이 강과 접하면 1, 그렇지 않으면 0))

- NOX - nitric oxides concentration (parts per 10 million)
(질소산화물 농도 (1천만분율))

- RM - average number of rooms per dwelling
(주거당 평균 객실 수)

- AGE - proportion of owner-occupied units built prior to 1940
(1940년 이전에 지어진 소유주 점유의 비율)

- DIS - weighted distances to five Boston employment centres
(보스턴 고용 센터 5곳까지의 가중 거리)

- RAD - index of accessibility to radial highways
(방사형 고속도로 접근성 지수)

- TAX - full-value property-tax rate per $10,000
($10,000당 전액 재산세율)

- PTRATIO - pupil-teacher ratio by town
(지역별 학생-교사 비율)

- B - 1000(Bk - 0.63)^2 where Bk is the proportion of blacks by town
(마을별 흑인 비율)
- LSTAT - % lower status of the population
(인구 중 하위 계층 비율 (%))

- MEDV - Median value of owner-occupied homes in $1000's
(소유주가 거주하는 주택의 중간값 $1000$s)


중간값(Median) vs 중앙값(Mean)
중간값: 데이터의 중앙값으로, 극단적인 값(이상치)의 영향을 받지 않음
평균값: 데이터의 합을 전체 데이터 수로 나눈 값으로, 이상치의 영향을 크게 받을 수 있음
```

### 1. 훈련 data와 테스트 data로 분리

```python
from sklearn.model_selection import train_test_split # data 분리작업
X = housing_df.drop(columns=['MEDV'])  # 독립 변수. MEDV column을 제외하고 가져옴
y = housing_df['MEDV']                 # 종속 변수. MEDV column만 가져옴

# 데이터 분리 (테스트 데이터를 30%로 사용, 70%는 훈련데이터로 사용)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# 분리된 데이터 크기 확인
print("훈련 데이터 (독립 변수):", X_train.shape)
print("테스트 데이터 (독립 변수):", X_test.shape)
print("훈련 데이터 (종속 변수):", y_train.shape)
print("테스트 데이터 (종속 변수):", y_test.shape)

#결과
훈련 데이터 (독립 변수): (354, 13)
테스트 데이터 (독립 변수): (152, 13)
훈련 데이터 (종속 변수): (354,)
테스트 데이터 (종속 변수): (152,)
```

{% hint style="info" %}
random\_state=


{% endhint %}











