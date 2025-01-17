# Django Project

## Django 개발 순서

1. project 및 app 생성 &#x20;

```python
# 프로젝트 생성
django-admin startproject project_name
# 앱 생성
python manage.py startapp app_name
```

* 생성한 앱을 `settings.py`의 `INSTALLED_APPS`에 등록

***

2. 모델(Model) 설계

* 데이터베이스에 저장할 구조를 정의
* 예: `models.py`에서 테이블 정의

```python
from django.db import models

class ExampleModel(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
```

* 모델 작성 후 마이그레이션 파일 생성

```python
python manage.py makemigrations
```

* 데이터베이스에 적용

```python
python manage.py migrate
```

***

3. 관리자 사이트(Admin) 설정

* `admin.py`에 모델 등록

```python
from .models import ExampleModel

admin.site.register(ExampleModel)
```

* 관리자 계정 생성

```python
python manage.py createsuperuser
```

* 관리자 사이트를 통해 데이터를 확인하고 관리

***

4. 뷰(View) 작성

* `views.py`에 로직 작성
* 예: 특정 데이터를 가져오는 함수형 뷰

```python
from django.shortcuts import render
from .models import ExampleModel

def example_view(request):
    data = ExampleModel.objects.all()
    return render(request, 'example.html', {'data': data})
```

***

5. 템플릿(Template) 작성

* HTML 템플릿 작성
  * `app_name/templates/app_name/example.html`에 HTML 파일 생성
  * 템플릿에서 데이터를 표시

```python
<ul>
    {% raw %}
{% for item in data %}
    <li>{{ item.name }} - {{ item.description }}</li>
    {% endfor %}
{% endraw %}
</ul>
```

***

6. URL 설정

* 프로젝트 레벨 `urls.py`와 앱 레벨 `urls.py`에서 URL 매핑 설정
* app\_name/urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    path('example/', views.example_view, name='example'),
]
```

* project\_name/urls.py

```python
from django.urls import include, path

urlpatterns = [
    path('app_name/', include('app_name.urls')),
]
```

***

7. 정적 파일 및 미디어 파일 설정

* 정적 파일 (`static/`)과 미디어 파일 (`media/`) 경로 설정
* 정적 파일 서빙 테스트

```python
python manage.py collectstatic
```

***

8. 테스트 작성

* 각 앱별로 `tests.py`에 유닛 테스트 작성
* 명령어로 테스트 실행

```python
python manage.py test
```

***

9. 배포 준비

* `DEBUG` 설정 변경, `ALLOWED_HOSTS` 지정
* WSGI 서버 사용 (예: Gunicorn, uWSGI).
* 웹 서버와 연결 (예: Nginx, Apache)





