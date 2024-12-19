---
description: 조건문
---

# Python Condition

1. **if 문(Statement)**\
   \- 조건이 True일때만 코드 블록 실행

```python
x = 10
if x > 5:
    print("x is greater than 5")
```



2. **if-else문**\
   \- 조건이 True일때와 False일때 각각 다른 코드를 실행

```python
if x > 5:
    print("x is greater than 5")
else:
    print("x is 5 or less")
```



3. **if-elif(else if)-else문**\
   \- 여러 조건을 순차적으로 확인하고, 첫 번째로 True인 조건의 코드를 실행

```python
if x < 5
    print("x is less than 5")
elif x == 5:
    print("x is equal to 5")
else:
    print("x is greater than 5")
```



4. **중첩 조건문**\
   \- 조건문 안에 다른 조건문 포함이 가능

```python
x = 10
if x > 5:
    if x > 20:
        print("x is greater than 5 and less than 20")
```



5. **한줄 조건문**\
   \- if와 else를 한줄로 표현 가능

```python
x = 10
result = "greater" if x > 5 else "smaller"
print(result) #output : "greater"
```





조건 비교 연산자

<table><thead><tr><th width="114">연산자</th><th width="353">의미</th><th>예제</th></tr></thead><tbody><tr><td>==</td><td>값이 같은지 비교</td><td>x == 5</td></tr><tr><td>!=</td><td>값이 다른지 비교</td><td>x ! = 5</td></tr><tr><td>&#x3C;,></td><td>왼쪽 값이 크거나 작은지 비교</td><td>x &#x3C; 5, x > 5</td></tr><tr><td>&#x3C;=,>=</td><td>왼쪽 값이 작거나같은지,  크거나같은지 비교 </td><td>x &#x3C;= 5, x >= 5 </td></tr></tbody></table>





### 논리연산자

-여러 조건을 결합할 때 사용

<table><thead><tr><th width="101">연산자</th><th>의미</th><th>예제</th></tr></thead><tbody><tr><td>and</td><td>모든 조건이 True</td><td>x > 5 and x &#x3C; 15</td></tr><tr><td>or</td><td>하나 이상의 조건이 True</td><td>x &#x3C; 5 or x > 15</td></tr><tr><td>not</td><td>조건의 True/False 반전</td><td>not x > 5 ( x &#x3C;= 5)</td></tr></tbody></table>



{% hint style="info" %}
Pass Statement\
\- 조건문 안에서 실행할 코드를 비워두고 싶다면 pass를 사용
{% endhint %}

ex)

```python
x = 10
if x > 5:
    pass    #아직 미구현한 코드의 경우
```
