---
description: 컬렉션 자료형
---

# Python collection data types

1. **리스트 (List)**\
   \- 정렬된 데이터의  순서 유지, **가변성**\
   \- 중복 허용\
   \- 인덱스와 슬라이싱 지원

```python
my_list = [1,2,3,"apple",[5,6]]
my_list.append(7) #추가
del my_list[0] #삭제
my_list[1] = 9 #수정
.sort() #오름차순 정렬
.sort(reverse=True) #내림차순 정렬
```



2. **튜플 (Tuple)**\
   \- 정렬된 데이터의 순서 유지, **불변성**\
   \- 중복 **허용**\
   \- 인덱스와 슬라이싱 지원

```python
my_tuple = (1,2,3,"apple")
print(my_tuple[1:3]) #(2,3) 
```

3. **집합 (Set)**\
   \- 순서가 없는 데이터 구조\
   \- 중복 **불허**\
   \- 인덱스 지원하지 않음

```python
my_set = {1, 2, 3, 3, "apple"}  
print(my_set)  # {1, 2, 3, "apple"} 중복 제거됨
my_set.add(4)  # {1, 2, 3, "apple", 4} 추가
```

4. **딕셔너리 (Dictionary)**\
   \- **키-값 쌍**으로 데이터를 저장\
   \- **키** 는 **불변적**, **값**은 **변경** 가능\
   \- 순서를 유지(Python 3.7+)

```python
my_dict = {"name":"bo","age"=35 }
my_dict["name"] # 'bo'
my_dict["age"] # 35
my_dict["city"] = "New York" #새 키:값 추가
```
