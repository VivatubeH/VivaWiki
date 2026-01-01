<img width="616" height="26" alt="image" src="https://github.com/user-attachments/assets/bd9bd4e1-5423-47c5-9e0e-9be061c29433" />

- Git은 비밀번호를 통한 연결이 지원되지 않아서, PAT(Personal Access Token) PAT를 발급받아서 써야함.

---

토큰 발급 방법
1. GitHub 우측 상단 프로필의 Settings
2. 좌측 메뉴 가자 아래 Developer Settings
3. Personal Access Tokens에서 Tokens (classic) 클릭
4. Generate new token
5. 만료 기한은 90일이나 No expiration 권장
- 생성된 토큰 문자열은 반드시 기록해두기 ( 한 번 창 닫으면 볼 수가 없음 )
---

#### 터미널에서 새롭게 인증하기

```bash
git remote remove origin
// 원격 저장소 기존 연결 삭제

git remote add origin https://[복사한토큰]@github.com/VivatubeH/TIL.git
// 토큰 기반 저장소 연결
```
