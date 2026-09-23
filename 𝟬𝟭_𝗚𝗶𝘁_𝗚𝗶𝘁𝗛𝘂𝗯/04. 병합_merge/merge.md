## 머지

<br>


# 01 Merge란?

→ Merge는 **서로 다른 브랜치에서 작업한 내용을 하나의 브랜치로 합치는 것**

Git에서는 보통 기능별로 브랜치를 나누어서 작업함

예를 들어 로그인 기능을 개발할 때 `feature/login`이라는 브랜치를 만들고, 해당 브랜치에서 작업함

작업이 끝나면 `feature/login` 브랜치의 내용을 `main` 브랜치에 합치는데, 이 과정을 **Merge**라고 함

```text
feature/login 브랜치의 작업 내용
                ↓
main 브랜치에 반영
```

즉, Merge는 **작업한 브랜치의 코드를 최종 브랜치에 반영하는 과정**임






# 02 브랜치란?

브랜치는 하나의 프로젝트에서 작업 내용을 나누어 관리하는 공간

기존 코드에 바로 작업하지 않고 새로운 브랜치를 만들면, 기존 프로젝트에 영향을 주지 않고 기능을 개발할 수 있음

예시:

- `main` : 최종적으로 사용하는 브랜치
- `feature/login` : 로그인 기능을 개발하는 브랜치
- `feature/payment` : 결제 기능을 개발하는 브랜치
- `fix/button` : 버튼 오류를 수정하는 브랜치

예를 들어 `main` 브랜치에서 바로 로그인 기능을 개발하면 작업 중인 코드가 바로 프로젝트에 섞이게 됨

그래서 다음과 같이 작업함

```text
main 브랜치에서 feature/login 브랜치 생성
→ feature/login에서 로그인 기능 개발
→ 작업이 끝나면 main에 Merge
```






# 03 Merge를 사용하는 이유

여러 명이 하나의 브랜치에서 동시에 작업하면 코드가 섞이거나 서로의 작업 내용을 덮어쓸 수 있음

그래서 기능별로 브랜치를 나누어 작업한 후, 작업이 끝났을 때 Merge를 사용해 코드를 합침

### Merge를 사용하는 이유

- 기능별로 작업을 나눌 수 있음
- 기존 코드에 영향을 주지 않고 작업할 수 있음
- 여러 명이 동시에 작업할 수 있음
- 작업이 완료된 기능만 선택해서 반영할 수 있음
- 문제가 생겼을 때 작업 내용을 확인하거나 되돌리기 쉬움






# 04 Merge의 기본 흐름

Merge는 보통 다음과 같은 순서로 진행함

```text
브랜치 생성
→ 코드 작업
→ Commit
→ GitHub에 Push
→ Pull Request 생성
→ 코드 리뷰
→ Merge
```

각 과정을 순서대로 살펴보면 다음과 같음




## ① 작업할 브랜치 생성

```bash
git switch -c feature/login
```

`feature/login`이라는 새로운 브랜치를 만들고 해당 브랜치로 이동함

이제부터 작성하는 로그인 기능은 `main`이 아니라 `feature/login` 브랜치에 저장됨




## ② 코드 작업

로그인 화면을 만들거나 로그인과 관련된 코드를 작성함

이때 `main` 브랜치의 코드는 직접 변경되지 않음




## ③ Commit

```bash
git add .
git commit -m "로그인 기능 추가"
```

작업한 내용을 커밋으로 저장함

- `git add .` : 변경한 파일을 커밋할 준비
- `git commit` : 작업 내용을 기록




## ④ GitHub에 Push

```bash
git push origin feature/login
```

로컬 컴퓨터에서 작업한 `feature/login` 브랜치를 GitHub에 업로드함




## ⑤ Pull Request 생성

GitHub에서 `feature/login` 브랜치의 내용을 `main` 브랜치에 합쳐달라고 요청함

이 요청을 **Pull Request**, 줄여서 **PR**이라고 함

```text
feature/login 브랜치
        ↓
main 브랜치에 합쳐달라고 요청
```




## ⑥ 코드 리뷰

다른 사람이 작성한 코드를 확인함

확인하는 내용:

- 코드가 정상적으로 작동하는지
- 기존 기능에 문제가 생기지 않는지
- 프로젝트의 규칙을 지켰는지
- 보안 문제가 없는지
- 불필요한 코드가 없는지

수정할 부분이 있으면 리뷰 내용을 반영하고 다시 Push함




## ⑦ Merge

코드 리뷰가 끝나고 문제가 없으면 PR을 Merge함

그러면 `feature/login` 브랜치에서 작업한 로그인 기능이 `main` 브랜치에 반영됨






# 05 GitHub에서 Merge하는 방법

## ① GitHub 저장소에 접속

작업한 브랜치를 GitHub에 Push한 후 GitHub 저장소에 접속함




## ② Pull Request 생성

`Compare & pull request` 버튼을 누르거나 `Pull requests` 메뉴에서 새로운 PR을 생성함




## ③ 브랜치 확인

