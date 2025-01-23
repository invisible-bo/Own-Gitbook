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

10\.

```python
문제 설명
정수 배열 numbers가 매개변수로 주어집니다. numbers의 원소 중 두 개를 곱해 만들 수 있는 
최댓값을 return하도록 solution 함수를 완성해주세요.
```

```python
def solution(numbers):
    num_list = sorted(numbers)
    return num_list[-1] * num_list[-2]
# 같은 결과값
def solution(numbers):
    numbers.sort()
    return numbers[-1] * numbers[-2]
```

11\.

```
정수 n이 매개변수로 주어질 때 n의 각 자리 숫자의 합을 return하도록 solution 함수를 완성해주세요
```

```python
def solution(n):
    return sum(map(int,str(n)))    
```

```
풀이
코드에서 n을 str로 변환하면 다음과 같은 일이 발생합니다:

정수 n이 문자열로 변환:

str(n)은 정수 n을 문자열로 변환합니다.
예: n = 123 → str(n) = "123".
문자열의 각 문자가 반복 가능한 객체로 다뤄짐:

문자열은 반복 가능한 객체(iterable)로 취급됩니다. 
따라서 str(n)의 각 문자를 하나씩 순회할 수 있습니다.
예: "123"은 문자 "1", "2", "3"로 나뉩니다.
map(int, str(n)):

map(int, str(n))는 문자열의 각 문자를 정수로 변환합니다.
예: "123" → [int('1'), int('2'), int('3')] → [1, 2, 3].
sum()로 합산:

sum() 함수는 map의 결과를 더합니다.
예: [1, 2, 3] → 1 + 2 + 3 = 6.
```

12\.

```
두 배열이 얼마나 유사한지 확인해보려고 합니다. 
문자열 배열 s1과 s2가 주어질 때 같은 원소의 개수를 return하도록 solution 함수를 완성해주세요.
```

```python
def solution(s1, s2):
    common = set(s1) & set(s2)
    return len(common)

def solution(s1, s2):
    return len(set(s1) & set(s2))
```

<pre><code><strong>- &#x26;는 집합 자료형에서 교집합 연산자로 동작한다
</strong><strong>- Python에서 True와 False는 1과 0으로 간주되므로, 
</strong><strong>  &#x26;를 논리 연산에 사용할 수도 있다. 
</strong><strong>  하지만 일반적으로 **and**를 사용하는 것이 더 명확하다.
</strong><strong>  
</strong><strong>  
</strong><strong>  len() 함수를 **집합(set)**에 사용하면, 집합에 포함된 원소의 개수를 반환한다
</strong><strong>  len()을 집합에 사용하면 중복이 제거된 고유한 원소의 개수를 반환
</strong></code></pre>

13\.

중앙값은 어떤 주어진 값들을 크기의 순서대로 정렬했을 때 가장 중앙에 위치하는 값을 의미합니다. 예를 들어 1, 2, 7, 10, 11의 중앙값은 7입니다. 정수 배열 `array`가 매개변수로 주어질 때, 중앙값을 return 하도록 solution 함수를 완성해보세요.

```python
def solution(array):
    array.sort()
    middle_num = len(array)//2  
    return array[middle_num]
    
# 중앙값을 찾기 위해 가장 간단하고 효율적인 방식.
# 배열 인덱스는 0부터 시작하니까, 전체 길이를 반으로 나눈 값이 중앙값의 인덱스가 됨
```



14\.

영어에선 a, e, i, o, u 다섯 가지 알파벳을 모음으로 분류합니다. 문자열 `my_string`이 매개변수로 주어질 때 모음을 제거한 문자열을 return하도록 solution 함수를 완성해주세요.

<pre class="language-python"><code class="lang-python">def solution(my_string):
    return ''.join(char for char in my_string if char not in 'aeiou')
    
# join()은 리스트의 각 요소를 연결하여 문자열을 생성.
# 앞의 ''는 연결할 때 사이에 아무 것도 넣지 않겠다는 뜻.    
<strong># my_string의 각 문자를 순회하며 모음을 제외한 문자만 리스트에 담아.
</strong># 그 리스트를 join()으로 연결해 새로운 문자열을 생성.        
</code></pre>













