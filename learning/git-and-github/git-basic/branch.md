---
description: 브랜치
---

# Branch

### Branch == 특정 commit을 가르키는 포인터

```bash
git branch {branch name}
# branch 생성
git switch -c {branch name}
# branch 생성과 동시에 이동
git swtich {brand name}
# 해당 branch로 이동
git switch main
# main branch로 이동
git branch
# check local branch
git branch -r
#check remote branch
```



## Merge

### Fast-forward merge

* 브랜치를 병합할 때, 병합 대상 브랜치가 기본 브랜치(main or master)의 끝 지점을 가리키도록 단순히 이동하는 병합 방식

```
# 병합 전
main: A -- B -- C
feature:         C -- D -- E
C = 최초 main commit

# 병합 후 (Fast-forward)
main: A -- B -- C -- D -- E
```

```bash
git switch main # 먼저 main branch로 이동
git merge {합치고 싶은 branch name} # branch name을 병합
```



### 3-way merge

* 병합할 때 \*\*공통 조상(base commit)\*\*을 기준으로, 두 브랜치의 변경 사항을 병합하는 방식
* 두 브랜치가 서로 독립적으로 작업했을 때
* 병합 시 충돌(conflict)이 발생할 수 있으며, 이를 해결해야 함

<pre><code><strong># 병합 전
</strong>main: A -- B -- C
feature:      \-- D -- E
# B = 최초 main commit

# 병합 후 (3-way Merge)
main: A -- B -- C ------- F
feature:      \-- D -- E

# F = New Merge Commit
C = branch 1 E = branch 2
</code></pre>

```bash
git switch main # 먼저 main branch로 이동
git merge {합치고 싶은 branch name} # branch name을 병합
```

### Merge commit

* 브랜치를 병합한 결과를 나타내는 **특별한 커밋**
* 3-way Merge 방식에서 병합 작업이 완료된 후 생성
* 병합의 결과물이 명시적으로 나타남
* 병합 시 충돌이 있었다면, 이를 해결한 후 병합 커밋이 생성

```
# 병합 전
main: A -- B -- C
feature:      \-- D -- E
# B = 최초 main commit

# 병합 후 (3-way Merge)
main: A -- B -- C ------- F
feature:      \-- D -- E

# F = New Merge Commit 
C = branch 1 E = branch 2
```

```bash
git switch main # 먼저 main branch로 이동
git merge {합치고 싶은 branch name} # branch name을 병합
```

#### 병합 중 conflict 발생 시

1. CONFLICT (content): Merge conflict in <파일명>

```
CONFLICT (content): Merge conflict in {file name}
```

2. 충돌된 파일을 열고, 충돌을 수동으로 해결
3. 충돌이 해결된 파일을 Git에 추가

```bash
git add {file name}
```

4. 병합을 완료하기 위해 커밋을 생성

```bash
git commit
```



#### 병합 이후 상태 확인

```bash
git log
git log --graph --oneline
```

결과 ex)

```
*   f1e2d3f (HEAD -> main) Merge branch 'feature' into main
|\
| * a1b2c3d (feature) Commit E
| * b2c3d4e Commit D
* c3d4e5f Commit C
* b2d3c4a Commit B
* a1b2c3e Commit A
```

```bash
git status로 상태확인
```



***

### Vi 편집기

UNIX 및 Linux의 Text편집기

* Command mode
* Insert mode
* Ex mode (:로 시작)

```bash
vi {file name}  # 실행
i # insert mode
:w # save
:q # quit
:wq or :x #save and quit
:q! # force quit
```
