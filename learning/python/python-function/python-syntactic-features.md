---
description: 문법적 기능, 코드 작성 방식
---

# Python Syntactic Features

* ## List comprehension
* 기존 리스트나 이터러블 객체에서 조건에 맞는 새로운 리스트를 **짧고 간결한 방식으로 생성**할 수 있는 파이썬 문법
* 반복문과 조건문을 한 줄로 작성하여, 기존 리스트나 이터러블 객체에서 새로운 리스트를 생성하는 데 사용

```python
[<expression> for <item> in <iterable> if <condition>]
# <expression>: 각 요소에 적용할 표현식(변환 또는 계산).
# <item>: 반복문에서 사용하는 변수.
# <iterable>: 반복 가능한 객체(리스트, 튜플, 문자열 등).
# <condition> (선택 사항): 요소를 필터링하기 위한 조건.
```

ex)

```python
numbers_str = ["1","2","3","4","5"]
numbers_int=[int(number) for number in numbers_str]
print(numbers_int)  
# for number in numbers_str: for문ㅁ-list의 각 요소를 하나씩 순회
# int(number): str을 int형으로 형변환
# 출력: [1, 2, 3, 4, 5]
```

해당 코드를 list comprehension없이 작성

```python
numbers_int = []
for number in numbers_str:
    numbers_int.append(int(number))
```



* ## Map

