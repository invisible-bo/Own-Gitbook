---
description: '메서드 : 특정 객체와 연관된 함수'
---

# Etc functions and method

`all` 함수 : 모든 조건이 True인지 확인

`count` 메서드 : Python의 리스트(List) 객체가 제공하는 내장 메서드. \
특정 값이 리스트에 몇 번 나타나는지 세어주는 기능

ex)&#x20;

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

```python
def solution(array, n):
    if 1 <= len(array) <= 100 and all(0 <= element <= 1000 for element in array) and 0 <= n <= 1000:
        return array.count(n)
```

`replace` : 문자열에서 특정 부분 문자열을 다른 문자열로 대체하는 Python의 문자열 메서드

```python
string.replace(old, new[, count]) 
```

* **`old`**: 교체하고 싶은 문자열(찾을 문자열).
* **`new`**: `old`를 대체할 문자열.
* **`count`** _(선택적)_: 교체를 수행할 최대 횟수. (생략하면 모든 `old`를 `new`로 교체)

***

```python
# 최대값
def 최대값(x):
    result = max(x)
# 최소값    
def 최소값(x):
    result = min(x)
    
# 범위
def 범위():
    i = range(3)
    print(list(i))
    
    j = range(2,6)
    print(list(j))
    
    k = range(2,6,1)
    print(list(k))
    
# 길이 확인 함수
def 길이(x):
    result = len(x)  #리스트, 튜플, 문자열 길이
    print("list의 길이: ", result)
    
# 정렬 함수
randomList = [5, 8, 2, 0, 6, -4, 7, -1, 45, 3, 3]
def 정렬(x):
    result = sorted(randomList) #새로운 list를 뽑을 때
    print("정렬된 list: ", result)

# 역순
def 역순(x):
    result = list(reversed(randomList))
    print("역순된 list: ", result)
    

# 데이터 엮어서 사전으로 또는 list로 만들기
xlist = ['a', 'b', 'c']
ylist = [1, 5, 8]
def 엮어(x, y):
    result = dict(zip(x, y))
    print("엮인 데이터: ", result)
# 엮어(xlist, ylist)

# 문자열분리(sampleText_en)
# 문자열분리(sampleText_ko)
sampleText_en = "Hello my AI9 people! "
sampleText_ko = "모두 킹같이 메킹리크리스마스! 킹받아라! "

def 문자열분리(x):
    result = x.split()
    print("분리된 문자열: ", result)



def 특정문자변환(x):
    result = x.replace('킹','')
    print("특정 문자가 제거됨: ", result)
# 특정문자변환(sampleText_ko)
```

***

`enumerate` : 반복 가능한 객체(iterable)를 순회할 때, 인덱스(index)와 해당 값(value)을 \
&#x20;                          동시에 가져오는 메서드

```python
enumerate(iterable, start=0)
iterable: 반복 가능한 객체(예: 리스트, 문자열, 튜플 등)
start: 인덱스를 시작할 값(기본값은 0)
각 반복에서 (index, value) 형태의 튜플이 반환
```

ex)

```python
text = "hello"
for idx, char in enumerate(text):
    print(f"Character at index {idx}: {char}")
# Character at index 0: h
# Character at index 1: e
# Character at index 2: l
# Character at index 3: l
# Character at index 4: o
```

***

## List comprehension

* 기존 리스트나 이터러블 객체에서 조건에 맞는 새로운 리스트를 **짧고 간결한 방식으로 생성**할 수 있는 파이썬 문법
* 반복문과 조건문을 한 줄로 작성하여, 기존 리스트나 이터러블 객체에서 새로운 리스트를 생성하는 데 사용

```python
[표현식 for 요소 in 반복가능한객체 if 조건식]
ex)
numbers = [x for x in range(5)]
print(numbers)
# 출력: [0, 1, 2, 3, 4]

evens = [x for x in range(10) if x % 2 == 0]
print(evens)
# 출력: [0, 2, 4, 6, 8]
```

***

## Map

**함수**와 **이터러블(반복 가능한 객체)**&#xC744; 입력으로 받아, \
이터러블의 각 요소에 함수를 적용한 결과를 반환하는 함수

* 기본구조

```python
map(함수, 이터러블)
```

* `함수`: 이터러블의 각 요소에 적용할 함수
* `이터러블`: 리스트, 문자열, 튜플 등 반복 가능한 객체

1. 반복가능한 객체의 요소를 하나씩 꺼냄
2. 함수에 집어넣고 결과를 돌려줌
3. 결과를 모아서 새로운 객체를 만

***

## 문자열 관련 함수

1. **`lower()`**
   * 문자열을 모두 소문자로 변환.
   * 예: `"Hello".lower()` → `"hello"`
2. **`upper()`**
   * 문자열을 모두 대문자로 변환.
   * 예: `"hello".upper()` → `"HELLO"`
3. **`swapcase()`**
   * 대문자는 소문자로, 소문자는 대문자로 변환.
   * 예: `"Hello World".swapcase()` → `"hELLO wORLD"`
4. **`capitalize()`**
   * 문자열의 첫 글자를 대문자로 변환하고, 나머지는 소문자로 변환.
   * 예: `"hello world".capitalize()` → `"Hello world"`
5. **`title()`**
   * 각 단어의 첫 글자를 대문자로 변환.
   * 예: `"hello world".title()` → `"Hello World"`









