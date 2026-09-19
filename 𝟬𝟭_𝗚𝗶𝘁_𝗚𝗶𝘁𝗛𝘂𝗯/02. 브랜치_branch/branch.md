## 브랜치 🥖

# 01 브랜치란?

→ **브랜치(branch)** 는 하나의 저장소에서 독립적으로 작업할 수 있도록 만든 작업 공간

원본 코드를 바로 수정하지 않고 브랜치를 만들어서 기능을 추가하거나 수정할 수 있음

> **ex.)** \
>`main` 브랜치는 완성된 코드를 보관하고 새로운 기능은 별도의 브랜치에서 작업함

# 02 브랜치를 사용하는 이유

- **원본 코드에 영향을 주지 않고 작업**할 수 있음
- 여러 사람이 **동시에 작업**할 수 있음
- 기능별로 작업 내용을 나눌 수 있음
- 문제가 생겨도 기존 코드로 쉽게 돌아갈 수 있음
- 작업이 끝난 뒤 `main` 브랜치에 합칠 수 있음

# 03 현재 브랜치 확인

→ 현재 사용 중인 브랜치를 확인하려면 `git branch` 명령어를 사용함

```bash
git branch
```

현재 사용 중인 브랜치 앞에는 `*` 표시가 붙음

```text
* main
```

# 04 브랜치 만들기

#### 새로운 브랜치를 만들 때는 다음 명령어를 사용함 ⬇️⬇️

```bash
git branch feature
```

예를 들어 새로운 기능을 개발하기 위한 브랜치를 만들 수 있음

```bash
git branch feature/character
```

= <mark>브랜치를 만든 것과 해당 브랜치로 이동하는 것은 별개의 작업</mark>임

# 05 브랜치 이동

→ 브랜치로 이동할 때는 `git switch` 명령어를 사용함

```bash
git switch feature
```

> #### ex.) ⬇️⬇️

```bash
git switch feature/character
```

# 06 브랜치 만들면서 이동하기

브랜치를 만들면서 바로 이동하려면 다음 명령어를 사용함

```bash
git switch -c feature
```

> #### ex.) ⬇️⬇️

```bash
git switch -c feature/character
```

→ `-c`는 브랜치를 생성하면서 해당 브랜치로 이동한다는 의미

# 07 브랜치에서 작업하기

브랜치로 이동한 뒤 파일을 수정하고 커밋하면 됨

```bash
git switch -c feature/character

git add .
git commit -m "feat: 캐릭터 정보 추가"
```

이 커밋은 현재 브랜치에만 저장됨

`main` 브랜치에는 바로 반영되지 않음 ‼️

# 08 브랜치 업로드하기

로컬에서 만든 브랜치를 GitHub에 업로드하려면 `git push`를 사용함

```bash
git push origin feature/character
```

처음 업로드할 때는 `-u` 옵션을 사용할 수 있음

```bash
git push -u origin feature/character
```

→ 이후에는 `git push`만 입력해도 됨

# 09 브랜치 합치기

작업이 끝난 브랜치를 `main` 브랜치에 합치는 것을 **병합(merge)**이라고 함

먼저 `main` 브랜치로 이동함

```bash
git switch main
```

그다음 작업 브랜치를 병합함

```bash
git merge feature/character
```

# 10 브랜치 삭제하기

작업이 끝난 브랜치를 삭제할 수 있음

```bash
git branch -d feature/character
```

강제로 삭제하려면 `-D` 옵션을 사용함

```bash
git branch -D feature/character
```

→ 아직 병합하지 않은 작업이 사라질 수 있으므로 주의해야 함

# 11 브랜치 전체 흐름

```bash
git pull origin main

git switch -c feature/character
[⤷ 맥은 git --version ⭐⭐]

git add .
git commit -m "feat: 캐릭터 정보 추가"

git push -u origin feature/character

git switch main
git merge feature/character

git push origin main
```

# 12 브랜치 관련 명령어 정리

| 명령어 | 설명 |
| --- | --- |
| `git branch` | 브랜치 목록 확인 |
| `git branch 이름` | 브랜치 생성 |
| `git switch 이름` | 브랜치 이동 |
| `git switch -c 이름` | 브랜치 생성 후 이동 |
| `git merge 이름` | 브랜치 병합 |
| `git branch -d 이름` | 브랜치 삭제 |
| `git push origin 이름` | 브랜치 업로드 |
| `git pull origin main` | 원격 저장소 내용 가져오기 |

> ### ✨ **브랜치는 원본 코드와 분리해서 작업할 수 있는 공간 작업이 끝나면 `merge`를 사용해서 브랜치를 합침** !!!!!!!