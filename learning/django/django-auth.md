# Django Auth

### Auth

<figure><img src="../../.gitbook/assets/image (18).png" alt="" width="375"><figcaption></figcaption></figure>

* `django.contrib.auth`→ 인증 핵심 로직과 관련 기본 모델
* `django.contrib.contenttypes` → 사용자의 모델과 권한을 연결
* 인증(Authentication)과 권한(Authorization)을 합쳐서 Auth라고 대개 인증시스템이라고 명명
  * 인증(Authentication) : 내가 누구인지를 입증하는 것
  * 권한(Authorization) : 수행할 수 있는 자격 여부

***

### Cookie & Session

* http 특징
  * Connectionless(비연결지향)
    * 한 번 요청에 대한 응답을 하면 연결이 끊어짐
  * Stateless(무상태)
    * 연결이 끊어지면 통신이 끝나고 서로를 잊어버림
    * 모든 메세지는 독립적
      * cookie와 세션이 없다면
        * 이전의 요청을 기억하지 못하게 된다

***

1. Cookie

* Server → Web browser에 전달하는 작은 데이터 조각
  * 유저가 웹을 방문하게 되면 서버로부터 쿠키를 전달받음
* Key-Value 형태로 데이터가 저장됨
* 이후 동일한 서버에 보내는 모든 요청에 cookie가 함께 전달
* cookie data는 user의 로컬에 저장되는 정보

***

2. Session

* session은 server와 client간 State(상태)를 기억하기 위한 것

Django의 Session 과 Auth

<figure><img src="../../.gitbook/assets/image (20).png" alt="" width="375"><figcaption></figcaption></figure>

* django에서 알아서 처리해주고 있기 때문에 직접 작성할 필요가 없다

***

### Django의 Authentication System

* 사용자의 인증 및 권한 관리를 위해 제공되는 강력한 내장 시스템(Built-in Form)
* 로그인을 위한 기본적인 form을 제공
* `login()` &#x20;

기본 흐름

1. 사용자가 로그인하면 `authenticate()` 함수가 사용자 자격 증명을 확인
2. 성공적으로 인증되면 `login()` 함수가 호출되어 세션에 사용자 정보가 저장
3. 권한 기반 작업은 `has_perm()`이나 `has_module_perms()`를 통해 확인 가능
4. 로그아웃 시 `logout()` 함수가 호출되어 세션이 종료







