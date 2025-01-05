# Template

## URL

urls.py

```python
# my_first_pjt/my_first_pjt/urls.py

from django.contrib import admin
from django.urls import path
from articles import views

urlpatterns = [
    path("admin/", admin.site.urls),
    path("index/", views.index),
]
```

### View

views.py

```python
from django.http import HttpResponse

def index(request):
	response = HttpResponse("<h1>Hello, Django!</h1>") 
	return response
```

* HttpRequest -> URLs -> View -> Template -> View -> HttpResponse\


render

```html
render(request, template_name, context)
```

***

### Templates System

* 데이터를 보여주는 로직 작성
* Template 기본 경로
  * `app_name / templates`&#x20;

### Django Template Language(DTL)

* Django template에서 사용하는 문법
  * (주의) PYTHON이 동작하는 것이 아님!!
* 데이터를 표현하기 위한 방법
* DTL문법
  * 변수 (Variable)
  * 필터 (Filters)
  * 태그 (Tags)
  * 주석 (Comments)

















