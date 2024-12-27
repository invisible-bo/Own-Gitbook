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















