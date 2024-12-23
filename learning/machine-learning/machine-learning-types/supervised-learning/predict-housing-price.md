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

<pre><code><strong># DataSet
</strong>CRIM    ZN  INDUS  CHAS    NOX     RM   AGE     DIS  RAD  TAX  \
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
</code></pre>

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

## 1. Columns Data 분석

<pre class="language-python"><code class="lang-python"># CHAS, RAD, B columns가 주택가격 형성에 크게 중요하지 않다고 판단하고 제거하기로 결정
columns_to_drop = ['CHAS', 'RAD', 'B']
# CHAS, RAD, B 컬럼 제거
# pandas의 drop 메서드를 사용하여 DataFrame에서 지정한 열(또는 행)을 제거
<strong>housing_df_cleaned = housing_df.drop(columns=columns_to_drop)
</strong># 3개의 컬럼을 제거한 데이터셋을 housing_df_cleaned에 변수로 지정

</code></pre>

***

## 2. Train Data와  Test Data로 분리

```python
from sklearn.model_selection import train_test_split # data 분리작업
X = housing_df_cleaned.drop(columns=['MEDV'])  # 독립 변수. MEDV column을 제외하고 가져옴
y = housing_df_cleaned['MEDV']                 # 종속 변수. MEDV column만 가져옴

# 데이터 분리 (테스트 데이터를 30%로 사용, 70%는 훈련데이터로 사용)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# 분리된 데이터 크기 확인
print("훈련 data (독립 변수):", X_train.shape)
print("테스트 data (독립 변수):", X_test.shape)
print("훈련 data (종속 변수):", y_train.shape)
print("테스트 data (종속 변수):", y_test.shape)

#결과
훈련 data (독립 변수): (354, 10)
테스트 data (독립 변수): (152, 10)
훈련 data (종속 변수): (354,)
테스트 data (종속 변수): (152,)
```

{% hint style="info" %}
random\_state

난수 시드값

random\_state는 난수 생성기의 초기값(seed)을 지정

같은 random\_state 값을 사용하면 동일한 무작위 결과가 재현됨

-설정이유

1. 결과 재현성:\
   머신러닝 실험에서 결과를 비교하거나 공유할 때, 데이터를 항상 동일하게 분리하는 것 중요\
   random\_state를 설정하지 않으면 매번 다른 데이터 분리가 이루어질 수 있음
2. 디버깅:\
   데이터를 항상 동일한 방식으로 분리하면 코드의 버그를 추적하거나 모델을 개선할 때 더 쉽게 분석할 수 있음
3. 협업:\
   다른 사람이 코드를 실행할 때도 동일한 결과를 얻을 수 있도록 보장
4. 고정값 설정:\
   random\_state=42는 관습적으로 많이 사용되며, 반드시 42일 필요는 없다. 원하는 숫자를 사용해도 동일한 역할을 수행
{% endhint %}

***

## 3. Data 전처리

```python
print(X_train.isnull().sum())
print(X_test.isnull().sum())  # 결측치 개수 확인
```

1\) 결측치 대체하기(Missing value imputation)

<pre class="language-python"><code class="lang-python">from sklearn.impute import SimpleImputer
# SimpleImputer : 결측치(NaN)**가 포함된 데이터를 특정 값(평균값, 중앙값, 최빈값 등)
# 으로 대체할 때 사용되는 scikit-learn 도구
# mean: 평균값으로 대체 (기본값)
# median: 중앙값으로 대체 
# most_frequent: 최빈값(가장 자주 등장하는 값)으로 대체
# constant: 지정된 값으로 대체(예: fill_value를 사용)
# SimpleImputer는 데이터가 수치형이어야 합니다. 범주형 데이터에는 적합하지 않음
# 결측치를 대체한 후 결과를 DataFrame으로 변환하는 것을 추천 
# 그렇지 않으면 열 이름(columns)이 손실됨

imputer = SimpleImputer(strategy='mean')
# 결측치(NaN)를 각 열의 평균값으로 대체
<strong>
</strong><strong>X_train_imputed = imputer.fit_transform(X_train)  
</strong># 훈련 데이터 처리
<strong># fit_transform:fit: 훈련 데이터 X_train의 각열에 대해 결측치를 대체할 값을 학습(평균값계산)
</strong># transform: 계산된 평균값을 사용해 결측치를 대체한 새로운 데이터를 반환.

X_test_imputed = imputer.transform(X_test)       
# 테스트 데이터 처리
# transform: 훈련 데이터(X_train)에서 학습된 평균값을 사용해 X_test의 결측치를 대체
# 주의: 테스트 데이터에서는 fit_transform을 사용하지 않음 
# 이는 훈련 데이터의 통계값만을 사용해야 데이터 누출(data leakage)을 방지할 수 있기 때문
</code></pre>

* 결측치 대체 확인

```python
# 결과는 NumPy 배열로 반환되므로, 필요하면 DataFrame으로 변환해 사용해야함
X_train_imputed = pd.DataFrame(X_train_imputed, columns=X_train.columns)
X_test_imputed = pd.DataFrame(X_test_imputed, columns=X_test.columns)
# columns=X_train.columns:변환된 DataFrame에 원래 열 이름을 할당

print("훈련 데이터 결측치 개수:", X_train_imputed.isnull().sum().sum())
print("테스트 데이터 결측치 개수:", X_test_imputed.isnull().sum().sum())
# 결과 훈련 데이터 결측치 개수: 0
# 결과테스트 데이터 결측치 개수: 0

```



2\) 이상치 처리(Outliers)

<pre class="language-python"><code class="lang-python">import pandas as pd

