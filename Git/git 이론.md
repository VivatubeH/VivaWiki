## 명령어의 의미
<img width="875" height="285" alt="image" src="https://github.com/user-attachments/assets/0d13fab4-e2ce-4248-b8ac-c2519edacdda" />

- git add : 작업한 파일 중 '기록하고 싶은 파일'을 staging 영역으로 보내기.
- git commit : staging 영역에 있는 파일 기록하기.

## Merge vs Rebase
- git pull의 기본 방식은 merge, rebase 2가지로 크게 분류할 수 있다.
- merge : 기본적인 pull 방식이며, 서버의 내용과 내 내용을 합쳐서 새로운 기록(Merge Commit)을 하나 더 만든다.
- rebase : 항상 내 작업의 시작점을 원격 저장소의 최신 상태로 통째로 옮겨버린다.

- 메커니즘 : 동기화 ( 서버의 최신 데이터를 내 컴퓨터로 가져옴 ) -> 순서 정렬 ( 내 컴퓨터의 작업 코드를 잠시 떼낸 후, 서버에서 가져온 파일 뒤로 붙임 ) -> 결과 ( 서버의 모든 내용 + 내 작업물 ) 
