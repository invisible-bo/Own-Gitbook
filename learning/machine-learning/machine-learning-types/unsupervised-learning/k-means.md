---
description: 비지도 학습 알고리즘
---

# K-means

## 1. K-means

주로 데이터 분석, 데이터 마이닝, 이미지 압축 및 분할 등에 사용

### 주요개념

* **클러스터(Cluster)**: 데이터가 유사한 그룹으로 나뉘어진 결과를 의미
* **군집 중심(Centroid)**: 클러스터 내의 데이터의 중심점으로, 각 클러스터를 대표
* **k**: 나누고자 하는 클러스터의 개수를 나타내는 매개변수



## 2. K-means 알고리즘 동작 과정

1. 초기화 : \
   클러스터의 개수 `k`를 지정\
   데이터를 무작위로 `k`개의 군집 중심(초기 중심)을 설정
2. 할당(Assignment):\
   각 데이터 포인트를 가장 가까운 군집 중심에 할당\
   "가까움"은 보통 유클리디안 거리(Euclidean Distance)를 사용해 계산
3. 중심 업데이트(Update Centroids)\
   각 클러스터에 할당된 데이터의 평균을 계산하여 새로운 군집 중심을 설정
4. 반복(Iterate)\
   할당과 업데이트 과정을 반복\
   군집 중심이 더 이상 변하지 않거나 지정된 반복 횟수에 도달하면 종료



## 3. K-means의 장, 단점

### 장점

* 간단하고 빠름: 계산 속도가 빠르며 구현이 쉬움
* 확장성: 대규모 데이터 세트에도 적합
* **다양한 응용 가능**: 이미지 압축, 추천 시스템, 고객 세분화 등 다양한 분야에서 사용 가능

### 단점

* k의 설정이 필요: 클러스터 개수를 사전에 알아야 함
* 초기 중심에 민감: 초기 군집 중심 값에 따라 결과가 달라질 수 있음
* 구형 클러스터에 적합: 데이터가 구형(spherical)으로 분포하지 않거나 크기가 다를 경우 성능이 떨어질 수 있음
* 잡음과 이상치에 민감: 데이터의 잡음이나 이상치(outlier)에 취약함














