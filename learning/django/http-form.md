# HTTP Form

*   `action`과 `method`

    ```
    <form action="/submit/" method="post">
        <label for="username">사용자 이름:</label><br>
        <input type="text" id="username" name="username" required><br>
        
        <label for="email">이메일 주소:</label><br>
        <input type="email" id="email" name="email" required><br>
        
        <label for="password">비밀번호:</label><br>
        <input type="password" id="password" name="password" required><br>
        
        <input type="submit" value="가입하기">
    </form>
    ```
* 데이터를 어디로(action) 어떤 방식(method)를 이용해서 보낼지 결정하는 속성

1. `action`

* 데이터가 전송될 URL을 지정
* 지정하지 않을경우 현재 페이지의 URL로 데이터를 전송

2. `method`

* 데이터를 전송하는 방식(HTTP request method)을 지정
* HTML Form은 `GET` 방식 또는 `POST` 방식으로만 전송이 가능



input 요소

**input**

* form에서 사용자의 입력을 받기 위해 사용
*   `type` 속성에 따라 입력 동작 방식이 달라짐

    → 지정하지 않을경우 `type=text`로 인식
* **데이터 전송에서 핵심 속성은 name**&#x20;
  * `name`으로 서버에 데이터를 전달하고, 서버는 `name`을 보고 데이터를 판단

**name 속성**

* form을 제출(submit)하면 `name`속성에 설정된 값이 서버로 전송
*   서버에서는 `name`속성을 사용하여 값에 접근

    ⇒ 즉, `name`속성이 없다면 서버가 데이터를 받을 수 없다
* `name`속성의 값이 key가 되고, 사용자가 입력한 값이 value가 되어 전송

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

***

HTTP(Hyper Text Transfer Protocol)

* 여러가지 리소스를 보내고 받을 때 사용하는 프로토콜(통신규약) == 약속
* 요청(request)과 응답(response)로 이뤄지는 통신
* 웹에서 이뤄지는 데이터 교환의 기초

HTTP Method

* HTTP에서 수행할 작업을 나타냄
* 특정 자원에 대해 내가 수행하고자 하는 동작을 METHOD로 정의
* GET, POST, PUT, DELETE
  *   GET

      * 특정한 자원을 조회하는데 사용
      * 데이터를 서버로 전송할때 쿼리스트링을 사용해서 전송

      \==URL에 데이터가 포함되어 전송











