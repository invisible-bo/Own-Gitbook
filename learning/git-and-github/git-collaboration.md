---
icon: github
---

# Git collaboration

### Shared Repository Model

1. 초기 세팅

* **중앙 저장소**: GitHub, GitLab, Bitbucket 등에서 공동 작업할 **원격 저장소(remote repository)**&#xB97C; \
  만든다
* **초기화**: 각 팀원(A, B, C)이 원격 저장소를 클론(clone)해서 로컬 저장소를 준비한다

```bash
git clone <repository_url>
```

***

2. #### **각자 작업 분담**

* **Branch 사용**: 각 팀원은 자신의 작업을 위해 **새 branch** 를 생성한다

```bash
git checkout -c feature/<작업_내용>
```

* **코드 작성**: 각자 자신이 맡은 기능이나 버그 수정 작업을 진행하고, 변경 내용을 commit한다

```bash
git add .
git commit -m "Add login feature"
```

***

3. #### **작업 병합(Pull Request 또는 Merge Request)**

* 작업이 끝난 팀원은 자신의 브랜치를 원격 저장소로 push한다

```bash
git push origin feature/<작업_내용>
```

* **Pull Request(PR) 생성**: GitHub이나 GitLab에서 PR을 만들어 코드 리뷰를 요청한다

***

4. #### **코드 리뷰와 병합**
   * **리뷰**: 나머지 팀원들이 PR을 검토하고, 의견을 제시하거나 수정을 요청할 수 있다
   * **Merge**: 리뷰가 완료되면, 브랜치를 메인 브랜치(main/master)에 병합한다

```bash
git checkout main
git merge feature/<작업_내용>
git push origin main
```

***

5. **Conflict** (필요 시)

* 만약 A와 B가 같은 파일을 수정했다면 **Merge Conflict**가 발생할 수 있다. 이때, 충돌(conflict)을 해결하고 다시 병합한다

```bash
git merge feature/<작업_내용>
# 충돌 해결 후
git add <수정된_파일>
git commit -m "Resolve merge conflict"
```

***

6. **주기적인 동기화**

* 모든 팀원은 메인 브랜치의 최신 상태를 주기적으로 pull 해서 작업한다

```bash
git pull origin main
```

***









