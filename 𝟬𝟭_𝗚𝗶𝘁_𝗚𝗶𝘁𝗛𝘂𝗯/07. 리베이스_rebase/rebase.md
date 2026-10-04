## 리베이스

<br>


# 01 Rebase란?

→ Rebase는 **내 브랜치가 갈라져 나온 지점(base)을 다른 브랜치의 최신 커밋으로 옮기는 것**

`feature/login` 브랜치에서 작업하는 동안 `main`에 다른 사람의 커밋이 계속 쌓이는 경우가 많음

이때 내 브랜치를 최신 `main` 뒤에서 시작한 것처럼 바꿔주는 게 Rebase임

| 구분 | Rebase 전 | Rebase 후 |
|---|---|---|
| main | A - B - C | A - B - C (그대로) |
| feature 시작 지점 | B에서 갈라져 나옴 | C에서 시작함 |
| feature 커밋 | D, E | D', E' (내용은 같지만 새로 만들어진 커밋) |
| 전체 모양 | 갈라진 형태 | 한 줄로 이어진 형태 |
| 커밋 해시 | D, E의 원래 해시 | 새 해시로 바뀜 |

내가 만든 `D`, `E` 커밋을 잠시 떼어놓았다가 `C` 뒤에 다시 하나씩 적용하는 방식이라, 내용은 같아도 **커밋 자체는 새로 만들어짐** (그래서 `D'`, `E'`로 표시)

<u>결과적으로 커밋 기록이 갈라지지 않고 한 줄</u>로 이어지게 됨 !!!!


<br>
<br>


# 02 Merge와 Rebase의 차이

둘 다 브랜치의 작업을 합친다는 목적은 같지만 기록이 남는 방식이 다름

Merge는 두 브랜치의 기록을 그대로 두고 합쳤다는 표시(Merge Commit)를 하나 추가함. 그래서 작업 과정이 그대로 보존되지만, 브랜치가 많아지면 기록이 복잡해짐

Rebase는 내 커밋들을 최신 기준으로 다시 만들어서 이어 붙임. Merge Commit이 생기지 않아서 기록이 깔끔하지만, **기존 커밋이 새 커밋으로 바뀌기 때문에** 이미 공유한 브랜치에서는 조심해야 함

### Rebase를 사용하는 이유

- 커밋 기록이 한 줄로 깔끔하게 정리됨
- 불필요한 Merge Commit이 생기지 않음
- 작업 브랜치를 최신 `main` 기준으로 맞출 수 있음
- 커밋을 합치거나 수정하는 등 기록을 정리할 수 있음

어느 쪽이 더 좋다기보다는 팀의 규칙에 따라 선택하는 부분임. 작업 과정을 다 남기고 싶으면 Merge, 기록을 깔끔하게 유지하고 싶으면 Rebase를 쓰는 편임


<br>
<br>


# 03 기본 사용법

Rebase는 **옮기려는 내 작업 브랜치에서 실행한다는 점**이 가장 중요함

Merge는 코드가 들어갈 `main`으로 이동해서 실행했지만, Rebase는 반대로 `feature` 브랜치에 있는 상태에서 "나를 최신 `main` 위로 옮겨줘"라고 말하는 방식임

```bash
git switch feature/login
git fetch origin
git rebase origin/main
```

먼저 작업 브랜치로 이동하고, GitHub의 최신 상태를 `fetch`로 받아온 뒤, `origin/main`을 기준으로 Rebase함

Rebase가 끝나면 `feature/login`의 커밋들이 최신 `main` 바로 뒤에 이어져 있음. 이후 `main`에 Merge하면 Merge Commit 없이 그대로 앞으로 이동하는데 이를 **Fast-forward**라고 함


<br>
<br>


# 04 Rebase 중 충돌 해결

Rebase는 커밋을 하나씩 순서대로 다시 적용하는 방식이라 **커밋마다 충돌이 따로 발생**할 수 있음

내 커밋이 3개라면 최대 3번까지 충돌을 해결해야 할 수도 있음. 이 점이 한 번에 합치는 Merge보다 번거롭게 느껴지는 부분임

충돌이 나면 Rebase가 그 자리에서 멈춤. 충돌한 파일을 열어서 수정하는 방법은 Merge Conflict와 완전히 같음. 수정을 마치면 `git add`로 해결했다고 알려주고, 이후에 **`git commit`이 아니라 `git rebase --continue`**로 다음 커밋으로 넘어감

```bash
git add 충돌이_해결된_파일
git rebase --continue
```

중간에 문제가 생기면 두 가지 선택지가 있음

