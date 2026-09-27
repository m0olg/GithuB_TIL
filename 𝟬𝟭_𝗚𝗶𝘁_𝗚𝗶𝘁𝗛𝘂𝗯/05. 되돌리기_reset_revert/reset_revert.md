## 되돌리기




# 01 되돌리기란?

→ Git에서 되돌리기는 **이전에 한 작업이나 변경 사항을 취소하는 것**

작업하다 보면 잘못 수정하거나, 원하지 않는 내용을 Commit할 수 있음  
이럴 때 Git의 되돌리기 기능을 사용하면 이전 상태로 돌아가거나 변경 내용을 취소할 수 있음

Git에는 상황에 따라 사용하는 방법이 여러 가지 있음

- `git restore`: 파일의 수정 사항을 취소
- `git reset`: Commit을 되돌리고 브랜치 기록을 이동
- `git revert`: 기존 기록은 유지하면서 취소하는 Commit을 생성






# 02 Git에서 관리하는 변경 단계

Git에서 파일의 변경 사항은 보통 다음 단계를 거침

> 파일 수정 → Staging Area에 추가 → Commit

- **수정된 파일**: 파일을 변경했지만 아직 `git add`하지 않은 상태
- **Staging Area**: Commit에 포함할 파일을 올려둔 상태
- **Commit**: 변경 내용을 Git 기록으로 저장한 상태

어느 단계의 내용을 되돌릴지에 따라 사용하는 명령어가 달라짐






# 03 `git restore`로 파일 수정 취소하기

아직 Commit하지 않은 파일의 수정을 취소할 때 사용함

```bash
git restore 파일명
```

예를 들어 `LoginView.swift`의 수정 사항을 취소하려면 다음과 같이 입력함

```bash
git restore LoginView.swift
```

이 명령은 파일을 마지막 Commit 상태로 되돌림  
아직 저장하지 않은 수정 내용은 사라질 수 있으므로 실행 전에 확인해야 함

### Staging Area에 올린 파일 수정 취소하기

이미 `git add`한 파일을 Staging Area에서 내리려면 다음과 같이 사용할 수 있음

```bash
git restore --staged 파일명
```

파일을 Staging Area에서 내리지만, 파일에 작성한 수정 내용 자체는 남아 있음






# 04 `git reset`이란?

→ `git reset`은 **브랜치가 가리키는 Commit을 이전 위치로 옮기는 명령어**

Commit을 되돌릴 때 사용할 수 있지만, 옵션에 따라 파일의 수정 내용까지 삭제될 수 있음

```bash
git reset [옵션] 되돌아갈_위치
```

예를 들어 가장 최근 Commit을 취소하려면 다음과 같이 입력

```bash
git reset HEAD~1
```

`HEAD~1`은 현재 위치에서 바로 이전 Commit을 뜻함

`git reset`은 Commit 기록을 실제로 이동시키므로 이미 깃헙에 Push한 Commit에 사용할 때는 주의해야 함






# 05 `git reset`의 옵션

## ① `--soft`

Commit만 취소하고 변경 내용은 Staging Area에 남김

```bash
git reset --soft HEAD~1
```

```text
Commit 취소
→ 변경 내용은 Staging Area에 남음
```

Commit 메시지를 다시 작성하거나, 여러 Commit을 합치고 싶을 때 사용할 수 있음

## ② `--mixed`

Commit을 취소하고, 변경 내용은 Staging Area에서 내림  
파일에 작성한 수정 내용은 남아 있음

```bash
git reset --mixed HEAD~1
```

`--mixed`는 `git reset`의 기본 옵션이라 생략할 수도 있음

```bash
git reset HEAD~1
```

```text
Commit 취소
→ Staging Area에서 내려옴
→ 파일 수정 내용은 남음
```

## ③ `--hard`

Commit과 파일 수정 내용까지 모두 되돌림

```bash
git reset --hard HEAD~1
```

```text
Commit 취소
→ Staging Area 변경 취소
→ 파일 수정 내용도 삭제
```

`--hard`는 작업 내용을 잃을 수 있으므로 실행 전에 반드시 확인해야 함






# 06 `git revert`란?

→ 기존 Commit은 그대로 두고, 그 변경 사항을 취소하는 새로운 Commit을 만드는 것

```bash
git revert 커밋ID
```

예를 들어 특정 Commit의 변경 내용을 취소하려면 다음과 같이 입력함

```bash
git revert a1b2c3d
```

`git revert`는 기존 기록을 삭제하거나 옮기지 않음  
대신 기존 변경을 반대로 적용한 새 Commit을 추가함

```text
기능 추가 Commit
→ 기능 추가를 취소하는 새 Commit
```

이미 GitHub에 Push했거나 여러 사람이 함께 사용하는 브랜치에서는 보통 `git revert`가 더 안전함 !!






# 07 `reset`과 `revert`의 차이

### `git reset`

- 브랜치가 가리키는 위치를 이전 Commit으로 이동함
- Commit 기록이 없어질 수 있음
- 아직 공유하지 않은 Commit을 정리할 때 주로 사용함
- 옵션에 따라 파일 수정 내용도 삭제할 수 있음

### `git revert`

- 기존 Commit을 그대로 보존함
- 변경 사항을 취소하는 새 Commit을 만듦
- 이미 Push한 Commit을 되돌릴 때 사용하기 좋음
- 여러 사람이 함께 쓰는 브랜치에서 비교적 안전함

간단히 구분하면 다음과 같음


> **reset**  → 이전 기록으로 돌아감 \
> **revert** → 취소하는 기록을 새로 추가함






# 08 상황에 맞는 되돌리기 명령어

| 상황 | 사용할 명령어 |
|---|---|
| Commit 전 파일 수정 취소 | `git restore 파일명` |
| Staging Area에서 파일 내리기 | `git restore --staged 파일명` |
| Commit은 취소하고 수정 내용은 남기기 | `git reset --soft HEAD~1` |
| Commit은 취소하고 수정 파일은 남기기 | `git reset --mixed HEAD~1` |
| Commit과 수정 내용을 모두 버리기 | `git reset --hard HEAD~1` |
| Push한 Commit의 변경을 안전하게 취소하기 | `git revert 커밋ID` |






# 09 되돌리기 전에 확인할 점

> 현재 파일 상태와 Commit 기록을 먼저 확인하는 습관이 필요함

```bash
git status
git log --oneline
```

- `git status`: 파일이 수정되었는지, Staging Area에 올라갔는지 확인
- `git log --oneline`: Commit 기록을 간단하게 확인

특히 `git reset --hard`는 수정 내용까지 삭제할 수 있으므로 실행 전에 작업 내용을 확인해야 함

이미 다른 사람과 공유한 Commit은 기록을 바꾸는 `reset`보다 `revert`를 사용하는 편이 안전함






# 10 정리

* `git restore`는 Commit 전 파일의 수정 내용을 취소할 때 사용
* `git reset`은 브랜치가 가리키는 Commit을 이전 위치로 옮길 때 사용
* `--soft`는 변경 내용을 Staging Area에 남김
* `--mixed`는 Staging Area에서 내리지만 파일 수정 내용은 남김
* `--hard`는 파일 수정 내용까지 삭제하므로 주의해야 함
* `git revert`는 기존 기록을 보존하고 취소 Commit을 새로 만듦
* 이미 Push했거나 공유한 Commit은 보통 `git revert`가 더 안전함
* 실행 전 `git status`와 `git log --oneline`으로 현재 상태를 확인하는 게 좋음

> ### ⇒ 되돌리기 전에 어떤 단계의 내용을 취소할지 확인하고, 공유된 기록은 신중하게 다루기 ✨