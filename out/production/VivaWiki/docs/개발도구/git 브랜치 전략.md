# Git 브랜치 전략

> PHASE 1 | 개발 환경 & 도구  
> 키워드: `Git Flow`, `GitHub Flow`, `main`, `develop`, `feature`, `release`, `hotfix`, `PR`, `CI/CD`

---

## 브랜치 전략이란?

여러 명이 협업할 때 **어떤 브랜치를 만들고, 어떻게 합칠지에 대한 규칙**.  
대표적으로 **Git Flow**와 **GitHub Flow** 두 가지가 있다.

---

## Git Flow

브랜치를 5가지로 나눠서 관리하는 전략.  
각 브랜치의 역할이 명확하게 분리되어 있다.

| 브랜치 | 역할 |
|---|---|
| `main` | 실제 운영 환경에 배포되는 코드 |
| `develop` | 다음 배포를 위한 통합 브랜치. feature들이 여기로 merge됨 |
| `feature/` | 기능 단위로 생성하는 개발 브랜치 |
| `release/` | 배포 전 QA 및 버그 수정 브랜치 |
| `hotfix/` | 운영 중 긴급 버그 수정 브랜치 |

```
feature/* → develop → release/* → main
                                      ↑
                                   hotfix/*
```

> `develop`은 테스트 브랜치가 아니라 다음 배포를 위해 feature들이 모이는 통합 브랜치다.  
> `release`는 develop에서 분기해서 최종 QA 후 main으로 merge하는 브랜치다.

---

## GitHub Flow

브랜치를 **main + feature/** 두 가지만 사용하는 단순한 전략.

```
feature/* → (PR & 코드 리뷰) → main → 즉시 배포
```

**흐름:**
1. main에서 feature 브랜치 생성
2. 기능 개발 후 push
3. PR 생성 → 코드 리뷰
4. merge → 즉시 배포

> feature → main 직접 merge가 아니라 **PR을 통한 코드 리뷰**가 필수다.  
> merge되면 바로 배포되는 구조라 PR의 역할이 더욱 중요하다.

---

## Git Flow vs GitHub Flow 비교

| | Git Flow | GitHub Flow |
|---|---|---|
| 브랜치 수 | 많음 (5종류) | 적음 (2종류) |
| 복잡도 | 높음 | 낮음 |
| 배포 주기 | 주기적 배포 | 수시 배포 |
| CI/CD 친화성 | 낮음 | 높음 |
| 적합한 상황 | 대규모 팀, 버전 관리 중요 | 소규모 팀, 스타트업, 빠른 배포 |

---

## 면접 포인트

**Q. Git Flow의 브랜치 5가지와 각각의 역할은?**
> `main`(운영 배포), `develop`(다음 배포 통합), `feature`(기능 개발),  
> `release`(배포 전 QA), `hotfix`(긴급 버그 수정).

**Q. GitHub Flow가 소규모 팀에 적합한 이유는?**
> 브랜치 구조가 단순하고, CI/CD와 잘 맞아 빠른 수시 배포가 가능하기 때문.  
> 대신 PR과 코드 리뷰의 역할이 더욱 중요해진다.

**Q. 두 전략의 가장 큰 차이는?**
> Git Flow는 브랜치가 많고 배포 주기가 주기적,  
> GitHub Flow는 브랜치가 단순하고 merge 즉시 배포되는 구조.