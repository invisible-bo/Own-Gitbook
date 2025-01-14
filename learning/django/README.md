---
icon: user-bounty-hunter
description: Django Framework
---

# Django

### Framework

* software 개발을 위한 구조적인 틀
  * 자주 사용하는 여러 도구를 모아놓은 것
  * 코드 뭉치(ex: Django, Flask, FastAPI)
* 생산성이 높아짐
* 부가적인 부분은 Framework에 맡기고, 핵심 로직에만 집중
* 구조적으로 안정적인 형태로 개발 가능

### Django Framework

* Python을 이용해서 web개발
* 빠른 web개발을 위한 모든 것이 준비되어 있음
* DRY(Don't Repeat Yourself)원칙
  * code 중복을 최소로 하는 개발 원칙을 따름
  * 다 갖춰진 Framework&#x20;
    * 보안, 관리자 기능, Auth 등
* 풍부한 레퍼런스
  * Google참조. 모든 Error는 이미 해결되어있다.
* 검증된 Framework
  * Spotify, Instagram, Dropbox, Toss 등등

***

### Install Django&#x20;

```bash
pip install django==4.2
```

{% hint style="info" %}
pip freeze > requirements.txt    #pip list 저장

pip install -r requirements.txt   #pip list install
{% endhint %}

***

### Django Project

* Django는 Project단위로 움직인다
* project를 만든다 == 하나의 프로그램을 만들기 시작한다

project 생성

```bash
django-admin startproject <project이름> <생성위치> # 생성위치 생략하면 현재 위치에 폴더 생성
django-admin startproject <project이름> . # 현재 폴더를 프로젝트 폴더로 사용해서 생성
```

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* `settings.py` : project의 설정 관리
* `urls.py` : 어떤 요청을 처리할지 결정하는 곳
* `__init__.py` : 하나의 폴더를 하나의 python 패키지로 인식하도록 하는 파일
* `wsgi.py` : 웹 서버 관련 설정 파일
* `manage.py` : django project 유틸리티(프로젝트 조종기)