- `git rebase --abort` : Rebase를 완전히 취소하고 시작 전 상태로 돌아감
- `git rebase --skip` : 충돌이 난 커밋을 건너뜀. 그 커밋의 내용은 반영되지 않으므로 신중하게 써야 함

충돌이 너무 꼬였다 싶으면 망설이지 말고 `--abort`로 처음 상태로 돌아가는 게 마음 편함


<br>
<br>





# 05 Interactive Rebase (커밋 정리하기)

Rebase에는 커밋 기록을 직접 정리하는 기능이 있는데, `-i` 옵션을 붙이면 사용할 수 있음

```bash
git rebase -i HEAD~3
```

최근 3개의 커밋을 대상으로 편집기가 열리고, 각 커밋 앞에 `pick`이 붙어 있음. 이 단어를 바꾸고 저장하면 그대로 적용됨

자주 쓰는 명령어는 다음과 같음

- `pick` : 커밋을 그대로 사용
- `reword` : 커밋 메시지만 수정
- `squash` : 바로 앞 커밋과 합침 (메시지도 합쳐서 다시 작성)
- `fixup` : 바로 앞 커밋과 합침 (이 커밋의 메시지는 버림)
- `drop` : 커밋을 삭제

실제로는 `squash`를 가장 많이 씀. 작업하면서 "버튼 수정", "오타 수정", "오류 수정"처럼 잘게 쪼개진 커밋이 쌓였을 때, 첫 번째 커밋만 `pick`으로 두고 나머지를 `squash`로 바꾸면 하나의 커밋으로 합쳐짐

PR을 올리기 전에 이렇게 한 번 정리해두면 리뷰하는 사람도 보기 편함. GitHub의 Squash and Merge와 결과는 비슷하지만, 이쪽은 Push하기 전에 내 컴퓨터에서 미리 정리한다는 차이가 있음

편집 도중에 마음이 바뀌면 이때도 `git rebase --abort`로 취소할 수 있음


<br>
<br>





# 06 Push할 때 주의할 점

Rebase는 기존 커밋을 새 커밋으로 다시 만드는 작업이라 **이미 GitHub에 Push한 브랜치를 Rebase하면 로컬과 원격의 기록이 서로 달라짐**

이 상태에서 평소처럼 `git push`를 하면 `rejected` 오류가 나면서 거부됨. 이럴 때는 강제로 Push해야 하는데, 이때 `--force`보다 `--force-with-lease`를 쓰는 것이 안전함

```bash
git push --force-with-lease origin feature/login
```

`--force`는 상대방이 올린 커밋이 있어도 무조건 덮어써버림. 반면 `--force-with-lease`는 내가 마지막으로 확인한 이후 **다른 사람이 새로 Push한 게 없을 때만** 덮어쓰기 때문에, 실수로 남의 작업을 날려버리는 일을 막아줌

강제 Push는 `main` 같은 공용 브랜치에서는 하지 않고 내가 혼자 쓰는 작업 브랜치에서만 사용해야 함



<br>
<br>




# 07 Rebase 황금 규칙

Rebase에서 가장 중요한 규칙은 **다른 사람과 함께 쓰는 브랜치는 Rebase하지 않는다는 것**임

내가 기록을 바꿔버리면, 같은 브랜치를 받아서 작업하던 팀원의 로컬 기록과 어긋나서 충돌이 연달아 생기고 상황이 매우 복잡해짐

- 나 혼자 쓰는 `feature` 브랜치 → Rebase해도 괜찮음
- 아직 Push하지 않은 로컬 커밋 → Rebase해도 괜찮음
- 여러 명이 함께 작업하는 브랜치 → 하지 않음
- `main`, `develop` 같은 공용 브랜치 → 절대 하지 않음

헷갈릴 때는 *"이 브랜치를 나 말고 누가 받아서 쓰고 있나?"* 를 먼저 생각해보면 됨 \
쓰는 사람이 있다면 Rebase 대신 Merge를 선택하는 게 안전 !!



<br>
<br>




# 08 pull --rebase

`git pull`은 원래 `fetch`와 `merge`를 한 번에 하는 명령어임. 여기에 `--rebase` 옵션을 붙이면 `merge` 대신 `rebase`로 동작함

```bash
git pull --rebase origin main
```

내 로컬에 아직 Push하지 않은 커밋이 있는 상태에서 `pull`을 하면 기본적으로 Merge Commit이 생기는데, `--rebase`를 쓰면 내 커밋이 최신 코드 뒤로 깔끔하게 이어짐. 팀원이 같은 브랜치에 먼저 Push해서 `pull`이 필요할 때 특히 유용함

매번 옵션을 붙이기 번거롭다면 `git config --global pull.rebase true`로 기본값을 바꿔둘 수도 있음


