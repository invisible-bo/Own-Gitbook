---
description: DBSCAN (Density-Based Spatial Clustering of Applications with Noise)
---

# DBSCAN

## DBSCAN

* 밀도 기반 클러스터링 알고리즘으로, 데이터 포인트의 밀도에 따라 클러스터를 형성하며, 노이즈와 이상치를 처리할 수 있는 특징을 가짐



### DBSCAN의 주요 개념

1. 밀도 기반 클러스터링:

* 데이터 포인트가 특정 밀도 기준을 충족하면 클러스터에 포함
* 밀도가 낮은 영역에 위치한 데이터는 **noise** 로 간주

2. 핵심 매개변수:

* `esp`(epsilon):\
  \- 데이터 포인트를 이웃으로 간주하기 위한 최대 거리
* `min_samples`:\
  \- 클러스터를 형성하기 위해 필요로 하는 최소 데이터 포인트 수

3. 포인트 유형:

* Core Point:\
  \- 반경 `esp` 내에 최소 `min_samples` 이상의 포인트가 있는 점
* Border Point:\
  \- 반경 `esp` 내에 `min_samples` 보다 적은 포인트가 있지만,\
  &#x20;  다른 Core Point에 속한 점
* Noise Point:\
  \- 어떠한 Core Point나 Cluster에도 속하지 않는 점



### DBSCAN의 작동 방식

1. 초기화:

* 모든 Data Point를 방문하지 않은 상태로 시작

2. 밀도 기반 확장:

* 하나의 Core Point에서 시작하여 반경 `eps` 내의 이웃 데이터 포인트를 찾고 클러스터를 확장
* 이웃 데이터 중 추가 Core Point가 있으면, 그 점을 중심으로 클러스터를 계속 확장

3. 노이즈 처리:

* Core Point와 Border Point에 속하지 않는 데이터는 노이즈로 분류

4. 반복:

* 모든 Data Point가 방문될 때까지 과정을 반복



### DBSCAN의 장, 단점

#### 장점

1. Noise 처리 가능:

* 밀도가 낮은 이상치나 노이즈를 클러스터에 포함시키지 않음

2. 비선형 구조에 적합:

* 원형, 타원형 등 복잡한 클러스터 구조를 감지할 수 있음

3. 클러스터 수 사전 설정 불필요:

* K-Means와 달리 클러스터 수를 사전에 지정할 필요가 없음



단점

1. 매개변수 설정 민감:

* `eps` 와 `min_samples` 값을 적절히 설정하지 않으면 성능이 저하될 수 있음.

2. 밀도 불균형에 약함:

* DataSet에서 클러스터 간 밀도가 크게 다르면 일부 클러스터를 감지하지 못할 수 있음

3. 고차원 데이터에 취약:

* 고차원 데이터에서 유클리디안 거리 기반으로 작동하기 때문에, **차원의 저주** 에 영향을 받을 수 있다

{% hint style="info" %}
차원의 저주(Curse of Dimensionality)

차원의 저주는 고차원 데이터 분석에서 발생하는 여러 문제를 설명하는 용어

이는 데이터의 차원이 증가할수록 데이터 분석, 머신 러닝 모델링, 또는 거리 기반 알고리즘의 성능에 부정적인 영향을 미칠 수 있음을 의미



1. 데이터 희소성 증가
2. 거리의 차이 축소
3. 계산 비용 증가
4. 모델 과적합 위험 증가
5. 데이터 시각화 및 해석 어려움



차원의 저주를 완화하는 방법

* 차원 축소(Dimensionality Reduction): PCA(Principal Component Analysis), t-SNE, UMAP과 같은 기법을 사용하여 데이터를 더 낮은 차원으로 변환
* 특징 선택(Feature Selection): 데이터에서 중요한 특징만 선택하여 차원을 줄임
* 정규화 및 거리 척도 변경: 고차원에서 거리 기반 문제를 완화하기 위해 적합한 거리 척도(예: 코사인 유사도)를 사용
* 데이터 샘플링: 데이터의 복잡성을 줄이기 위해 적절히 샘플링



고차원 데이터에서는 차원의 저주를 이해하고, 이를 완화하기 위한 적절한 기법을 적용하는 것이 중요
{% endhint %}

***

### DBSCAN을 사용할 때 적절한 Data

* 밀도가 서로 다른 클러스터를 포함한 data
* 이상치(Noise)가 포함된 data
* 비선형적 또는 비구형 클러스터 구조를 가진 data


















