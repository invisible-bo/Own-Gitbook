# Django Form

* 유저가 입력하는 데이터는 반드시 **유효성 검사**가 필요
* form 작성, view도 작성, 유효성 검사 -> 중복되는 코드발생
* django는 일부 반복되는 작업과 코드를 줄일 수 있는 django form을 제공
  * **직접 구현한 Form + View로직이 필요하다면 사용하지 않아도 됨**

***

### Form 적용

* 새 글 작성에 적용 (new)

```html
...
{{ form.as_p }}
...
```



* Form Widget

ex) (widget=forms.Textarea)













