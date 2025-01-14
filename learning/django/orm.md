# ORM

### ORM

* Object-Relational-Mapping(객체-관계형-맵)
* SQL안쓰고 python으로 데이터베이스 조작할 수 있음

장점

* SQL잘 알지 못해도 DB조작 가능
* SQL을 알아도 기존의 복잡한 쿼리문 작성 없이 객체 지향적인 접근 가능
* SQL을 잘 사용하지 못한다면 ORM이 변환해주는 것이 더 빠름
* 생산성 높음

단점

* ORM에서 지원하지 않는 쿼리라면 직접 작성해야 함
* 서비스가 커질수록 ORM만으로는 한계가 있을 수 있음
* 매우 효율적인 SQL을 작성하고 싶다면 ORM이 불편할 수 있음

***

### Database API

* Database를 쉽게 사용할 수 있게 하는  도구
* Database-abstraction-API(데이터베이스 추상화 API)
* 쉽게말해 Django ORM으로 Database API를 사용해서 데이터베이스를 조작

### \*\*Manager\*\*

* Model 클래스를 생성하면 Django는 자동적으로 CRUD(Create, Read, Update, Delete) \
  할 수 있는 Database API를 제공
* 집사를 한명 붙여주는데 그게 바로 Manager
  * 정식 이름은 Django ORM Manager인데 하는일은 우리가 작성한 모델 클래스를 이용하여\
    데이터베이스 쿼리작업을 도와주는 역할
* 우리는 Manager를 이용해서 Django ORM의 Queryset API를 사용하게 될 것
  * Querset == ORM을 사용해서 데이터베이스로부터 전달받은 객체
* 이 Manager의 기본(default)이름은 `objects`

## \*\*MyModel.objects.all()\*\*

* Model Class.Manager.QuerysetAPI

***

Django Shell

* Django가 제공하는 여러가지 기능을 명령어로 입력해서 실행해볼 수 있는 Shell 환경
* `python manage.py shell` : 현재 Django 프로젝트 환경을 Shell로 접글할 수 있게 해줌

Shell 관련 package

* django-extensions
  * Django 기본 Shell보다 더 많은 기능이 있는 shell\_plus를 제공

```python
pip install django-extensions
```



* ipython
  * python 기본 shell에 여러가지 기능을 더한것
  * 자동완성, 코드 색상 강조...

```python
pip install ipython
```



