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

print(housing_df_cleaned)
   CRIM    ZN  INDUS    NOX     RM   AGE     DIS  TAX  PTRATIO  LSTAT  \
0    0.00632  18.0   2.31  0.538  6.575  65.2  4.0900  296     15.3   4.98   
1    0.02731   0.0   7.07  0.469  6.421  78.9  4.9671  242     17.8   9.14   
2    0.02729   0.0   7.07  0.469  7.185  61.1  4.9671  242     17.8   4.03   
3    0.03237   0.0   2.18  0.458  6.998  45.8  6.0622  222     18.7   2.94   
4    0.06905   0.0   2.18  0.458  7.147  54.2  6.0622  222     18.7    NaN   
..       ...   ...    ...    ...    ...   ...     ...  ...      ...    ...   
501  0.06263   0.0  11.93  0.573  6.593  69.1  2.4786  273     21.0    NaN   
502  0.04527   0.0  11.93  0.573  6.120  76.7  2.2875  273     21.0   9.08   
503  0.06076   0.0  11.93  0.573  6.976  91.0  2.1675  273     21.0   5.64   
504  0.10959   0.0  11.93  0.573  6.794  89.3  2.3889  273     21.0   6.48   
505  0.04741   0.0  11.93  0.573  6.030   NaN  2.5050  273     21.0   7.88   

     MEDV  
0    24.0  
1    21.6  
2    34.7  
3    33.4  
4    36.2  
..    ...  
501  22.4  
502  20.6  
503  23.9  
504  22.0  
505  11.9  

[506 rows x 11 columns]
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
   random\_state=42는 관습적으로 많이 사용되며, 반드시 42일 필요는 없음. 원하는 숫자를 사용해도 동일한 역할을 수행
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



3\)  X\_train에서 IQR 기준 계산

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



4\) Scaling(Standardization or Normalization) : 표준화 혹은 정규화

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



5\) Feature Selection(특징선택)

* 종속 변수(MEDV)와 가장 관련이 높은 변수를 식별
* 종속 변수(MEDV)와 각 독립 변수 간 상관관계를 확인\
  상관계수가 높은 변수는 모델 성능에 더 기여할 가능성이 크다

```
1)상관관계 분석:
종속 변수(MEDV)와 각 독립 변수 간 상관관계를 확인하여 선택/제거할 변수를 결정

2)랜덤 포레스트 기반 변수 중요도 평가:
트리 기반 모델로 변수 중요도를 계산하여 선택

3)통계적 방법:
SelectKBest 또는 RFE(Recursive Feature Elimination) 방법으로 중요한 변수를 선택

4)결과 데이터 준비:
선택된 변수만으로 새로운 데이터셋 구성
```

<pre><code><strong>1)seaborn 설치(시각화도구)
</strong>pip install seaborn

2)matplotlib : Python의 시각화 라이브러리
matplotlib.pyplot

3)plt는 그래프 생성, 설정, 표시 등의 작업을 간단히 수행할 수 있는 강력한 도구

plt로 제공되는 주요 기능
- 그래프 생성
그래프를 생성하고 데이터를 시각화
예: 선 그래프, 막대 그래프, 산점도, 히스토그램 등
- 그래프 설정

축(x, y)의 범위 설정, 제목, 레이블, 범례 추가
- 그래프 표시

**plt.show()를 통해 생성한 그래프를 출력**
</code></pre>

{% hint style="info" %}
<pre><code><strong>1)히트맵 - 데이터의 상관관계 또는 행렬 데이터를 시각화
</strong><strong>import seaborn as sns
</strong>import matplotlib.pyplot as plt

sns.heatmap(data=corr_matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap")
plt.show()

2)박스 플롯 - 데이터 분포와 이상치를 시각화:
sns.boxplot(data=housing_df, x="MEDV", y="RM")
plt.title("Box Plot of RM vs MEDV")
plt.show()

3)분포 플롯 - 데이터의 분포를 확인
sns.histplot(data=housing_df, x="MEDV", kde=True)
plt.title("Distribution of MEDV")
plt.show()

4)산점도 플롯 - 변수 간 관계를 시각화
sns.scatterplot(data=housing_df, x="RM", y="MEDV")
plt.title("Scatter Plot of RM vs MEDV")
plt.show()
</code></pre>
{% endhint %}

```python
# 상관관계 행렬 계산
corr_matrix = housing_df_cleaned.corr()

# 상관관계 히트맵 시각화
plt.figure(figsize=(12, 8))
sns.heatmap(corr_matrix, annot=True, cmap="coolwarm", fmt=".2f")
plt.title("Correlation Matrix with MEDV")
plt.show()

# MEDV와의 상관관계 출력
medv_corr = corr_matrix['MEDV'].sort_values(ascending=False)
print("MEDV와의 상관관계:\n", medv_corr)
```

