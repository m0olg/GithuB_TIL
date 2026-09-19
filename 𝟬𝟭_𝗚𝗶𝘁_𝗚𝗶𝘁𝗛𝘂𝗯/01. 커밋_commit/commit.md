## 커밋 `commit`
# 01 커밋이란?
→ **커밋(commit)**은 작업 내용을 Git의 기록으로 저장하는 것

파일을 수정했다고 바로 저장소에 기록되는 건 아님 \
변경된 파일을 먼저 스테이징 영역에 추가한 뒤 커밋해야함

# 02 Git의 기본 작업 흐름
```
작업 디렉터리
    ↓ git add
스테이징 영역
    ↓ git commit
로컬 저장소
    ↓ git push
GitHub 원격 저장소
```

# 03 기본 명령어
```bash
git status
git add .
git commit -m "수정 내용"
git push origin main
```

# 04 명렁어 설명
| 명령어 | 설명 |
| --- | --- |
| `git status` | 파일의 변경 상태 확인 |
| `git add .` | 변경된 모든 파일을 스테이징 영역에 추가 |
| `git add 파일명` | 특정 파일만 추가 |
| `git commit -m "메시지"` | 변경 사항을 커밋 |
| `git push origin main` | main 브랜치에 커밋 업로드 |

# 05 커밋하는 과정
### ① 1단계 - 상태 확인
현재 수정되거나 새로 만들어진 파일을 확인 : `git status`
### ② 2단계 - 파일 추가
모든 변경 파일을 추가 : `git add .`
⭐⭐ **특정 파일만 추가**할 수도 있음 : `git add commit.md`
### ③ 3단계 - 커밋
`-m` 옵션 뒤에 커밋 메시지 작성 : `git commit -m "요기에작성하면됨!!`
### ④ 4단계 - GitHub에 업로드
`git push origin main (git push)`

# 06 규칙
| 접두사 | 의미 | 예시 |
| --- | --- | --- |
| `docs` | 문서 작성 및 수정 | `docs: Git 명령어 정리` |
| `feat` | 새로운 기능 추가 | `feat: 로그인 기능 추가` |
| `fix` | 오류 수정 | `fix: 링크 오류 수정` |
| `refactor` | 코드 구조 개선 | `refactor: 함수 구조 변경` |
| `style` | 코드 스타일 수정 | `style: 들여쓰기 수정` |
| `chore` | 기타 작업 | `chore: 이미지 추가` |

# 07 자주 사용하는 커밋 명령어
* **커밋 기록 확인** : `git log`
    * 간단하게 확인 : `git log --oneline`
* **최근 커밋 내용 확인** : `git show`
* **커밋 전 변경 내용 확인** : `git diff`

# 08 주의할 점
* 커밋 메시지는 변경 내용을 알 수 있게 작성
* 하나의 커밋엔 가능하면 하나의 작업만 담기
* `git add .`를 실행하기 전에 불필요한 파일이 포함되지 않았는지 확인
* 커밋은 로컬 저장소에 저장하는 것이고 깃헙에 올리려면 `git push`가 필요함

# 09 정리
```bash
git status
git add .
git commit -m "수정 내용"
git push origin main
```
> 커밋은 로컬 저장소에 변경 내용을 기록하는 작업
> GitHub에 업로드하려면 반드시 `git push`를 실행해야 함