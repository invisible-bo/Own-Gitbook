---
icon: html5
description: HyperText Markup Language
---

# HTML

### 1. HTML 기본구조

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>문서 제목</title>
</head>
<body>
    <h1>안녕하세요!</h1>
    <p>HTML 문법을 배우는 중입니다.</p>
</body>
</html>
```

* `<!DOCTYPE html>`: HTML5 문서를 선언.
* `<html>`: HTML 문서의 루트 요소.
* `<head>`: 문서 정보를 포함(메타데이터, 제목 등).
* `<body>`: 화면에 표시될 콘텐츠를 포함.

***

### 2. HTML 태그



* 제목 태그 : 제목을 표시할 때 사용. 숫자가 작을수록 글자가 커짐

```html
<h1>제목 1</h1>
<h2>제목 2</h2>
<h3>제목 3</h3>
```



* 문단 태그 : 본문 텍스트를 작성할 때 사용

```html
<p>이 문장은 문단 안에 작성된 텍스트입니다.</p>
```



* 링크 태그 : 다른 페이지나 URL로 이동하는 링크를 생성

```html
<a href="https://example.com">여기로 이동</a>
```



* 이미지 태그 : 이미지를 삽입할 때 사용. 닫는 태그가 필요 없고, `src` 속성으로 이미지 경로를 지정

```html
<img src="image.jpg" alt="이미지 설명" width="300">
```



* 목록 태그 : 순서 없는 목록

```html
<ul>
    <li>항목 1</li>
    <li>항목 2</li>
</ul>
```



* 목록 태그 : 순서 있는 목록

```html
<ol>
    <li>첫 번째</li>
    <li>두 번째</li>
</ol>
```



* 버튼 태그 : 버튼을 만들 때 사용

```html
<button>클릭하세요</button>
```



* 주석

```html
<!-- 이 부분은 주석입니다. -->
```

***

### 3. HTML 속성

* HTML 태그에 추가적인 정보를 제공. 주요 속성 예:



* `id`: 요소의 고유 식별자

```html
<p id="unique">이 문단은 고유 ID를 가집니다.</p>
```



* `class`: 여러 요소에 공통 스타일 적용.

```
<p class="highlight">스타일 적용 문단</p>
```



* `style`: 인라인 스타일

```html
<p style="color: red;">빨간색 문장</p>
```

***

### 4. HTML 폼 태그

* 사용자 입력을 받을 때 사용

```html
<form action="/submit" method="post">
    <label for="name">이름:</label>
    <input type="text" id="name" name="name">
    <input type="submit" value="제출">
</form>
```

***

### 5. HTML 문법 규칙

1. 모든 태그는 열고 닫아야함

```html
<p>문장</p>
```

* (단, `<img>`, `<input>` 같은 **빈 태그**는 예외.)



2. 속성 값은 큰따옴표(`"`)로 묶어야 함

```html
<a href="https://example.com">링크</a>
```



3. 중첩된 태그는 닫는 순서를 지켜야 함

```
<div>
    <p>중첩된 태그</p>
</div>
```

