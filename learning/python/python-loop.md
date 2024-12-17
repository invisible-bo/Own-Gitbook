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

