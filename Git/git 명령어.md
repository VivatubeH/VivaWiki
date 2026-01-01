## 로컬 -> 깃허브

1. 로컬 저장소 만들기 ( git init )
```terminal
git init
```
- 해당 작업 폴더에서 git 사용 시작
- 즉, 해당 시점부터 해당 폴더는 Git으로 관리된다.

2. 작성한 파일 스테이징하기 ( git add )
```terminal
git add 파일명

git add 파일명1 파일명2

git add .
```
- 해당 파일 스테이징하기, 여러 파일 스테이징하기, 모든 파일 스테이징하기.
- 즉, 수정한 파일이더라도 기록하고 싶은 파일만 선택한다.

3. 스테이징한 파일 기록하기 ( git commit )
```terminal
git commit -m "메모"
```
- commit 및 commit 메시지 남기기.
- 즉, 기록하고 싶다고 staging한 파일에 대해 실제 기록을 남긴다.

4. 외부 저장소에 연결하기
```terminal
git remote add origin 레포지토리 URL
```
- 깃허브에서 생성한 Repository의 주소를 입력해서 저장소를 연결한다.

5. 외부 저장소로 코드를 보낸다.
```terminal
git push origin 브랜치명
```
- 내 컴퓨터에 저장된 기록들을 온라인인 Github로 전송한다.

## 깃허브 -> 로컬

#### 프로젝트를 처음 컴퓨터로 내려받을 때

```terminal
git clone 레포지토리 URL
```
- 해당 명령어를 사용할 경우, 폴더 생성 / git init / remote add 등이 한 번에 완료된다.

#### 프로젝트 폴더가 이미 컴퓨터에 있는 경우
```terminal
git pull origin 브랜치명
```
- 깃허브에 올라가 있는 변경 사항만 동기화한다.

```terminal
git status
```
- 어떤 파일을 staging 및 수정했는지 등 상태 확인

#### Java 프로젝트 Git 사용 주의점
- .java는 올리되, .class는 올리지 않는다. ( 다른 환경에서 빌드 시 결과가 달라질 수 있고, 용량 낭비가 됨. )
- 
