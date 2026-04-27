# Git 기본

> PHASE 1 | 개발 환경 & 도구  
> 키워드: `git add`, `git commit`, `git push`, `git pull`, `branch`, `merge`, `Working Directory`, `Staging Area`, `Repository`

---

## Git이란?

코드의 변경 이력을 추적하고 여러 사람이 협업할 수 있게 해주는 **분산 버전 관리 시스템**.  
로컬에서도 독립적으로 동작하며, GitHub 같은 원격 저장소와 연동해서 사용한다.

---

## Git의 3가지 영역

Git은 파일이 이동하는 3가지 영역으로 구성된다.

| 영역 | 설명 |
|---|---|
| **Working Directory** | 실제 파일을 수정하는 공간 |
| **Staging Area** | commit할 파일을 모아두는 임시 공간 |
| **Repository** | commit이 저장되는 공간 (로컬 or 원격) |

```
Working Directory  →(add)→  Staging Area  →(commit)→  Repository
```

> `add`는 Working Directory → Staging Area 이동,  
> `commit`은 Staging Area → Repository 이동이다.

---

## 핵심 명령어

### git add

```bash
git add .                   # 변경된 파일 전체를 Staging Area로
git add src/Main.java       # 특정 파일만 추가
```

- 모든 변경사항을 한 번에 commit하지 않고, **원하는 파일만 선택**해서 묶을 수 있다.
- 실무에서는 기능 단위로 파일을 골라 add하는 습관이 중요하다.

### git commit

```bash
git commit -m "feat: 로그인 기능 추가"
```

- Staging Area에 올라온 파일들의 **스냅샷을 찍어 이력으로 저장**한다.
- 저장 버튼이 아니라 **이력을 남기는 행위**에 가깝다.

> 커밋 메시지는 `feat:`, `fix:`, `docs:` 같은 prefix를 붙이는 컨벤션이 실무에서 표준처럼 쓰인다.

### git status / git log

```bash
git status              # 현재 Working Directory / Staging Area 상태 확인
git log --oneline       # commit 이력 한 줄씩 요약 확인
```

- `git status`: add 전후, commit 전후에 **"지금 어떤 파일이 어느 영역에 있는지"** 확인할 때 사용한다.
- `git log --oneline`: push 전에 **내 커밋 이력이 맞는지** 빠르게 확인하는 용도로 자주 쓰인다.

> `add` → `commit` → `git log`로 확인 → `push` 순서가 실무에서 자연스러운 흐름이다.

### git push / pull

```bash
git push origin main    # 로컬 Repository → 원격 저장소(GitHub)
git pull origin main    # 원격 저장소 → 로컬 Repository
```

- `push`: 내 작업을 원격에 올린다.
- `pull`: 원격의 변경사항을 로컬로 가져온다.
- 협업 시 작업 전에 항상 `pull`을 먼저 하는 습관이 중요하다.

---

## branch / merge

### branch란?

독립된 작업 공간이다. **main 브랜치를 건드리지 않고** 기능을 개발할 수 있다.

```bash
git branch feature/login        # 브랜치 생성
git checkout feature/login      # 브랜치 이동
git checkout -b feature/login   # 생성 + 이동 동시에
```

### merge란?

특정 브랜치의 코드를 다른 브랜치로 합친다.

```bash
git checkout main
git merge feature/login         # feature/login을 main에 합치기
```

> 브랜치를 쓰는 이유: 운영 중인 main 코드를 보호하면서, 각자 독립된 공간에서 기능을 개발하기 위해.

---

## 전체 흐름 요약

```bash
git checkout -b feature/login   # 브랜치 생성 & 이동
# ... 코드 작업 ...
git status                      # 변경된 파일 확인
git add .
git commit -m "feat: 로그인 구현"
git log --oneline               # 커밋 이력 확인
git push origin feature/login   # 원격에 push
# GitHub에서 PR 생성 → 코드 리뷰 → merge
```

---

## 면접 포인트

**Q. Git의 3가지 영역을 설명하고, add와 commit이 각각 어떤 이동인지 말해보세요.**
> Working Directory, Staging Area, Repository 3가지 영역이 있습니다.  
> `add`는 Working Directory에서 Staging Area로, `commit`은 Staging Area에서 Repository로 이동시킵니다.

**Q. 브랜치를 왜 사용하나요?**
> main 브랜치를 건드리지 않고 독립된 공간에서 기능을 개발하기 위해 사용합니다.  
> 운영 중인 코드를 보호하면서 안전하게 새 기능을 만들 수 있습니다.

**Q. push와 pull의 차이는?**
> `push`는 로컬 Repository의 코드를 원격 저장소에 올리는 것이고,  
> `pull`은 원격 저장소의 변경사항을 로컬로 가져오는 것입니다.