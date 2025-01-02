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

| 용어         | 설명                   |
| ---------- | -------------------- |
| class      | 제품의 설계도              |
| object(객체) | 설계도로 만든 제품           |
| 속성         | class 안의 변수          |
| method     | class안의 함수           |
| 생성자        | object를 만들 때 실행되는 함수 |
| 인스턴스       | 메모리에 살아있는 object     |

* Class 클래스이름:\
  &#x20;   def 매서드이름(self):\
  &#x20;       명령블록
* 객체 = 클래스이름()\
  객체.메서드()

```python
class Monster:
    def say(self):
        print("I am monster")

shark = Monster()
shark.say()
# I am monster
```



* 속성추가

```python
class Monster:
    def __init__(self, name):
        self.name = name
    def say(self):
        print(f"나는 {self.name}")
        
shark = Monster("상어")
shark.say()
```







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

{% hint style="info" %}
\_\_로 시작하는 method == magic method
{% endhint %}



### 4. Method:

* 객체의 동작(function)으로, class 내부에서 정의된 함수
* 첫 번째 매개변수로 `self` 를 사용하여 현재 object(객체)를 참조



### 5. Encapsulation(캡슐화):

* data를 보호하고 객체 외부에서 직접 접근하지 못하도록 속성을 숨기는 것
* python에서는 변수명 앞에 밑줄(`_` or `__`)를 붙여 이를 나타냄
* 데이터와  함수를 캡슐 안에 넣는것.  캡슐은 class를 의미한다&#x20;
* 코드가 좀 더 구조화되고, 함수나 메서드가 인수를 취할 필요가 없어짐



### 6. Inheritance(상속):

* 기존 class를 확장하여 새로운 class를 만드는 기능
* '부모 class'의 속성과 메서드를 '자식 class'가 상속받음
* 자식 class가 부모 class의 속성을 모두 가지고 추가적으로 다른 속성을 가진다는 뜻

```python
# 부모 class 정의
class Animal:
    def __init__(self, name):
        self.name = name
    def speak(self):
        return "this animal makes a sound"
        
# 자식 class 1
class Dog(Animal):
    def speak(self):
        return f"{self.name} says Woof!"
# 자식 class 2
class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow!"
    
# 객체 생성 및 사용
dog = Dog("Buddy")
cat = Cat("Kitty")

print(dog.speak())  # Buddy says Woof!
print(cat.speak())  # Kitty says Meow!
```

`Animal` class는 `name` 속성과 `speak` 메서드를 가지고 있음

`Dog` 와 `Cat` class는 `Animal` 을 상속 받으며 `speak` 메서드를 각각 자신만의 방식으로\
재정의(override)함

각 자식 class의 instance를 생성하여 고유한 `speak` 메서드 동작을 확인



### 7. Abstraction(추상화):

* 복잡한 시스템에서 필요한 정보만을 드러내고 불필요한 세부 사항은 감추는 것
* 코드의 복잡성을 줄이고, 사용자가 필요한 기능에만 집중할 수 있도록 도움



### 8. Polymorphism(다형성,  여러개의 형태):

* 같은 인터페이스(또는 메서드)를 사용하지만, 객체에 따라 다른 동작을 수행할 수 있는 능력

주요특징

1. 동일한 인터페이스, 다른 동작:\
   동일한 메서드 이름이지만, 객체의 종류에 따라 메서드가 다른 방식으로 동작 \
   &#x20; ex) speak() 메서드는 개(Dog)에서는 "Woof!"를, 고양이(Cat)에서는 "Meow!"를 출력
2. 유연성과 확장성:\
   새로운 class가 추가되더라도 기존 코드를 수정하지 않고 쉽게 확장\
   부모 클래스나 인터페이스로 작업하면, 객체가 어떤 하위 클래스인지 몰라도 동일한 방식으로 \
   사용할 수 있다













