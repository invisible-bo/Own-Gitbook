---
description: '데이터 전처리 : 데이터를 모델에 맞게 정제하고 준비하는 과정'
---

# Data Preprocessing

{% hint style="info" %}
일반적으로 Data를 훈련 data와 테스트 data로 먼저 분리한 후에 전처리를 진행

* 전처리를 데이터 전체에 적용하면 테스트 데이터에 대한 정보가 훈련 데이터에 포함되어 정보 누출(data leakage) 문제가 발생할 수 있다.
* 실제 상황에서는 새로운 데이터를 처리해야 하므로, 테스트 데이터는 모델이 보지 못한 상태로 유지되어야 한다.
{% endhint %}



## scikit-learn library

머신러닝 라이브러리로, 데이터 전처리, 지도 학습 및 비지도 학습, 모델 평가 및 선택 등 다양한 머신러닝 작업을 수행할 수 있는 기능을 제공

```
pip install scikit-learn
```

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

