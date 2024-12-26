---
description: 고객 세분화 분석, 고객 데이터셋을 사용하여 비슷한 행동을 보이는 고객 그룹을 식별
---

# \*Customers analytics

## 1. Dataset 탐색 및 전처리

```python
import pandas as pd

customer_df = pd.read_csv('Mall_Customers.csv')
print(customer_df)
```

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

```
Annual Income (k$)
- 고객의 연간 소득을 1,000달러 단위로 나타낸 값
  예를 들어, 값이 15라면 해당 고객의 연간 소득은 15,000달러를 의미
- 고소득과 저소득 고객을 구분하여 다른 마케팅 전략을 수립하는 데 유용

Spending Score (1-100)
- 쇼핑몰에서 고객의 소비 성향을 1에서 100 사이의 점수로 나타낸 값
  점수가 높을수록 고객의 소비가 활발하거나 구매 가능성이 높음을 의미
- 소비 성향이 높은 고객(고득점)과 낮은 고객(저득점)을 구분하여 마케팅 캠페인을 타겟팅할 수 있다
```

### 결측치 탐지

```python
print(customer_df.isnull().sum()) # 결측치 개수 확인
# 결과 CustomerID                0
# Gender                    0
# Age                       0
# Annual Income (k$)        0
# Spending Score (1-100)    0
# dtype: int64 
```

### 이상치 처리(outliers)

Z-Score(표준화 점수)

z-Score를 계산하여 절대값이 특정 임계값(일반적으로 3)을 초과하는 값을 이상치로 간주

```python
from scipy.stats import zscore

# Z-Score 계산
z_scores = zscore(customer_df[['Annual Income (k$)', 'Spending Score (1-100)']])

# 이상치 탐지
customer_df_cleaned = customer_df[(abs(z_scores) < 3).all(axis=1)]

# 이상치 필터링 (Z-Score 절대값이 3 이상인 데이터를 이상치로 간주)
outliers = customer_df[(abs(z_scores) >= 3).any(axis=1)]

# 이상치 데이터 출력
print(outliers)

# 결과
Empty DataFrame
Columns: [CustomerID, Gender, Age, Annual Income (k$), Spending Score (1-100)]
Index: []
```

```python
# 이상치 탐지
customer_df_cleaned = customer_df[(abs(z_scores) < 2.5).all(axis=1)]
# 이상치 필터링 (Z-Score 절대값이 2.5 이상인 데이터를 이상치로 간주)
outliers = customer_df[(abs(z_scores) >= 2.5).any(axis=1)]
# 이상치 데이터 출력
print(outliers)

# 결과
     CustomerID Gender  Age  Annual Income (k$)  Spending Score (1-100)
198         199   Male   32                 137                      18
199         200   Male   30                 137                      83
```

```python
# 해당되는 두개의 data 이상치 제거
customer_df_cleaned = customer_df[(abs(z_scores) < 2.5).all(axis=1)]
```

***

{% hint style="info" %}
고객 세분화 프로젝트에서는 정규화(Normalization)와 **표준화(Standardization)** 중 표준화(Standardization)가 더 적합한 선택



#### **1. 표준화(Standardization)를 선택해야 하는 이유**

1. **클러스터링 알고리즘의 특성**
   * K-Means와 같은 클러스터링 알고리즘은 **거리 기반**으로 작동하므로, 데이터의 분포가 평균 0, 표준편차 1로 스케일링되면 모든 변수에 걸쳐 균일한 중요도를 가지게 된다
   * 표준화는 변수 간 크기 차이로 인해 특정 변수가 클러스터링에 지나치게 영향을 미치는 문제를 방지
2. **데이터의 분포**
   * `Annual Income (k$)`와 `Spending Score (1-100)`는 값의 범위와 분포가 다
     * `Annual Income (k$)`는 10\~130 (범위가 더 넓음)
     * `Spending Score (1-100)`는 1\~100 (범위가 좁음)
   * 이처럼 값의 분포와 범위가 다를 경우, 표준화를 통해 데이터의 분포를 동일하게 맞추는 것이 효과적
3. **정규분포를 가정하지 않아도 됨**
   * 표준화는 데이터가 정규분포를 따르지 않아도 유용\
     이는 클러스터링처럼 데이터의 분포보다는 거리에 의존하는 알고리즘에서 중요





#### **2. 정규화(Normalization)가 덜 적합한 이유**

1. **0\~1 범위로 데이터 제한**
   * 정규화는 변수 값을 0\~1로 제한하여 상대적 크기만 유지
   * 하지만, 값의 분포를 근본적으로 바꾸지는 않으므로 분포가 왜곡되거나 클러스터링 성능에 큰 영향을 미칠 수 있다
2. **변수 분포 차이 해결 부족**
   * 정규화는 변수 간 분포 차이를 해결하지 못하므로, 클러스터링 결과에서 범위가 좁은 변수가 덜 중요하게 다뤄질 수 있다
{% endhint %}

<pre class="language-python"><code class="lang-python"><strong># 표준화 선택
</strong>from sklearn.preprocessing import StandardScaler
# StandardScaler 객체 생성
scaler = StandardScaler()
# 데이터 표준화 
scaled_data = scaler.fit_transform(customer_df[['Annual Income (k$)', 'Spending Score (1-100)']])
</code></pre>

<pre class="language-python"><code class="lang-python"><strong># 표준화된 데이터 데이터프레임으로 변환
</strong>standardized_df = pd.DataFrame(scaled_data, columns=['Annual Income (k$)_standardized', 'Spending Score (1-100)_standardized'])
</code></pre>

{% hint style="info" %}
DataFrame화가 필요한 이유

* **가독성**:
  * 표준화된 데이터를 NumPy 배열로 유지하면 변수 이름이 없어서 어떤 값이 어떤 변수인지 알기 어렵다
* **데이터 병합**:
  * 기존의 데이터프레임과 표준화된 데이터를 병합하거나, 기존 데이터프레임을 대체하려면 데이터프레임화가 유용하다
* **분석 편의성**:
  * 데이터프레임은 Pandas의 다양한 기능(ex: 필터링, 집계, 시각화)을 활용할 수 있어 작업이 편리하다
{% endhint %}

***













