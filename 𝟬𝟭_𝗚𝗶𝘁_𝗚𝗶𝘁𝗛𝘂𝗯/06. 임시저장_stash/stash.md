## 임시저장 (Stash)

<br>


# 01 Stash란?

→ Stash는 **작업 중인 변경 사항을 커밋하지 않고 임시로 보관해두는 기능**

작업하다 보면 아직 커밋하기 애매한 상태에서 다른 브랜치로 이동해야 할 때가 있음

이때 Stash를 사용하면 작업 중이던 코드를 잠시 치워두고, 나중에 다시 꺼내서 이어서 작업할 수 있음

```text
작업 중인 코드
      ↓ git stash
임시 보관함에 저장 (작업 폴더는 깨끗한 상태)
      ↓ git stash pop
다시 꺼내서 이어서 작업
```

즉, Stash는 **커밋 없이 작업 내용을 잠깐 맡겨두는 서랍**임


<br>
<br>


# 02 Stash를 사용하는 이유

예를 들어 `feature/login` 브랜치에서 로그인 기능을 작업하던 중에 `main` 브랜치의 급한 버그를 수정해야 하는 상황임

이때 작업 중인 변경 사항이 남아 있으면 브랜치 이동이 막히거나, 변경 사항이 다른 브랜치로 따라올 수 있음


> 로그인 기능 작업 중 (커밋하기엔 미완성) → 급하게 main에서 버그 수정 필요 → 브랜치를 이동해야 하는데 변경 사항이 남아 있음

### Stash를 사용하는 이유

- 미완성 코드를 커밋하지 않고 보관할 수 있음
- 브랜치를 이동할 때 작업 폴더를 깨끗하게 만들 수 있음
- 급한 작업을 처리한 후 하던 작업으로 바로 돌아올 수 있음
- `git pull` 전에 변경 사항을 잠시 치워둘 수 있음

<br>


<br>

# 03 변경 사항 임시 저장하기

## ① git stash

```bash
git stash
```

수정한 파일들을 임시 보관함에 저장하고, 작업 폴더를 마지막 커밋 상태로 되돌림

- 이미 Git이 추적 중인 파일의 변경 사항이 저장됨
- `git add`로 스테이징한 내용도 함께 저장됨




## ② 메시지와 함께 저장

```bash
git stash push -m "로그인 작업 중"
```

stash가 여러 개 쌓였을 때 구분하기 쉽도록 메시지를 붙여서 저장함

> 메시지 없이 저장하면 나중에 어떤 작업이었는지 헷갈리기 쉬우므로 메시지를 붙이는 습관이 좋음




## ③ 새로 만든 파일까지 저장

```bash
git stash push -u
git stash push -u -m "새 파일 포함 저장"
```

기본 `git stash`는 **새로 만든 파일(Untracked 파일)을 저장하지 않음**

새 파일까지 함께 보관하려면 `-u` 옵션을 사용함

- `-u` : Untracked 파일(Git이 아직 추적하지 않는 새 파일)도 함께 저장
- `-a` : `.gitignore`로 제외된 파일까지 모두 저장 (거의 사용하지 않음)


<br>
<br>


# 04 Stash 목록 확인하기

## ① git stash list

```bash
git stash list
```

저장해둔 stash 목록을 확인함

```
stash@{0}: On feature/login: 로그인 작업 중
stash@{1}: On main: 버튼 색상 수정
```

- `stash@{0}` : 가장 최근에 저장한 stash
- 숫자가 커질수록 오래된 stash임
- 어떤 브랜치에서 저장했는지도 함께 표시됨




## ② git stash show

```bash
git stash show
git stash show -p
git stash show stash@{1}
```

stash에 어떤 변경 사항이 들어있는지 확인함

- `git stash show` : 변경된 파일 목록 확인
- `-p` : 변경된 코드 내용까지 자세히 확인
- `stash@{n}` : 특정 stash를 지정해서 확인



<br>
<br>

# 05 Stash 꺼내기

## ① git stash pop

```bash
git stash pop
```

가장 최근 stash를 꺼내서 현재 작업 폴더에 적용하고, **목록에서 삭제**함




## ② git stash apply

```bash
git stash apply
```

가장 최근 stash를 현재 작업 폴더에 적용하되, **목록에는 그대로 남겨둠**




## ③ pop과 apply의 차이


> git stash pop   = 적용 + 목록에서 삭제 \
> git stash apply = 적용만 하고 목록에 유지

- `pop` : 한 번 쓰고 끝낼 때 (대부분의 경우)
- `apply` : 같은 변경 사항을 여러 브랜치에 적용하고 싶을 때




## ④ 특정 stash 꺼내기

```bash
git stash pop stash@{1}
git stash apply stash@{1}
```

가장 최근이 아닌 다른 stash를 꺼내고 싶을 때는 번호를 직접 지정함

> `git stash list`로 번호를 먼저 확인한 후 사용하는 것이 안전함



<br>
<br>


# 06 Stash 삭제하기

## ① 특정 stash 삭제

```bash
git stash drop
git stash drop stash@{1}
```

- `git stash drop` : 가장 최근 stash 삭제
- `git stash drop stash@{n}` : 번호를 지정해서 삭제