<figure><img src="../../../../.gitbook/assets/image (10).png" alt=""><figcaption><p>MEDV와의 상관관계: MEDV 1.000000 RM 0.695360 ZN 0.373136 DIS 0.249929 CRIM -0.391363 AGE -0.394656 NOX -0.427321 TAX -0.468536 INDUS -0.481772 PTRATIO -0.507787 LSTAT -0.735822 Name: MEDV, dtype: float64</p></figcaption></figure>

```
특징 선택
선택 기준
상관계수의 절대값 기준:
|상관계수| ≥ 0.7: 매우 강한 상관관계 (Strong correlation)
0.5 ≤ |상관계수| < 0.7: 강한 상관관계 (Moderate to strong correlation)
0.3 ≤ |상관계수| < 0.5: 중간 정도의 상관관계 (Moderate correlation)
|상관계수| < 0.3: 약한 상관관계 (Weak or no correlation)
```

```
1. MEDV와 주요 변수 상관관계
히트맵에서 MEDV와 다른 변수 간의 상관관계를 보면:

RM (주거당 평균 객실 수):

상관계수: +0.70
양의 상관관계: 객실 수가 많을수록 주택 가격이 상승.
LSTAT (하위 계층 비율):

상관계수: -0.74
음의 상관관계: 하위 계층 비율이 높을수록 주택 가격이 감소.
PTRATIO (학생-교사 비율):

상관계수: -0.51
음의 상관관계: 학생-교사 비율이 높을수록 주택 가격이 감소.
TAX (재산세율):

상관계수: -0.47
음의 상관관계: 재산세율이 높을수록 주택 가격이 감소.
NOX (질소산화물 농도):

상관계수: -0.43
음의 상관관계: 공기 오염도가 높을수록 주택 가격이 감소.
```

```python
# 상관관계 
# RM (주거당 평균 객실 수): 양의 상관관계(객실 수가 많을수록 주택 가격이 상승)
# LSTAT (하위 계층 비율): 음의 상관관계(하위 계층 비율이 높을수록 주택 가격이 감소)
# PTRATIO (학생-교사 비율) : 음의 상관관계(학생-교사 비율이 높을수록 주택 가격이 감소)
# TAX (재산세율) : 음의 상관관계(재산세율이 높을수록 주택 가격이 감소)
# NOX (질소산화물 농도) : 음의 상관관계(공기 오염도가 높을수록 주택 가격이 감소)
```



6\) Data준비 마무리

```python
selected_features = ['RM', 'LSTAT', 'PTRATIO', 'TAX', 'NOX']

X_train_selected = X_train_cleaned[selected_features] 
# train data의 독립 변수(스케일링, 전차리를 한뒤의)중에 선택된 변수만 가져옴

X_test_selected = X_test_cleaned[selected_features] 
# test data의 의 독립 변수(스케일링, 전차리를 한뒤의) 중에 선택된 열만 선택
```

{% hint style="info" %}
특징 선택 필요한 이유:

* 불필요한 변수 제거로 모델의 계산 효율성을 높이고 과적합(overfitting)을 방지
* 선택된 변수들이 MEDV와 가장 관련성이 높으므로, 모델의 성능을 최적화할 가능성이 크다
* 훈련 데이터(X\_train\_cleaned)와 테스트 데이터(X\_test\_cleaned)에서 동일한 변수만 사용하여 일관된 학습 및 평가 환경을 제공
{% endhint %}

```python
print(X_train_selected.shape) 
print(X_test_selected.shape)  
# 훈련 데이터의 샘플 수(행), 선택된 특성(변수)수 (열)
# 선택된 독립변수(x_train_selected)와 종속변수(Y-train)로 모델학습
# (162, 5)
# (92, 5)

# X_train_selected와 y_train을 데이터프레임으로 변환
X_train_selected = pd.DataFrame(X_train_selected)
y_train = pd.Series(y_train)



# X_train_selected의 인덱스와 동일하게 y_train 필터링
y_train = y_train.loc[X_train_selected.index]

print(f"X_train_selected shape: {X_train_selected.shape}")
print(f"y_train shape: {y_train.shape}")
# X_train_selected shape: (162, 5)
# y_train shape: (162,)
```

***

## 4. Model training & Model Evaluation (모델학습 & 모델평가)

* 선택된 독립변수(x\_train\_selected)와 종속변수(Y-train)로 모델학습



1. 선형 회귀 모델(Linear Regression)

