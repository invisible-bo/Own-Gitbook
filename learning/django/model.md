# Model

### Django Model

* 저장할 데이터에 대한 필드와 동작들을 포함한 데이터베이스 구조 (layout)
* Django는 Model을 이용해서 데이터를 조작
* 일반적으로 하나의 Model은 하나의 데이터베이스 테이블을 의미



#### 쿼리(Query)

* 데이터베이스를 조작할 수 있는 언어

#### 스키마(Schema)

* 데이터베이스의 구조, 관계 등을 정의한 것

#### 데이터베이스 기본 구조

| **User\_ID** | **Name** | **Email**                                   | **Address** |
| ------------ | -------- | ------------------------------------------- | ----------- |
| 1            | John Doe | [john@example.com](mailto:john@example.com) | 123 Main St |
| 2            | Jane Doe | [jane@example.com](mailto:jane@example.com) | 456 Elm St  |

* 테이블(Table)
* 기본키, PK(Primary Key)
* 열(Column)
* 행(Row)

***

#### **Model 작성**

1. `models.py`
   * ```python
     from django.db import models

     class Article(models.Model):
         pass
     ```
   * `models.Model`을 상속받아서 사용하고자 하는 데이터 스키마를 정의
   * 모든 모델은 `models.Model`의 서브 클래스로 표현
2. 필드 추가하기
   * ```python
     from django.db import models

     class Article(models.Model):
         title = models.CharField(max_length=50)
         content = models.TextField()
     ```
   * 각각의 필드는 테이블의 컬럼
   * 필드의 타입에 따라 사용하며, 각 필드별로 필요한 옵션들이 존재



