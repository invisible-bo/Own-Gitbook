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

```python
print(customer_df.isnull().sum()) # 결측값 개수 확인
# 결과 CustomerID                0
# Gender                    0
# Age                       0
# Annual Income (k$)        0
# Spending Score (1-100)    0
# dtype: int64 
```

### EDA(Exploratory Data Analysis)-데이터 탐색 분석













* 데이터셋 탐색 및 전처리:
  * 결측치 처리
  * 스케일링
    * 데이터의 스케일을 조정하기 위해 표준화(Standardization) 또는 정규화(Normalization)를 수행합니다
* 클러스터링 기법 적용:
  * K-means
  * 계층적 군집화
  * DBSCAN 등의 알고리즘
* 최적의 클러스터 수 결정:
  * 엘보우 방법 또는 실루엣 점수를 사용하여 최적의 클러스터 수를 찾습니다.
* 결과 시각화:
  * 클러스터링 결과를 2D 또는 3D로 시각화하여 고객 세분화 결과를 분석합니다.
    * **시각화**: matplotlib 또는 seaborn을 사용하여 클러스터를 색상으로 구분하여 시각화합니다. 2D 플롯을 사용하여 각 클러스터를 다른 색으로 표현합니다.









