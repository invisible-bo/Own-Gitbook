---
description: Python의 범위
---

# Python scope

## 이름 검색 규칙(Name resolution)

* python에서 사용되는 name(식별자)들은 이름공간(namespace)에 저장되어 있음



* 아래와 같은 순서로 name을 찾아나가며, LEGB Rule이라고 부름\
  \
  \- Local scope : 지역범위(현재 작업 중인 범위)\
  \
  \- Enclosed scope : 지역범위  한 단계 위 범위\
  \
  \- Global scope : 최상단에 위치한 범위\
  \
  \- Built-in scope : 모든 것을 담고 있는 범위   ex)    print()

### global keyword

* 함수 내부에서 global variable(전역변수)에 접근하거나 값을 변경할 수 있도록 해줌

ex)

```python
counter = 0 # global variable

def count():
    global counter # global variable counter를 사용하겠다고 선언
    print(counter) # 현재 counter 값 print
    counter += 1 # global variable counter값을 1 증가

count() # count 함수 호출 (첫 번째)
count() # count 함수 호출 (두 번째)
print(counter) # global variable counter값을 출력
# 0 
# 1
# 2
```

ex)

```python
a = 0
b = 1

def enclosed(): # 외부 함수
    a = 10
    c = 3
    
    def local(c): # 내부 함수
        print(a, b, c) # 내부에서 접근 가능한 variable 출력
        
    local(300) # 내부 함수 호출
    print(a, b, c) # 외부 함수의 변수 print

enclosed() # 외부 함수 호출
print(a, b) # global variable print
# (10, 1, 300)
# (10, 1, 3)
# (0, 1)
```