```python
from sklearn.linear_model import LinearRegression #선형 회귀 모델

# 모델 생성 및 학습
model = LinearRegression()
model.fit(X_train_selected, y_train)

# 테스트 데이터 예측
y_pred = model.predict(X_test_selected)    
```

```python
# 평가
mse = mean_squared_error(y_test, y_pred)
mae = mean_absolute_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f"평가 결과:\nMSE: {mse:.2f}, MAE: {mae:.2f}, R²: {r2:.2f}")
# 평가 결과:
# MSE: 9.56, MAE: 2.22, R²: 0.77
```

{% hint style="info" %}
<pre><code>MSE (Mean Squared Error):
예측값과 실제값의 차이를 제곱한 후 평균을 구한 값
값이 작을수록 모델이 실제값에 더 가까운 예측을 하고 있다는 의미

MAE (Mean Absolute Error): 
예측값과 실제값의 절대적인 차이의 평균
모델이 평균적으로 단위만큼의 오차를 내고 있다는 것을 의미

<strong>R² (R-Squared): 
</strong>모델이 데이터를 얼마나 잘 설명하는지를 나타내는 지표
1.0에 가까울수록 더 나은 모델
0.77은 모델이 전체 데이터 분산의 77%를 설명하고 있다는 의미
</code></pre>
{% endhint %}

```
평가 결과 해석

(1) MSE(Mean Squared Error) 
MSE는 9.56으로, 모델이 예측한 주택 가격이 실제 주택 가격과 
평균적으로 9.56 단위의 제곱 오차를 가지고 있음을 의미

(2)MAE(Mean Absolute Error)
MAE는 2.22로, MSE보다 더 직관적으로 모델의 예측 오차가 평균적으로 약 2.22 단위임을 나타냄
주택 가격(MEDV)의 값이 $1000 단위로 측정되므로, 평균적으로 약 $2200 정도의 
오차가 발생한다고 볼 수 있음

(3) R²(R-Squared):결정계수
R² = 0.77:
모델이 입력 변수(RM, LSTAT, PTRATIO, TAX, NOX)를 기반으로, 
주택 가격(MEDV)의 변동성 중 77%를 설명
1.0에 가까울수록 좋은 성능이며, 0.77은 비교적 괜찮은 성능을 나타냄
다만, 남은 23%의 변동성은 모델이 설명하지 못하며, 
이는 추가적인 변수나 비선형 모델 도입으로 보완할 수 있다
```

***

2. 의사 결정 나무(Decision Tree)

```python
from sklearn.tree import DecisionTreeRegressor #의사결정나무
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score

# 의사결정 나무 모델 생성 및 학습
tree_model = DecisionTreeRegressor(random_state=42)
tree_model.fit(X_train_selected, y_train)

# 테스트 데이터 예측
y_pred_tree = tree_model.predict(X_test_selected)
```

```python
# 평가 지표 계산
mse_tree = mean_squared_error(y_test, y_pred_tree)
mae_tree = mean_absolute_error(y_test, y_pred_tree)
r2_tree = r2_score(y_test, y_pred_tree)

print(f"의사결정 나무 평가 결과:\nMSE: {mse_tree:.2f}, MAE: {mae_tree:.2f}, R²: {r2_tree:.2f}")
# 의사결정 나무 평가 결과:
# MSE: 10.19, MAE: 2.51, R²: 0.76
```

```python
# 트리 구조 시각화
from sklearn.tree import plot_tree
import matplotlib.pyplot as plt

plt.figure(figsize=(20, 10))
plot_tree(tree_model, feature_names=X_train_selected.columns, filled=True, rounded=True)
plt.title("Decision Tree Visualization")
plt.show()
```

```python
# 교차 검증으로 모델의 일반화 성능을 평가
from sklearn.model_selection import cross_val_score

cv_scores_tree = cross_val_score(tree_model, X_train_selected, y_train, cv=5, scoring='r2')
print("교차 검증 R² 점수:", cv_scores_tree)
print("평균 R² 점수:", cv_scores_tree.mean())
# # 평가 지표 계산
mse_tree = mean_squared_error(y_test, y_pred_tree)
mae_tree = mean_absolute_error(y_test, y_pred_tree)
r2_tree = r2_score(y_test, y_pred_tree)

print(f"의사결정 나무 평가 결과:\nMSE: {mse_tree:.2f}, MAE: {mae_tree:.2f}, R²: {r2_tree:.2f}")

# 의사결정 나무 평가 결과:
# MSE: 10.19, MAE: 2.51, R²: 0.76
```

