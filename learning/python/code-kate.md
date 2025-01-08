---
description: practice
---

# \*Code kate

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

3\.

```
문제 설명
영어에선 a, e, i, o, u 다섯 가지 알파벳을 모음으로 분류합니다. 
문자열 my_string이 매개변수로 주어질 때 모음을 제거한 
문자열을 return하도록 solution 함수를 완성해주세요.

제한사항
my_string은 소문자와 공백으로 이루어져 있습니다.
1 ≤ my_string의 길이 ≤ 1,000
```

```python
def solution(my_string):
    vowels = "aeiou"
    if 1 <= len(my_string) <= 1000:
        return ''.join(char for char in my_string if char not in vowels)

# join()은 리스트 []의 요소를 하나씩 가져옴
# 각 요소를 빈 문자열 ''로 연결
# char는 my_string에 있는 각 개별 문자를 순회(iterate)하며 나타나는 변수
# 문자 순회: for char in my_string는 my_string의 각 문자를 하나씩 가져옴
# 필터링: 조건문 if char not in vowels를 통해 
# char가 모음(a, e, i, o, u)에 속하지 않을 때만 처리
# for char in my_string:
   #  if char not in vowels:
     #    print(char)
```

4\.

```
문자열 my_string과 정수 n이 매개변수로 주어질 때, my_string에 
들어있는 각 문자를 n만큼 반복한 문자열을 return 하도록 solution 함수를 완성해보세요.

제한사항
2 ≤ my_string 길이 ≤ 5
2 ≤ n ≤ 10
"my_string"은 영어 대소문자로 이루어져 있습니다.
```

```python
def solution(my_string, n):
    if 2 <= len(my_string) <= 5 and 2 <= n <= 10:
        return ''.join(char * n for char in my_string)
```



5\.

```
문제 설명
어떤 세균은 1시간에 두배만큼 증식한다고 합니다. 처음 세균의 마리수 n과 경과한 
시간 t가 매개변수로 주어질 때 t시간 후 세균의 수를 return하도록 solution 함수를 완성해주세요.

제한사항
1 ≤ n ≤ 10
1 ≤ t ≤ 15

```

```python
def solution(n, t):
    if 1 <= n <= 10 and 1 <= t <= 15:
        return n * (2**t)
```

6\.

```
문제 설명
문자열 my_string이 매개변수로 주어질 때, 대문자는 소문자로 
소문자는 대문자로 변환한 문자열을 return하도록 solution 함수를 완성해주세요.

제한사항
1 ≤ my_string의 길이 ≤ 1,000
my_string은 영어 대문자와 소문자로만 구성되어 있습니다.
```

```python
def solution(my_string):
    return my_string.swapcase()
```

{% hint style="info" %}
swapcase() : 이 메서드는 대문자를 소문자로, 소문자를 대문자로 변환
{% endhint %}

7\.

```
문제 설명
정수 리스트 num_list가 주어질 때, 첫 번째로 나오는 음수의 인덱스를 
return하도록 solution 함수를 완성해주세요. 음수가 없다면 -1을 return합니다.

제한사항
5 ≤ num_list의 길이 ≤ 100
-10 ≤ num_list의 원소 ≤ 100
```

```python
def solution(num_list):
    if 5 <= len(num_list) and all(-10 <= num <= 100 for num in num_list):
        for inx, num in enumerate(num_list):
            if num < 0:
                return inx
        return -1    
```

8\.

```
문제 설명
정수 배열 arr와 자연수 k가 주어집니다.

만약 k가 홀수라면 arr의 모든 원소에 k를 곱하고, k가 짝수라면 arr의 모든 원소에 k를 더합니다.

이러한 변환을 마친 후의 arr를 return 하는 solution 함수를 완성해 주세요.
```

```python
def solution(arr, k):
    if k % 2 == 0:
        return [x + k for x in arr]
    else:
        return [x * k for x in arr]
```

9\.

```
문제 설명
정수 배열 arr가 주어집니다. arr의 각 원소에 대해 값이 50보다 크거나 같은 짝수라면 2로 나누고,
50보다 작은 홀수라면 2를 곱합니다. 
그 결과인 정수 배열을 return 하는 solution 함수를 완성해 주세요.
```

```python
```



