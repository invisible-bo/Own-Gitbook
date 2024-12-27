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

***

### 3. Normalization or Standardization(데이터 정규화 또는 표준화)

###

### 정규화(Normalization)

* **목적:** 각 변수의 값을 0과 1 사이로 변환
* 적용 방법: Min-Max Scaling (최솟값과 최댓값을 기준으로 변환)
* 대표적인 도구: sklearn.preprocessing.MinMaxScaler&#x20;
* 사용 사례: 데이터의 상대적 크기를 유지하며, 범위를 0\~1로 제한하고 싶을 때

{% code fullWidth="false" %}
```python
from sklearn.preprocessing import MinMaxScaler

# MinMaxScaler 객체 생성
scaler = MinMaxScaler()

# 데이터 정규화 (예: 특정 열만 정규화)
normalized_data = scaler.fit_transform(df[['Feature1', 'Feature2']])

# 정규화된 데이터를 DataFrame으로 변환 (선택 사항)
normalized_df = pd.DataFrame(normalized_data, columns=['Feature1_normalized', 'Feature2_normalized'])

# 확인
print(normalized_df.head())

```
{% endcode %}

### 표준화(Standardization)

* **목적:** 각 변수의 값이 평균 0, 표준편차 1이 되도록 변환
* 적용 방법: Z-Score Scaling (데이터에서 평균을 빼고, 표준편차로 나눔)
* 대표적인 도구: sklearn.preprocessing.StandardScaler
* **사용 사례**: 데이터의 분포 차이를 제거하고, 각 변수를 동일한 중요도로 처리하고 싶을 때

```python
from sklearn.preprocessing import StandardScaler

# StandardScaler 객체 생성
scaler = StandardScaler()

# 데이터 표준화 (예: 특정 열만 표준화)
scaled_data = scaler.fit_transform(df[['Feature1', 'Feature2']])

# 표준화된 데이터를 DataFrame으로 변환 (선택 사항)
scaled_df = pd.DataFrame(scaled_data, columns=['Feature1_scaled', 'Feature2_scaled'])

# 확인
print(scaled_df.head())

```

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

### 전체 DataFrame에 적용

표준화 또는 정규화를 데이터프레임 전체에 적용

```python
# 데이터프레임 전체를 표준화
scaled_data = scaler.fit_transform(df)

# 데이터프레임 전체를 정규화
normalized_data = scaler.fit_transform(df)

# 결과를 다시 DataFrame으로 변환
scaled_df = pd.DataFrame(scaled_data, columns=df.columns)
normalized_df = pd.DataFrame(normalized_data, columns=df.columns)
```



### 주의사항

1\) Fit/Transform 분리: Train/Test 데이터로 나눈 경우, 항상 train 데이터에 fit한 스케일러를 test 데이터에 동일하게 적용해야 한다

```python
# Train/Test 데이터 분리 후
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)  # transform만 수행
```

2\) 알고리즘 선택에 따라 다름: 스케일링이 필요한 알고리즘(K-Means, PCA, SVM 등)과 필요하지 않은 알고리즘(트리 기반 모델)은 구분해야 한다





