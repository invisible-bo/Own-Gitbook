---
description: practice
---

# Code kate

1\.

```
문제 설명
정수가 담긴 리스트 num_list가 주어집니다. num_list의 홀수만 순서대로 이어 붙인 수와 짝수만 
순서대로 이어 붙인 수의 합을 return하도록 solution 함수를 완성해주세요.

제한사항
2 ≤ num_list의 길이 ≤ 10
1 ≤ num_list의 원소 ≤ 9
num_list에는 적어도 한 개씩의 짝수와 홀수가 있습니다.
```

```python
def solution(num_list):
    odd = ""  # 홀수를 이어 붙일 문자열
    even = ""  # 짝수를 이어 붙일 문자열

    for num in num_list:  # 리스트의 각 요소를 하나씩 가져옴
        if num % 2 == 0:  # 짝수 확인
            even += str(num)
        else:  # 홀수 확인
            odd += str(num)

    return int(odd) + int(even)  # 연결한 문자열을 정수로 변환 후 합산

```

2\.

```python
def solution(a, b, flag):
    if -1000 <= a <= 1000 and -1000 <= b <= 1000:
        if flag == true:
            return a + b
        else:
            return a - b

==
def solution(a, b, flag):
    return a + b if flag else a - b
```
