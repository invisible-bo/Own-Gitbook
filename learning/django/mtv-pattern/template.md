# Template

### Templates System

* 데이터를 보여주는 로직 작성
* Template 기본 경로
  * `app_name / templates`&#x20;

### 앱 내부 구조의 권장 규칙

```
articles/
├── templates/
│   └── articles/
│       └── index.html
```

* **앱 간의 템플릿 이름 충돌**을 방지하기 위해서
  * views.py에서 articles/index.html로 위치를 명시해주어야 함

```python
from django.shortcuts import render

def index(request):
    return render(request, 'articles/index.html')
```

***

### Django Template Language(DTL)

* Django template에서 사용하는 문법
  * (주의) PYTHON이 동작하는 것이 아님!!
* 데이터를 표현하기 위한 방법
* DTL문법
  * **변수 (Variable)**
    * **\{{ variable \}}**
  * 필터 (Filters)
    * \{{ variable|filter \}}
    * 변수에 작업을 추가적으로 더해 수정하고 싶을때 사용
  * **태그 (Tags)**
    * **\{% tag %\}**
    * 반복 또는 논리를 수행하여 제어 흐름을 만들거나 특수한 기능을 수행
    * ex) \{% if \~ %\} \
      &#x20;      \{% endif %\}
  * 주석 (Comments)
    * {# 한줄주석#}
    * \{%  comment %\}\
      여러줄\
      주석\
      \{% endcomment %\}

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

***

### Template Inheritance(템플릿  상속)

* Django는 템플릿 상속을 지원
* 코드의 재사용성, 상위 템플릿에 공통이 될 부분을 정의하고\
  하위 템플릿에서 달라질 부분을 Block으로 만드는 Skeleton형태

`{% block block_name %}`&#x20;

`{% endblock block_name %}`&#x20;

* 상위 템플릿에서 하위 템플릿 마다 달라질 부분을 정의



`{% extends 'template_name' %}`&#x20;

* 하위 템플릿에서 상위 템플릿을 상속해서 확장한다는 것&#x20;
* 템플릿의 가장 최상단에 위치해야함
* 다중 상속을 지원하지 않음

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>













