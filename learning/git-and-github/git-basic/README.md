---
icon: github
description: How to commit git
---

# Git basic

```python
git init #make Local Repository .git폴더 생성(hidden folder)
```

###

#### **필수 요소**

1. **`<type>`**: 변경 사항의 종류를 나타냄.
   * `feat`: 새로운 기능 추가
   * `fix`: 버그 수정
   * `docs`: 문서 변경
   * `style`: 코드 스타일 변경 (공백, 세미콜론 등 비즈니스 로직 무관)
   * `refactor`: 코드 리팩토링 (기능 변경 없이 구조 개선)
   * `test`: 테스트 추가 또는 수정
   * `chore`: 기타 변경사항 (빌드 프로세스나 패키지 설정 등)
   * `remove` : 파일/디렉토리 삭제
   * `rename` : 파일/디렉토리 이름 수
2. **`<description>`**: 변경 내용을 간략히 요약

#### **선택 요소**

* **`<scope>`**: 변경된 파일이나 기능의 범위를 나타냄
* **본문**: 변경 이유, 상세 설명 등 추가 정보를 작성
* footer: 관련 이슈 번호나 참고 정보를 추가

***

1. **Working directory**

* 내가 실제로 작업하고 있는 디렉토리



2. **Staging Area**

* commit으로 남기고 싶은, 특정 버전으로 관리하고 싶은 파일이 모여있는 곳

```python
git add {file name} # add to Staging Area
        # add하지 않은 file은 untracked  상태
        # add한 file은 tracked 상태
git add {file name1} {file name2} # 여러개의 파일 add
git add . #현재 folder내의 모든 file들을 Staging Area로 add
```

3. **Local Repository**

* Commit들이 저장되는 곳

```python
git commit     
gir commit -m "commit message" # Staging Area to Local Repository(committed)
```



* Commit convention
  * 커밋 메시지를 작성할 때 일정한 규칙을 따르는 것

```bash
type: subject

body

footer
```

{% hint style="info" %}
```
git branch -M main(master)
# master 를 main으로 변경
```
{% endhint %}

4. **Remote Repository**&#x20;

* GitHub과 같은 서버에 있는 저장소

```bash
git push -u origin main(master) 
# Local Repository to Remote Repository 
# u = upstream. connect local branch and remote branch
# 최초 push할때 upstream 설정 이후 git push로 간단하게 사용
git push
```

***

```python
git status # view working directory and staging area status
```

```python
git log #view the commit history of a Git repository
git log --oneline # view simple log
git log -n <number> # 가장 최근의 N개 커밋만 표시
git log <file name> # 특정 파일에 대한 변경 이력만 확인
git log --graph # 시각적으로 보여줌
```

{% hint style="info" %}
commit된 파일을 수정 후 git status로 확인 시 modified 파일로 뜸
{% endhint %}

***

## connect Local Repository with Remote Repository

commit기반으로 연결

* Github에서 create New repository

```bash
git remote add origin {New repository https}
# https주소를 origin에 할당(관례)

git push -u origin main(master) 

git push 
```

## Remote Repository → Local Repository&#x20;

Clone

* Github에서 Repository 선택

```bash
git clone {repository https}

git push -u origin main

git push

git pull

open . # current folder open 

start . # current folder open

code . # 해당 폴더에서 vscode로 open
```

***

### Hiding file

```bash
.gitignore
# .gitignore안에 file and folder 작성
# 반드시 레포지토리에 만들어 놓는것이 좋음

gitignore.io

#한번 commit되면 .gitignore에 넣을 수 없음
```

{% hint style="info" %}
```
git config --global user.name "user name" 
git config --global user.email "user email" 
# adding acount information to Git
```
{% endhint %}



