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





