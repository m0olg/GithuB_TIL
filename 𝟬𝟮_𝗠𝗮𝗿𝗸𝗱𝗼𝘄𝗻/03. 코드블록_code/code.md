## 코드 블록
<sub><sub> 아 이것도 기본문법에서 써버렷는데 자세히 알고잇음 좋을 것 같아서 일단 적어둠\
<sub>온통다먼작귀인건같은내용쓰기너무힘들어서어쩔수없엇다나중에수정하기‼️‼️

# 01 코드 블록이란?

→ **코드 블록(code block)** 은 여러 줄의 코드나 명령어를 보기 좋게 작성하는 영역

# 02 인라인 코드

한 줄의 코드나 짧은 명령어를 작성할 때 사용함

코드 앞뒤에 백틱 `` ` ``을 붙이면 됨

```markdown
`git status`
```

`git status`

> ### ex.) ⬇️⬇️

```markdown
치이카와 파일을 확인할 때 `git status`를 사용함
```

치이카와 파일을 확인할 때 `git status`를 사용함

# 03 기본 코드 블록

백틱 3개를 코드 앞뒤에 작성하면 여러 줄의 코드를 나타낼 수 있음

````markdown
```
치이카와
하치와레
돼지우사기
```
````

결과:

```
치이카와
하치와레
돼지우사기
```

# 04 언어 지정

코드 블록을 시작할 때 언어를 작성하면 코드에 색상이 적용됨

````markdown
```swift
let name = "치이카와"
print(name)
```
````

결과:

```swift
let name = "치이카와"
print(name)
```

# 05 자주 사용하는 언어

| 언어 | 작성 방법 |
| --- | --- |
| Bash | ` ```bash ` |
| swift | ` ```swift ` |
| HTML | ` ```html ` |

일단 이거 3개정도만 내가 자주쓰는 거고

| 언어 | 작성 방법 |
| --- | --- |
| JavaScript | ` ```javascript ` |
| Python | ` ```python ` |
| CSS | ` ```css ` |
| Java | ` ```java ` |
| SQL | ` ```sql ` |
| JSON | ` ```json ` |

이건 자주 보이는 언어들

# 06 Bash 코드 블록

터미널 명령어를 작성할 때 사용함

````markdown
```bash
cd TIL
git status
git add .
```
````

결과:

```bash
cd TIL
git status
git add .
```

> ### 나머지는 너무 기초라 귀찮으니까 요정도까지만 쓰고 패스 🐔