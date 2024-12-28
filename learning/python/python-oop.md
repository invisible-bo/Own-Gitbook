---
description: Object-oriented programming(객체지향프로그래밍)
---

# Python OOP

* Python의 객체 지향 프로그래밍(Object-Oriented Programming, OOP)은 \
  Data를 객체로 모델링하고, 이 객체들 간의 상호작용을 중심으로 프로그램을 설계하는 \
  Programming 패러다임. Python은 객체 지향 언어로, 모든 것이 객체로 구성되어 있다

## Python의 OOP특징

* Dynamic Typing(동적 타이핑):
  * Python에서는 객체의 타입을 runtime에 결정
* 모든 것이 객체(Object):
  * 숫자, 문자열, 함수 등 모든 것이 object로 취급됨

##

## 객체지향프로그래밍의 주요 개념

### 1. Class

* 객체(object)를 생성하기 위한 청사진(설계도), 붕어빵 틀
* class는 속성(data)과 메서드(method, 동작)를 정의한다

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name  # 속성
        self.breed = breed  # 속성

    def bark(self):  # 메서드
        print(f"{self.name} says Woof!")
```

### 2. Object(객체)

* class의 instance로, class에서 정의된 구조를 **실제로** 메모리에 구현한 것, 붕어빵

```python
my_dog = Dog("Buddy", "Golden Retriever")
print(my_dog.name) 
my_dog.bakr() 
# 출력:Buddy
#      Buddy says Woof!
```



### 3. Attributes(속성):

* object(객체)의 데이터를 저장하는 변수
* `__init__` method를 사용하여 object가 생성될 때 속성을 초기화 한다



### 4. Method:

* 객체의 동작(function)으로, class 내부에서 정의된 함수
* 첫 번째 매개변수로 `self` 를 사용하여 현재 object(객체)를 참조



### 5. Encapsulation(캡슐화):

* data를 보호하고 객체 외부에서 직접 접근하지 못하도록 속성을 숨기는 것
* python에서는 변수명 앞에 밑줄(`_` or `__`)를 붙여 이를 나타냄



### 6. Inheritance(상속):

* 기존 class를 확장하여 새로운 class를 만드는 기능
* '부모 class'의 속성과 메서드를 '자식 class'가 상속받음

```python
class Animal:
    def speak(self):
        print("Animal speaks")
        
class Dog(Animal):
    def speak(self):
        print("Dog barks")
        
dog = Dog()
dog.speak()
# 출력 : Dog barks
```









