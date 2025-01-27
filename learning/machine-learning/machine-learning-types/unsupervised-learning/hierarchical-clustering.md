---
description: 계층적 군집화
---

# Hierarchical Clustering

## 계층적 군집화(Hierarchical Clustering)

데이터 포인트를 계층적으로 그룹화하여 클러스터링을 수행하는 방법\
이 기법은 데이터의 계층 구조를 시각화할 수 있는 **덴드로그램(Dendrogram)** 을 생성하여 \
클러스터링 과정을 직관적으로 보여줌



### 1. 계층적 군집화의 주요 특징

1. 계층적 구조:

* 클러스터가 단계적으로 합쳐지거나 분리되면서 트리 구조를 형성
* 결과는 데이터 간의 유사성을 기반으로 클러스터링 과정을 나타내는 **덴드로그램** 으로 시각화 됨

2. 모든 클러스터링 과정 시각화:

* 클러스터의 수를 사전에 정하지 않아도, 덴드로그램에서 적절한 클러스터 수를 \
  시각적으로 결정할 수 있음

3. 유형

* **병합적 방법(Agglomerative)**:

— 각 데이터 포인트(data point)를 개별 클러스터로 시작하고, 유사한 클러스터를 점차 병합

— 가장 일반적인 계층적 군집화 방법

* **분할적 방법(Divisive)**:

— 모든 데이터를 하나의 클러스터로 시작하고, 점차적으로 분리

{% hint style="info" %}
Data point?

군집화를 수행할 데이터 집합 내의 개별 관측값 또는 객체를 의미

이는 군집화 과정에서 각 데이터 포인트가 서로 다른 군집으로 분류되거나, 유사성에 따라 다른 데이터 포인트와 함께 하나의 군집으로 묶이는 단위
{% endhint %}



### 2. 병합적 군집화 과정

1. 각 데이터 포인트를 하나의 클러스터로 시작.
2. 가장 유사한 두 클러스터를 병합
3. 이 과정을 반복하여 클러스터 수가 하나가 될 때까지 진행
4. 덴드로그램을 통해 최적의 클러스터 수를 결정



### 3. 클러스터 간 유사도 계산 방법

1. Single Linkage:

* 두 클러스터 간 가장 가까운 데이터 포인트 간의 거리로 유사도를 계산
* 긴 사슬 모양 클러스터가 생성될 수 있음

2. Complete Linkage:

* 두 클러스터 간 가장 먼 데이터 포인트 간의 거리로 유사도를 계산
* 밀집된 클러스터 생성

3. Average Linkage:

* 두 클러스터 간 모든 데이터 포인트의 평균 거리를 사용

4. Centroid Linkage:

* 클러스터의 중심(centroid) 간의 거리로 계산



### 4. Dendrogram(덴드로그램)

* 덴드로그램은 데이터 간의 계층적 관계를 나무 구조로 표현
* **X축**: 데이터 포인트 또는 클러스터
* **Y축**: 두 클러스터를 병합할 때의 거리(유사도)
* 덴드로그램에서 적절한 **클러스터 수**를 결정:\
  \- 클러스터 간의 병합 거리(Y축)가 급격히 증가하는 지점을 기준으로 클러스터 수 선택



### 5. 장, 단점

**장점**&#x20;

1. 클러스터 수를 사전에 설정할 필요 없음

* 덴드로그램을 통해 적절한 클러스터 수를 직관적으로 결정

2. 직관적인 시각화

* 데이터의 계층적 구조를 명확히 볼 수 있음

3. 다양한 데이터에 적합

* 크기가 다른 클러스터나 비선형적 구조를 가진 데이터에도 적합



**단점**&#x20;

1. 계산 복잡성

* 데이터 포인트 수가 많아질수록 계산 비용이 급격히 증가
* 대규모 데이터에 적합하지 않음

2. 병합 과정의 불가역성

* 잘못 병합된 클러스터를 다시 분리할 수 없음









