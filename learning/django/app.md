# App

### Django App

* 내가 생각하는 하나의 기능 덩어리
* 하나의 project는 여러개의 app이 있을 수 있음
* 하나의 app으로 모두 개발하는 것도 가능

{% hint style="info" %}
Project : 어플리케이션의 집합체

App : 각각의 기능 단위 module
{% endhint %}

### App 사용

1. app 생성

```python
python manage.py startapp {app name} # app의 이름은 복수형 권장
```

1. App 등록

* settings.py로 이동
* INSTALLED\_APPS에 생성한 App 이름등록 + '트레일링 콤마'



### App 살펴보기

`admin.py` : 관리자용 페이지 관련 설

`app.py` : app관련 정보 설정

`models.py` : DB관련 데이터 정의 파일

`tests.py` : test관련 파일

`views.py` : 요청을 처리하고 처리한 결과를 반환하는 파일



