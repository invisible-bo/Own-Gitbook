---
description: 데이터를 모아 놓은 전체 집합
---

# Dataset

* 여러 개의 Feature와 Label(Target)으로 구성\
  ex) 머신러닝에서의 CSV 파일, database table, 이미지 폴더 등

ex)

```markdown
| Age | Height | Weight | Gender (Target) |
|-----|--------|--------|-----------------|
| 25  | 170    | 65     | Male            |
| 30  | 160    | 55     | Female          |
```



### 1.  Feature (특징)

* 데이터셋에서 모델 학습에 사용되는 개별적인 속성 또는 열(column)
* 데이터셋의 한 부분으로, 예측을 위해 입력으로 사용
* 입력 변수(Input Variable)라고도 함
* 위 dataset에서 `age` `Height` `Weight` 는 모두 Feature(column)



### 2. Label(레이블)



* 학습 데이터셋에서 Feature(입력 데이터)에 대응되는 정답 또는 목표 값
* 지도 학습(supervised learning)에서는 레이블이 반드시 필요하며, \
  모델은 Feature와 Label 간의 관계를 학습
* 학습 후, 새로운 Feature가 주어지면 그에 맞는 Label을 예측
* 종류\
  \- 분류 문제(Classification): Label은 이산적인 값(카테고리)을 가진다\
  &#x20;   ex) 스팸 메일 분류 (스팸/스팸 아님), 숫자 인식 (0\~9)\
  \
  \- 회귀 문제(Regression): Label은 연속적인 값(숫자)을 가진다\
  &#x20;   ex) 주택 가격 예측, 온도 예측

