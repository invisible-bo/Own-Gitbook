---
description: 문자열 관련 함수
---

# String-related functions

1. **`lower()`**
   * 문자열을 모두 소문자로 변환.
   * 예: `"Hello".lower()` → `"hello"`&#x20;
2. **`upper()`**
   * 문자열을 모두 대문자로 변환.
   * 예: `"hello".upper()` → `"HELLO"`
3. **`swapcase()`**
   * 대문자는 소문자로, 소문자는 대문자로 변환.
   * 예: `"Hello World".swapcase()` → `"hELLO wORLD"`
4. **`capitalize()`**
   * 문자열의 첫 글자를 대문자로 변환하고, 나머지는 소문자로 변환.
   * 예: `"hello world".capitalize()` → `"Hello world"`
5. **`title()`**
   * 각 단어의 첫 글자를 대문자로 변환.
   * 예: `"hello world".title()` → `"Hello World"`
6. `replace` : 문자열에서 특정 부분 문자열을 다른 문자열로 대체하는 Python의 문자열 메서드

<pre class="language-python"><code class="lang-python"><strong>string.replace(old, new, count) 
</strong></code></pre>

* **`old`**: 교체하고 싶은 문자열(찾을 문자열).
* **`new`**: `old`를 대체할 문자열.
* **`count`** _(선택적)_: 교체를 수행할 최대 횟수. (생략하면 모든 `old`를 `new`로 교체)
* `replace()`는 **새로운 문자열**을 반환
* 원본 문자열은 **불변(immutable)** 이라, 바뀌지 않음



7. `char.isdigit()` : 문자열이 숫자(10진수)로 구성되어 있는지 확인하는 데 사용\
   &#x20;                                      **`True`** 또는 **`False`** 값을 반환

* 문자열이 **숫자**로만 구성되어 있으면 `True`를 반환.
* 공백, 알파벳, 특수문자 등 숫자가 아닌 문자가 포함되어 있으면 `False`를 반환.
* 문자열의 길이가 1 이상이어도, 문자열 전체가 숫자면 `True` &#x20;

**`char.isalpha()`**: 문자열이 알파벳으로만 구성되어 있는지 확인

**`char.isalnum()`**: 문자열이 알파벳과 숫자로만 구성되어 있는지 확인



8. ' ' . join() : 문자열을 결합하는 데 사용하는함수. \
   &#x20;                 `join()` 메서드는 특정 **구분자**(`separator`)를 기준으로, \
   &#x20;                  **iterable** (리스트, 튜플 등) 안에 있는 문자열 요소들을 하나의 문자열로 합쳐준다

```python
separator.join(iterable)
```

* `separator`: 각 문자열 요소 사이에 들어갈 구분자(빈 문자열도 가능)
* `iterable`: 문자열 요소로 이루어진 리스트, 튜플 등

***

9. **`str.capitalize()`** / **`str.title()`**:
   * `capitalize`: 첫 글자만 대문자로 변환.
   * `title`: 단어별 첫 글자를 대문자로 변환