다음과 같은 방향으로 설정되어 있는지 확인함

```text
feature/login → main
```

- `main` : 최종적으로 코드가 들어갈 브랜치
- `feature/login` : 작업한 내용이 있는 브랜치

GitHub에서는 보통 다음과 같이 표시됨

```text
base: main
compare: feature/login
```




## ④ PR 작성

PR 제목과 설명을 작성함

```text
제목: 로그인 기능 추가

내용:
- 로그인 화면 구현
- 아이디와 비밀번호 입력 기능 추가
- 로그인 버튼 동작 구현
```




## ⑤ 코드 리뷰 및 검사

코드 리뷰를 받고 자동 테스트가 실행되는지 확인함

수정할 부분이 있다면 코드를 수정하고 다시 Push함




## ⑥ Merge 버튼 클릭

문제가 없다면 `Merge pull request` 버튼을 클릭함

그러면 작업 브랜치의 코드가 `main` 브랜치에 합쳐짐






# 06 터미널에서 직접 Merge하는 방법

GitHub 웹사이트를 사용하지 않고 터미널에서 직접 Merge할 수도 있음

먼저 코드가 들어갈 브랜치로 이동해야 함

```bash
git switch main
```

현재 로컬의 `main` 브랜치를 GitHub의 최신 상태로 업데이트함

```bash
git pull origin main
```

그다음 `feature/login` 브랜치를 `main` 브랜치에 Merge함

```bash
git merge feature/login
```

Merge가 끝나면 변경된 내용을 GitHub에 Push함

```bash
git push origin main
```

전체 과정은 다음과 같음

```bash
git switch main
git pull origin main
git merge feature/login
git push origin main
```

여기서 중요한 점은 **합쳐지는 대상인 `main` 브랜치로 먼저 이동해야 한다는 것**임






# 07 Merge Conflict(머지 충돌)

Merge Conflict는 두 브랜치에서 같은 파일의 같은 부분을 서로 다르게 수정했을 때 발생함

Git 입장에서는 어느 쪽의 코드를 사용해야 할지 판단할 수 없기 때문에 사용자에게 직접 선택하도록 요청함

예를 들어 다음과 같은 상황임

- `main` 브랜치에서 버튼 색상을 파란색으로 수정함
- `feature` 브랜치에서 같은 버튼 색상을 빨간색으로 수정함
- 두 브랜치를 Merge하려고 함

이 경우 Git은 파란색과 빨간색 중 어떤 코드를 남겨야 할지 결정하지 못함

이런 상황을 **Merge Conflict**라고 함






# 08 Merge Conflict 해결 방법

## ① 충돌이 발생한 파일 확인

```bash
git status
```

충돌이 발생한 파일을 확인함




## ② 충돌한 코드 확인

충돌한 파일을 열면 Git이 충돌 부분을 표시해둠

```text
<<<<<<< HEAD
현재 브랜치의 코드
=======
합치려는 브랜치의 코드
>>>>>>> feature/login
```

- `<<<<<<< HEAD` : 현재 사용 중인 브랜치의 코드
- `=======` : 두 코드의 구분선
- `>>>>>>> feature/login` : Merge하려는 브랜치의 코드




## ③ 필요한 코드만 남기기

두 코드 중 필요한 내용을 선택하거나, 두 코드를 적절히 합침

그 후 아래와 같은 충돌 표시를 모두 삭제함

```text
<<<<<<< HEAD
=======
>>>>>>>
```




## ④ 수정한 파일 추가

```bash
git add 충돌이_해결된_파일
```

충돌을 해결했다는 것을 Git에 알려줌




## ⑤ Merge 완료

```bash
git commit -m "Merge conflict 해결"
```

충돌을 해결한 내용을 커밋함




## ⑥ GitHub에 Push

```bash
git push origin main
```

충돌이 해결된 결과를 GitHub에 업로드함






# 09 Merge 방식

GitHub에서는 여러 가지 방식으로 Merge할 수 있음




## (1) Merge Commit

기존 브랜치의 커밋 기록을 그대로 유지하면서 두 브랜치를 합치는 방식

예를 들어 `feature` 브랜치에서 여러 번 커밋한 기록이 있다면, 그 기록을 그대로 `main` 브랜치에 반영함

그리고 두 브랜치가 합쳐졌다는 것을 나타내는 별도의 Merge Commit이 생성됨

### 장점

- 브랜치가 합쳐진 기록을 확인할 수 있음
- 작업 과정이 그대로 남음
- 어떤 시점에 브랜치가 합쳐졌는지 알 수 있음




## (2) Squash and Merge

작업 브랜치에서 만든 여러 개의 커밋을 하나로 합친 후 Merge하는 방식

예를 들어 작업하면서 다음과 같이 여러 번 커밋했다고 가정함

```text
로그인 화면 수정
버튼 위치 수정
오류 수정
텍스트 수정
```

Squash and Merge를 사용하면 위의 커밋들이 하나로 합쳐짐

```text
로그인 기능 추가
```

### 장점

