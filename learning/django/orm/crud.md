---
description: Create, Read, Update, Delete
---

# CRUD

* Django의 ORM(Object-Relational Mapping)과 함께 쉽게 구현



### 1. Create (생성)&#x20;

* 데이터베이스에 새로운 레코드를 추가하는 작업

방법:

* 모델 객체 생성: Django 모델 클래스를 사용하여 데이터를 생성하고 저장

```python
from myapp.models import MyModel

# 데이터 생성 및 저장
new_entry = MyModel(field1="value1", field2="value2")
new_entry.save()
```

* 폼 사용: 사용자 입력 데이터를 통해 객체를 생성

```python
from myapp.forms import MyModelForm

def create_view(request):
    if request.method == "POST":
        form = MyModelForm(request.POST)
        if form.is_valid():
            form.save()  # 데이터 저장

```

***

### 2. Read (읽기)

* 데이터베이스에서 데이터를 조회하는 작업

방법:&#x20;

* 전체 데이터 조회

```python
all_entries = MyModel.objects.all()
```

* 특정 조건으로 조회

```python
filtered_entries = MyModel.objects.filter(field1="value1")
```

* 단일 데이터 조회

```python
single_entry = MyModel.objects.get(id=1)
```

* 템플릿에 데이터 전달

```python
from django.shortcuts import render

def list_view(request):
    entries = MyModel.objects.all()
    return render(request, "list.html", {"entries": entries})
```

***

### 3. Update (수정)

* 기존 데이터를 수정하는 작업

방법:

* 객체 조회 후 수정

```python
entry = MyModel.objects.get(id=1)
entry.field1 = "new value"
entry.save()
```

* 폼 사용

```python
from django.shortcuts import get_object_or_404

def update_view(request, pk):
    entry = get_object_or_404(MyModel, pk=pk)
    if request.method == "POST":
        form = MyModelForm(request.POST, instance=entry)
        if form.is_valid():
            form.save()
    else:
        form = MyModelForm(instance=entry)
    return render(request, "update.html", {"form": form})
```

***

### 4. Delete (삭제)

* 데이터베이스에서 데이터를 삭제

방법:

* 단일 객체 삭제

```python
entry = MyModel.objects.get(id=1)
entry.delete()
```

* 뷰에서 삭제 처리

```python
from django.shortcuts import get_object_or_404, redirect

def delete_view(request, pk):
    entry = get_object_or_404(MyModel, pk=pk)
    if request.method == "POST":
        entry.delete()
        return redirect("list_view")
    return render(request, "delete_confirm.html", {"entry": entry})
```

















