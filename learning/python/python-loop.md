---
description: 반복문
---

# Python Loop

* ## For loop

```python
for i in range(5):
    print(i)
# 0, 1, 2, 3, 4
```

ex)

```python
for i in my_dict.key():
# my_dict의 key를 반환
for i in my_dict.value():
# my_dict의 value를 반환
for i in my_dict.items():
# my_dict의 모든 (key, value) 쌍을 tuple로 반환
for key, value in my_dict.items():
    print(f"Key: {key}, Value: {value}")
# items()는 각 반복에서 (key, value) 튜플을 반환하므로
# 이를 두 개의 변수로 나눠 받을 수도 있다
```

{% hint style="info" %}
`range:`일정한 범위의 숫자 시퀀스를 생성하는 Python의 내장 함수

```python
range(start, stop, step)
```

* `start` (선택 사항): 숫자 시퀀스의 시작 값. 기본값은 `0`.
* `stop` (필수): 숫자 시퀀스가 끝나는 위치(해당number포함 X)
* `step` (선택 사항): 숫자 간의 간격. 기본값은 `1`.

```python
for i in range(5):  # range(0, 5)로 해석
    print(i) # 0,1,2,3,4
```
{% endhint %}

!) range의 개념을 while로  구현&#x20;

```python
i = 0
while i < 5:
    print(i)
    i += 1
# 0, 1, 2, 3, 4
```



*   ## While loop

    조건이 True인  동안 무한 반복

```python
count = 0
while count < 5:
    count += 1  
    print(count) 
# 1, 2, 3, 4, 5
```



### While loop에서 자주 쓰이는 code

#### break

```python
count = 0
while True:  # 무한 반복
    count += 1
    print(count)
    if count >= 5:  # 특정 조건이 만족되면 반복문 종료
        break
# 1, 2, 3, 4, 5
```



#### continue

```python
count = 0
while count < 5:
    count += 1
    if count == 3:
        continue  # 3은 건너뛰고 다음 반복으로 이동
    print(count)
# 1, 2, 4, 5
```



#### else

while 반복문이 정상적으로 종료되었을 때(즉, break에 의해 중단되지 않았을 때) 실행

```python
count = 0
while count < 5:
    print(count)
    count += 1
else:
    print("Loop finished successfully.")    
# 0, 1, 2, 3, 4 
# Loop finished successfully.
```



#### input

동적 사용자 입력을 처리할 때 유용

```python
while True:
    command = input("Enter a command ('quit' to stop): ").lower()
    if command == 'quit':
        print("Goodbye!")
        break
    print(f"You entered: {command}")
```

```python
ex)
while True:
    command = input("Enter a command ('quit' to stop): ").lower()
    if command == 'quit':
        print("Goodbye!")
        break
    else:
        print("다시 입력하세요")
        continue #명시적으로 사용. continue가 없어도 while루프라서 반복됨
```

#### time.sleep

루프에서 일정시간 대기

```python
import time

count = 0
while count < 5:
    print(f"Count: {count}")
    time.sleep(1)  # 1초 대기
    count += 1
```



#### try-except

`try` 안에 문제가 발생할 가능성이 있는 코드를 넣는다.

`except` 에서 예외 상황을 처리한다.

```python
while True:
    try:
        number = int(input("Enter a number: "))  # 숫자가 아닌 값 입력 시 예외 발생
        print(f"You entered: {number}")
        break  # 올바른 숫자를 입력하면 루프 종료
    except ValueError:  # 숫자가 아닌 값 입력 시 실행
        print("Invalid input! Please enter a valid number.")
```