## ② 전체 stash 삭제

```bash
git stash clear
```

저장된 모든 stash를 한 번에 삭제함

> 삭제한 stash는 복구하기 어려우므로 `git stash list`로 확인한 후 사용해야 함




<br>
<br>

# 07 Stash에서 브랜치 만들기

```bash
git stash branch feature/new-login
```

stash를 저장했던 시점의 커밋에서 새로운 브랜치를 만들고, 그 브랜치에 stash를 적용함

stash를 꺼낼 때 충돌이 날 것 같거나, 저장해둔 작업을 별도 브랜치로 분리하고 싶을 때 사용함

- 새 브랜치 생성 → 해당 브랜치로 이동 → stash 적용 → stash 삭제가 한 번에 진행됨




<br>
<br>

# 08 Stash 전체 흐름

예를 들어 로그인 기능을 작업하다가 `main`의 버그를 급하게 수정해야 하는 상황임

```bash
# 1. 작업 중인 내용을 임시 저장
git stash push -m "로그인 작업 중"

# 2. main 브랜치로 이동해서 버그 수정
git switch main
git switch -c fix/button
# (버그 수정 후 commit, push)

# 3. 원래 작업하던 브랜치로 복귀
git switch feature/login

# 4. 임시 저장한 작업 꺼내기
git stash pop
```

전체 과정은 다음과 같음


> 작업 중 급한 일 발생 → git stash (작업 내용 임시 저장) → 다른 브랜치에서 급한 작업 처리 → 원래 브랜치로 복귀 → git stash pop (작업 내용 복구) → 하던 작업 이어서 진행


<br>
<br>



# 09 Stash 충돌 해결

stash를 꺼낼 때 현재 코드와 stash 내용이 같은 부분을 수정했다면 **Merge Conflict**가 발생할 수 있음

```bash
git stash pop
```

```text
CONFLICT (content): Merge conflict in login.swift
```

충돌이 발생하면 다음과 같이 처리 !!

1. 충돌한 파일을 열어서 직접 코드를 수정함 (Merge Conflict 해결 방법과 동일)
2. `git add 충돌이_해결된_파일`로 해결했다고 알려줌
3. 필요 없어진 stash는 직접 삭제함

```bash
git stash drop
```

> `pop`을 했을 때 충돌이 발생하면 **stash가 자동으로 삭제되지 않고 목록에 남아 있음**. 충돌을 해결한 후 직접 `drop`해야 함


<br>
<br>



# 10 Stash 사용할 때 주의할 점

### ① 새 파일은 기본적으로 저장되지 않음

`git stash`만 사용하면 새로 만든 파일은 그대로 남아 있음

새 파일도 함께 보관하려면 `-u` 옵션을 사용해야 함

```bash
git stash push -u
```




### ② stash는 로컬에만 저장됨

`git push`를 해도 stash는 GitHub에 올라가지 않음

다른 컴퓨터에서 사용할 수 없고, 로컬 저장소를 삭제하면 함께 사라짐




### ③ 장기간 보관하는 용도로 사용하지 않기

<mark>stash는 **잠깐 치워두는 용도**임</mark>

오래 보관해야 하는 작업은 stash보다 임시 브랜치에 커밋해두는 것이 안전함

```bash
git switch -c wip/login
git add .
git commit -m "WIP: 로그인 작업 중"
```




### ④ 어느 브랜치에서든 꺼낼 수 있음

stash는 저장한 브랜치에 묶여 있지 않아서 다른 브랜치에서도 꺼낼 수 있음 !!

의도하지 않은 브랜치에 `pop`하지 않도록 현재 브랜치를 확인한 후 꺼내야 함

```bash
git branch
git stash pop
```




### ⑤ pop 전에 stash 목록 확인하기

여러 개의 stash가 쌓여 있을 때 무심코 `pop`하면 다른 작업이 적용될 수 있음

```bash
git stash list
```

<br>
<br>




# 11 정리

- Stash는 커밋하지 않은 작업 내용을 임시로 보관하는 기능임
- 브랜치를 급하게 이동해야 하거나 `pull` 전에 작업 폴더를 정리할 때 사용함
- `git stash push -m "메시지"`로 저장하면 나중에 구분하기 쉬움
- 새로 만든 파일까지 저장하려면 `-u` 옵션이 필요함
- `git stash list`로 저장된 stash 목록을 확인함
- `git stash show -p`로 stash에 들어있는 변경 내용을 확인함
- `git stash pop`은 꺼내면서 삭제하고, `git stash apply`는 꺼내기만 하고 남겨둠
- 특정 stash는 `stash@{번호}`로 지정함
- `git stash drop`은 하나를 삭제하고, `git stash clear`는 전부 삭제함
- `git stash branch 이름`으로 stash 내용을 새 브랜치로 분리할 수 있음
- pop할 때 충돌이 나면 stash가 남아 있으므로 해결 후 직접 `drop`해야 함
- stash는 로컬에만 저장되고 GitHub에 올라가지 않음
- 오래 보관할 작업은 stash보다 브랜치에 커밋해두는 것이 안전함