<br>
<br>





# 09 Cherry-pick

## ① Cherry-pick이란?

→ **다른 브랜치에 있는 특정 커밋 하나만 골라서 현재 브랜치로 가져오는 것**

Merge나 Rebase는 브랜치 전체를 대상으로 하지만, Cherry-pick은 이름 그대로 **원하는 커밋만 쏙 골라서** 가져옴

예를 들어 `feature` 브랜치에서 작업하다가 급한 버그를 하나 고쳤고, 그 수정만 먼저 `main`에 반영하고 싶은 상황에서 쓰임. 나머지 작업은 아직 미완성이라 가져오면 안 되는 경우임




## ② 사용 방법

가져온 커밋을 **받을 브랜치로 먼저 이동**한 뒤, 가져올 커밋의 해시를 지정함

```bash
git switch main
git cherry-pick a1b2c3d
```

커밋 해시는 `git log --oneline`으로 확인할 수 있음. 여러 개를 가져오고 싶으면 해시를 공백으로 이어서 적으면 되고, `A..B`처럼 범위로 지정할 수도 있음 (이때 A는 포함되지 않고 A 다음 커밋부터 B까지 가져옴)

옵션도 두 가지 정도 알아두면 좋음

- `-n` : 커밋하지 않고 변경 내용만 가져옴. 여러 커밋을 하나로 묶어서 커밋하고 싶을 때 씀
- `-x` : 커밋 메시지에 어느 커밋에서 가져왔는지 기록을 남김




## ③ 충돌과 주의할 점

Cherry-pick도 충돌이 날 수 있음. 해결 방식은 Rebase와 같아서 파일을 수정하고 `git add`한 뒤 `git cherry-pick --continue`로 이어가거나, `--abort`로 취소함

주의할 점은 **같은 내용의 커밋이 서로 다른 해시로 두 개 존재하게 된다**는 것임. 나중에 두 브랜치를 Merge할 때 같은 변경이 중복으로 잡혀서 충돌이 나는 경우가 있음. 그래서 꼭 필요한 커밋만 가져오고, 습관적으로 쓰지는 않는 것이 좋음





<br>
<br>


# 10 Rebase 취소하기

> Rebase가 아직 진행 중이라면 `git rebase --abort`로 간단하게 취소할 수 있음

이미 Rebase가 끝나버린 뒤에 되돌리고 싶다면 `reflog`를 사용함. Git은 HEAD가 어디를 가리켰는지를 전부 기록해두는데, 이 기록에서 Rebase 직전 시점을 찾아 `git reset --hard`로 돌아가는 방식임. 자세한 방법은 09번 reflog 문서에서 다룸




<br>
<br>



# 11 Rebase 전체 흐름

로그인 기능을 작업하는 사이에 `main`에 새 커밋이 추가된 상황을 예로 들면 다음과 같음

```text
main에서 feature/login 생성
→ feature/login에서 작업하고 Commit
→ 그 사이 main에 다른 사람의 커밋이 추가됨
→ feature/login을 최신 main 위로 Rebase
→ 충돌 해결 (필요한 경우)
→ 이미 Push했다면 --force-with-lease로 Push
→ Pull Request 생성
→ 코드 리뷰
→ Merge
```

Merge만 쓸 때와 비교하면 PR을 올리기 전에 Rebase로 한 번 정리하는 단계가 추가된 셈임


<br>
<br>





# 12 정리

- Rebase는 내 브랜치의 커밋들을 다른 브랜치의 최신 커밋 뒤로 옮겨서 이어 붙이는 작업
- Merge는 기록을 그대로 보존하고 Rebase는 기록을 한 줄로 깔끔하게 정리
- Rebase는 합쳐질 브랜치가 아니라 **옮기려는 작업 브랜치에서 실행**함
- Rebase 중 충돌이 나면 해결 후 `git add`하고 `git rebase --continue`를 사용함
- 진행 중인 Rebase는 `git rebase --abort`로 취소할 수 있음
- `git rebase -i HEAD~n`으로 최근 커밋을 합치거나 수정하거나 삭제할 수 있고, 가장 많이 쓰는 건 `squash`임
- 이미 Push한 브랜치를 Rebase했다면 `--force-with-lease`로 Push해야 함
- 여러 명이 함께 쓰는 브랜치나 `main`에서는 Rebase하지 않음
- `git pull --rebase`는 불필요한 Merge Commit 없이 최신 코드를 가져옴
- Cherry-pick은 다른 브랜치의 특정 커밋만 골라서 가져오는 명령어임
- Cherry-pick한 커밋은 원본과 해시가 달라서 남용하면 중복과 충돌이 생길 수 있음