# IQR 방식으로 이상치를 제거하는 함수
<strong>def remove_outliers_iqr_pandas(data):
</strong>    cleaned_data = data.copy()  # 원본 데이터를 보호하기 위해 복사본 생성
    for column in cleaned_data.columns:
        Q1 = cleaned_data[column].quantile(0.25)  # 1사분위수(데이터의 하위 25% 값을 계산)
        Q3 = cleaned_data[column].quantile(0.75)  # 3사분위수(데이터의 상위 75% 값을 계산)
        IQR = Q3 - Q1  # IQR 계산
        lower_bound = Q1 - 1.5 * IQR  # 하한선
        upper_bound = Q3 + 1.5 * IQR  # 상한선
        # 이상치 제거
        cleaned_data = cleaned_data[(cleaned_data[column] >= lower_bound) &#x26; (cleaned_data[column] &#x3C;= upper_bound)]
    return cleaned_data

# 예시: X_train 데이터에 IQR 방식 적용
X_train_df = pd.DataFrame(X_train, columns=X.columns)  # X_train을 DataFrame으로 변환
X_train_cleaned = remove_outliers_iqr_pandas(X_train_df)

# 결과 출력
print("이상치 제거 전 X_train 데이터 크기:", X_train.shape)
print("이상치 제거 후 X_train 데이터 크기:", X_train_cleaned.shape)
# 결과
# 이상치 제거 전 X_train 데이터 크기: (354, 10)
# 이상치 제거 후 X_train 데이터 크기: (162, 10)
</code></pre>

* X\_train 데이터에서 이상치 제거 완료 후 X\_test 데이터의 이상치를 제거할 때는 X\_train에서 계산한 IQR 기준을 그대로 사용해야 함. 테스트 데이터는 모델 평가를 위해 사용되며, 훈련 데이터에서 학습한 정보만을 기반으로 처리해야 **데이터 누출(data leakage)을 방지**할 수 있다





* &#x20;X\_train에서 IQR 기준 계산

<pre class="language-python"><code class="lang-python"># IQR 기준 계산
iqr_bounds = {
    column: (
        X_train_df[column].quantile(0.25) - 1.5 * (X_train_df[column].quantile(0.75) - X_train_df[column].quantile(0.25)),
        X_train_df[column].quantile(0.75) + 1.5 * (X_train_df[column].quantile(0.75) - X_train_df[column].quantile(0.25))
    )
    for column in X_train_df.columns
}

<strong># IQR 계산 기준 확인 코드
</strong>for column, (lower_bound, upper_bound) in iqr_bounds.items():
    print(f"{column}: 하한선 = {lower_bound}, 상한선 = {upper_bound}")

</code></pre>

* &#x20;X\_test 데이터에 IQR 기준 적용

```python
# IQR 기준으로 `X_test` 데이터 이상치 제거
def remove_outliers_iqr_test(data, iqr_bounds):
    cleaned_data = data.copy()
    for column, (lower_bound, upper_bound) in iqr_bounds.items():
        cleaned_data = cleaned_data[(cleaned_data[column] >= lower_bound) & (cleaned_data[column] <= upper_bound)]
    return cleaned_data

X_test_df = pd.DataFrame(X_test, columns=X.columns)  # `X_test`를 DataFrame으로 변환
X_test_cleaned = remove_outliers_iqr_test(X_test_df, iqr_bounds)
print("이상치 제거 전 X_test 데이터 크기:", X_test.shape)
print("이상치 제거 후 X_test 데이터 크기:", X_test_cleaned.shape)
# 결과
# 이상치 제거 전 X_test 데이터 크기: (152, 10)
# 이상치 제거 후 X_test 데이터 크기: (92, 10)

```



3\) Scaling(Standardization or Normalization) : 표준화 혹은 정규화

```python
# Standardization 표준화
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X_train_normalized = scaler.fit_transform(X_train_cleaned)
X_test_normalized = scaler.transform(X_test_cleaned)
```

<pre class="language-python"><code class="lang-python"><strong># Normalization 정규화
</strong><strong>from sklearn.preprocessing import StandardScaler
</strong>
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train_cleaned)
X_test_scaled = scaler.transform(X_test_cleaned)
</code></pre>

* 표준화로 진행

```python
# Standardization 표준화로 진행
# 특성(feature)을 평균이 0이고, 
# 분산이 1이 되도록 변환하는 작업
from sklearn.preprocessing import StandardScaler

# 표준화 객체 생성
scaler = StandardScaler()

# 훈련 데이터 표준화 (fit + transform)
X_train_scaled = scaler.fit_transform(X_train_cleaned)

# 테스트 데이터 표준화 (transform만 사용)
X_test_scaled = scaler.transform(X_test_cleaned)
```

```python
# 표준화된 데이터를 DataFrame으로 변환
X_train_scaled_df = pd.DataFrame(X_train_scaled, columns=X_train_cleaned.columns)
X_test_scaled_df = pd.DataFrame(X_test_scaled, columns=X_test_cleaned.columns)

# 표준화된 데이터 확인
print("train 데이터 (표준화 후):")
print(X_train_scaled_df.head())  # 상위 5개 행 출력

print("test 데이터 (표준화 후):")
print(X_test_scaled_df.head())

```



4\) Feature Selection(특징선택)

* 종속 변수(MEDV)와 가장 관련이 높은 변수를 식별
* 종속 변수(MEDV)와 각 독립 변수 간 상관관계를 확인\
  상관계수가 높은 변수는 모델 성능에 더 기여할 가능성이 크다

```python
```







## 4. Model training & Model Evaluation (모델학습 & 모델평가)































