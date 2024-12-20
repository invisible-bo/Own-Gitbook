---
description: '데이터 전처리 : 데이터를 모델에 맞게 정제하고 준비하는 과정'
---

# Data Preprocessing

### 1. Missing Values(결측치 처리)

결측치 : 데이터셋 에서 값이 비어있거나 누락된 데이터

* 삭제 : 결측값이 적은 경우 해당 샘플 또는 feature 삭제
* 대체 : 평균, 중앙값, 최빈값, 또는 예측 모델을 사용해 대체

ex)

```python
# 예: pandas로 결측값 처리
df.fillna(df.mean(), inplace=True)  # 평균으로 결측값 대체
```



### 2. Outliers(이상치 처리)

이상치 : 다른 데이터와 비교했을 때 현저히 차이가 나는 값\
**이상치 탐지 방법**: IQR(Interquartile Range), z-score, 도메인 지식

* 제거, 대체(중앙값이나 평균값으로), 변환(로그변환, 스케일링등)
* 의미있는 데이터일 경우 분석 모델에 포함



### 3. Normalization or Standardization(데이터 정규화 또는 표준화)

* 정규화 :&#x20;

1\) 데이터 값을 0과 1 사이로 스케일링.

2\) 주로 최소/최대 범위로 정규화 (Min-Max Scaling)

```python
from sklearn.preprocessing import MinMaxScaler
scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)
```

* 표준화 :&#x20;

1\) 데이터 분포를 평균 0, 표준편차 1로 변환

2\) 주로 정규분포 가정을 필요로 하는 알고리즘에 적합 (예: SVM, 회귀)

```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