- `main` 브랜치의 커밋 기록이 깔끔해짐
- 작업 중간에 만든 불필요한 커밋을 정리할 수 있음
- 기능 하나를 하나의 커밋으로 관리하기 쉬움




## (3) Rebase and Merge

작업 브랜치의 커밋을 최신 `main` 브랜치 뒤에 이어 붙인 후 Merge하는 방식

기존의 Merge Commit을 만들지 않기 때문에 커밋 기록이 일렬로 정리됨

### 장점

- 커밋 기록이 깔끔하게 이어짐
- 별도의 Merge Commit이 생기지 않음

### 주의할 점

- 커밋 기록이 변경될 수 있음
- 이미 다른 사람이 사용하는 브랜치에서 사용하면 문제가 생길 수 있음
- 협업 중인 브랜치에서는 신중하게 사용해야 함






# 10 Merge와 Pull Request의 차이

### Merge

서로 다른 브랜치의 코드를 실제로 하나로 합치는 작업

### Pull Request

브랜치를 Merge하기 전에 다른 사람에게 코드 검토와 승인을 요청하는 과정

둘은 비슷해 보이지만 같은 의미는 아님

```text
Pull Request 생성
→ 코드 리뷰
→ 승인
→ Merge
```

Pull Request는 Merge를 위한 요청 과정이고, Merge는 실제로 코드를 합치는 작업임






# 11 Merge할 때 주의할 점

### ① Merge 전에 최신 코드 받기

```bash
git switch main
git pull origin main
```

최신 상태의 `main` 브랜치에 작업 내용을 합치는 것이 좋음




### ② 작업 내용을 Commit하기

Commit하지 않은 변경 사항이 있으면 Merge 과정에서 문제가 생길 수 있음

```bash
git status
```

현재 저장되지 않은 변경 사항이 있는지 확인하는 습관이 필요함




### ③ Merge 전에 코드 확인하기

Merge하기 전에 다음 내용을 확인해야 함

- 기능이 정상적으로 작동하는지
- 기존 기능이 망가지지 않았는지
- 테스트가 통과하는지
- 불필요한 파일이 포함되지 않았는지
- 개인정보나 비밀번호가 포함되지 않았는지




### ④ `main`에 바로 Push하지 않기

협업할 때는 보통 `main` 브랜치에 바로 Push하지 않고 Pull Request를 사용하는 것이 안전함

```text
작업 브랜치 생성
→ 코드 작업
→ Commit
→ Push
→ Pull Request
→ 코드 리뷰
→ Merge
```






# 12 Merge 취소하기

Merge를 진행하다가 문제가 생기면 상황에 따라 취소할 수 있음




## 아직 Merge가 완료되지 않은 경우

```bash
git merge --abort
```

진행 중인 Merge를 취소하고 Merge 전 상태로 돌아감




## 이미 Merge가 완료된 경우

```bash
git revert -m 1 <merge-commit-id>
```

이미 완료된 Merge를 되돌리는 새로운 커밋을 생성함

공유된 브랜치에서는 기존 기록을 강제로 삭제하는 것보다 `revert`를 사용하는 것이 안전함






# 13 Merge 전체 흐름

```text
작업 브랜치 생성
→ 기능 개발
→ Commit
→ GitHub에 Push
→ Pull Request 생성
→ 코드 리뷰
→ 충돌 확인 및 해결
→ Merge
→ main 브랜치에 반영
```

예를 들어 로그인 기능을 추가한다고 하면 다음과 같이 진행함

```text
main에서 feature/login 생성
→ feature/login에서 로그인 기능 개발
→ 작업 내용 Commit
→ GitHub에 Push
→ feature/login에서 main으로 Pull Request 생성
→ 코드 리뷰
→ Merge
→ 로그인 기능이 main에 반영
```






# 14 정리

- Merge는 서로 다른 브랜치의 코드를 하나로 합치는 작업임
- 보통 기능별로 브랜치를 만든 후 작업이 끝나면 `main`에 Merge함
- GitHub에서는 Pull Request를 생성한 후 코드 리뷰를 거쳐 Merge함
- `base`는 코드가 들어갈 브랜치이고, `compare`는 작업한 브랜치임
- 터미널에서 Merge할 때는 코드가 들어갈 브랜치로 먼저 이동해야 함
- 같은 파일의 같은 부분을 다르게 수정하면 Merge Conflict가 발생할 수 있음
- Conflict가 발생하면 직접 코드를 수정한 후 다시 Commit해야 함
- Merge 방식에는 Merge Commit, Squash and Merge, Rebase and Merge가 있음
- Pull Request는 Merge 전에 검토를 요청하는 과정임
- 협업할 때는 `main`에 바로 Push하기보다 Pull Request를 사용하는 것이 안전함
- 진행 중인 Merge는 `git merge --abort`로 취소할 수 있음
- 완료된 Merge는 `git revert`를 사용해 되돌릴 수 있음

> ### ⇒ Merge는 브랜치에서 작업한 코드를 다른 브랜치에 합쳐서 최종 프로젝트에 반영하는 과정임 ✨