```
평가 결과 해석

(1) 10.19는 모델이 주택 가격 예측에서 평균적으로 10.19 단위의 제곱 오차를 내고 있음을 의미
(2) 주택 가격이 $1000 단위로 측정되므로, 평균 약 $2510 정도의 오차가 발생
(3) 0.76은 모델이 전체 데이터의 변동성 중 76%를 설명한다는 것을 의미
    나머지 24%는 모델이 설명하지 못하는 변동성
```

***

3. 랜덤 포레스트(Random Forest)

```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score

# 랜덤 포레스트 모델 생성
rf_model = RandomForestRegressor(random_state=42, n_estimators=100)

# 모델 학습
rf_model.fit(X_train_selected, y_train)

# 테스트 데이터 예측
y_pred_rf = rf_model.predict(X_test_selected)
```

```python
# 평가 지표 계산
mse_rf = mean_squared_error(y_test, y_pred_rf)
mae_rf = mean_absolute_error(y_test, y_pred_rf)
r2_rf = r2_score(y_test, y_pred_rf)

print(f"랜덤 포레스트 평가 결과:\nMSE: {mse_rf:.2f}, MAE: {mae_rf:.2f}, R²: {r2_rf:.2f}")
# 랜덤 포레스트 평가 결과:
# MSE: 6.90, MAE: 1.83, R²: 0.83
```

```
평가 결과 해석

(1) 랜덤 포레스트 모델이 주택 가격을 예측할 때 평균적으로 6.90 단위의 제곱 오차를 냄
(2) 랜덤 포레스트 모델이 주택 가격을 예측할 때 평균적으로 약 $1830 정도의 오차가 발생
(3) 0.83은 모델이 주택 가격 변동성의 83%를 설명할 수 있음을 의미
```

###

### Model 비교

| Model  | MSE   | MAE  | R^2  |
| ------ | ----- | ---- | ---- |
| 선형회귀   | 9.56  | 2.22 | 0.77 |
| 의사결정나무 | 10.19 | 2.51 | 0.76 |
| 랜덤포레스트 | 6.90  | 1.83 | 0.83 |

**랜덤 포레스트 모델이 가장 우수한 성능**

```python
# 중간에 X_test_selected와 y_test의 크기 차이로 오류발생, 
# X_test_selected와 동일한 인덱스를 사용하여 y_test를 필터링
print("X_test_selected 크기:", X_test_selected.shape)
print("y_test 크기:", y_test.shape)
# 크기 확인 후
y_test = y_test.loc[X_test_selected.index]
```



***

### 결과 시각화

1. 선형회귀모델

* 선형회귀모델시각화는 **예측값과 실제값 비교**, **잔차 분석** 등을 통해 모델 성능을 시각적으로 평가

```python
import matplotlib.pyplot as plt

# 예측값과 실제값 비교
plt.figure(figsize=(8, 6))
plt.scatter(y_test, y_pred, alpha=0.7, color='blue')
plt.plot([y_test.min(), y_test.max()], [y_test.min(), y_test.max()], color='red', linestyle='--', linewidth=2)
plt.xlabel("실제값 (y_test)")
plt.ylabel("예측값 (y_pred)")
plt.title("선형 회귀 모델: 예측값과 실제값 비교")
plt.grid(True)
plt.show()
```

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

2. 의사결정나무&#x20;

* Python의 sklearn.tree 모듈을 사용하면 의사결정 나무를 시각화

<pre class="language-python"><code class="lang-python">from sklearn.tree import plot_tree
import matplotlib.pyplot as plt

<strong># 의사결정 나무 모델 생성 및 학습 (기존 모델 사용)
</strong>tree_model = DecisionTreeRegressor(random_state=42)
tree_model.fit(X_train_selected, y_train)

# 의사결정 나무 시각화
plt.figure(figsize=(20, 10))
plot_tree(tree_model, feature_names=X_train_selected.columns, filled=True, rounded=True)
plt.title("Decision Tree Visualization")
plt.show()

</code></pre>

<figure><img src="../../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

```python
from sklearn.tree import export_text # 의사결정나무텍스트기반 시각화

# 트리 구조를 텍스트로 출력
tree_rules = export_text(tree_model, feature_names=list(X_train_selected.columns))
print(tree_rules)
```

3. 랜덤포레스트 시각화

```python
import matplotlib.pyplot as plt #랜덤포레스트 시각화
import pandas as pd

# 특성 중요도 추출
feature_importances = pd.DataFrame({
    'Feature': X_train_selected.columns,
    'Importance': rf_model.feature_importances_
}).sort_values(by='Importance', ascending=False)

# 특성 중요도 시각화
plt.figure(figsize=(10, 6))
plt.bar(feature_importances['Feature'], feature_importances['Importance'])
plt.xlabel('Feature')
plt.ylabel('Importance')
plt.title('Feature Importances from Random Forest')
plt.show()
```

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
