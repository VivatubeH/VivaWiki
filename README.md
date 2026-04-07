# 백엔드 신입 개발자 학습 체크리스트

> 목표: 면접 통과 + 실무 기본기 확립  
> 사용법: 학습 완료 시 `- [ ]` → `- [x]` 로 변경

---

## 1. 네트워크

### 1-1. HTTP/HTTPS
- [ ] HTTP 메서드 (GET, POST, PUT, PATCH, DELETE) 차이와 멱등성
- [ ] HTTP 상태코드 (2xx, 3xx, 4xx, 5xx) 의미와 대표 코드
- [ ] HTTP 헤더 구조 (Content-Type, Authorization, Cache-Control 등)
- [ ] HTTPS 동작 원리 (TLS handshake, 인증서)
- [ ] HTTP/1.1 vs HTTP/2 차이 (multiplexing, 헤더 압축)
- [ ] 쿠키 vs 세션 vs 토큰 비교

### 1-2. TCP/IP
- [ ] TCP vs UDP 차이
- [ ] 3-way handshake (연결 수립)
- [ ] 4-way handshake (연결 종료)
- [ ] IP 주소 & 서브넷 기초
- [ ] 포트 번호 개념

### 1-3. 웹 인프라 기초
- [ ] DNS 동작 원리 (도메인 → IP 변환 흐름)
- [ ] 로드밸런서 개념 (L4 vs L7)
- [ ] 프록시 vs 리버스 프록시
- [ ] CDN 개념
- [ ] 웹소켓 vs HTTP 폴링 차이

---

## 2. 운영체제

### 2-1. 프로세스 & 스레드
- [ ] 프로세스 vs 스레드 차이
- [ ] 멀티프로세스 vs 멀티스레드
- [ ] 컨텍스트 스위칭 개념
- [ ] PCB (Process Control Block) 기초

### 2-2. 동시성
- [ ] Race condition 개념
- [ ] synchronized 키워드 동작 방식
- [ ] volatile 키워드 역할
- [ ] 교착상태 (Deadlock) 4가지 조건
- [ ] Deadlock 해결/회피 방법

### 2-3. 스케줄링 & 메모리
- [ ] CPU 스케줄링 기초 (FCFS, Round Robin, 우선순위)
- [ ] 메모리 구조 (스택 / 힙 / 코드 / 데이터 영역)
- [ ] 가상 메모리 & 페이징 기초
- [ ] 스왑 영역 개념

### 2-4. Linux 실습
- [ ] 기본 명령어 (ls, cd, cp, mv, rm, cat, grep, find)
- [ ] 권한 관리 (chmod, chown, 숫자 표기법)
- [ ] 프로세스 관리 (ps, kill, top, htop)
- [ ] 로그 확인 (tail -f, journalctl)
- [ ] 네트워크 명령어 (netstat, curl, ping)

---

## 3. 컴퓨터 구조

- [ ] CPU 구조 기초 (ALU, CU, 레지스터, 클럭)
- [ ] 캐시 메모리 계층 (L1/L2/L3) & 지역성 원리
- [ ] 메모리 계층 구조 (레지스터 → 캐시 → RAM → 디스크)
- [ ] 빅엔디안 vs 리틀엔디안
- [ ] 비트 & 바이트 연산 기초 (AND, OR, XOR, shift)

---

## 4. 자료구조 & 알고리즘

### 4-1. 자료구조
- [ ] Array vs LinkedList
- [ ] Stack & Queue
- [ ] Tree (이진 트리, BST, 순회)
- [ ] Heap (우선순위 큐)
- [ ] Hash Map 내부 동작 (해시 충돌 해결)
- [ ] Graph (인접 행렬 vs 인접 리스트)

### 4-2. 알고리즘
- [ ] 시간/공간 복잡도 (Big-O)
- [ ] 정렬 (버블, 선택, 삽입, 합병, 퀵)
- [ ] 이진 탐색
- [ ] DFS & BFS
- [ ] 동적 프로그래밍 (DP) 기초
- [ ] 그리디 기초
- [ ] 재귀 & 백트래킹 기초

---

## 5. Java 핵심

### 5-1. 기초 & JVM
- [ ] JDK / JRE / JVM 구조 차이
- [ ] 컴파일 → 바이트코드 → 실행 흐름
- [ ] Java 메모리 모델 (Stack / Heap / Method Area)
- [ ] GC 동작 원리 (Minor GC, Major GC, G1 GC)
- [ ] 기본 자료형 vs 참조형 (박싱/언박싱)

### 5-2. 객체지향
- [ ] OOP 4원칙 (캡슐화, 상속, 다형성, 추상화)
- [ ] 인터페이스 vs 추상클래스 차이와 사용 기준
- [ ] SOLID 원칙 5가지 설명 및 예시
- [ ] 불변 객체 설계 & final 활용
- [ ] static 키워드 올바른 사용

### 5-3. 타입 & 컬렉션
- [ ] String vs StringBuilder vs StringBuffer
- [ ] equals() & hashCode() 재정의 원칙
- [ ] 제네릭 (Generic) 개념 & 와일드카드
- [ ] ArrayList vs LinkedList vs HashMap 내부 동작
- [ ] Comparable vs Comparator
- [ ] enum 활용법 (상수 대체, 메서드 추가)

### 5-4. 함수형 & 스트림
- [ ] 람다 표현식 문법
- [ ] 함수형 인터페이스 (Function, Predicate, Consumer, Supplier)
- [ ] 스트림 API (filter, map, reduce, collect)
- [ ] Optional 올바른 사용법
- [ ] 메서드 참조 (::)

### 5-5. 동시성
- [ ] Thread & Runnable 기본
- [ ] synchronized 블록 vs 메서드
- [ ] volatile 키워드
- [ ] ExecutorService & ThreadPool 사용법
- [ ] CompletableFuture 기초

### 5-6. 기타 실무 필수
- [ ] 어노테이션 개념 & 커스텀 어노테이션
- [ ] 리플렉션 기초 (Spring 내부 동작 이해용)
- [ ] try-with-resources (AutoCloseable)
- [ ] var (Java 10+), record (Java 16+)
- [ ] Lombok 주요 어노테이션 (@Getter, @Builder, @RequiredArgsConstructor)

---

## 6. 프론트엔드 기초

- [ ] HTML 시맨틱 태그 (header, main, section, article 등)
- [ ] CSS 기본 (선택자, box model, flexbox, position)
- [ ] JavaScript 기본 문법 (ES6+: let/const, 화살표 함수, 구조분해)
- [ ] DOM 조작 & 이벤트 처리
- [ ] AJAX & Fetch API (비동기 요청)
- [ ] Promise & async/await 기초
- [ ] Thymeleaf 기본 문법 (th:text, th:if, th:each, th:href)
- [ ] JSP & JSTL 기본
- [ ] jQuery 기본 사용법 ($, 이벤트, $.ajax)
- [ ] Bootstrap 기본 사용법 (그리드 시스템, 컴포넌트)

---

## 7. 개발 도구

- [ ] Git 기본 (add, commit, push, pull, branch, merge)
- [ ] Git 브랜치 전략 (git-flow, GitHub flow)
- [ ] 충돌 해결 (merge conflict)
- [ ] GitHub PR & 코드리뷰 흐름
- [ ] Gradle 빌드 스크립트 기본 (dependencies, task)
- [ ] Maven 기본 (pom.xml 구조)
- [ ] IntelliJ 주요 단축키 & 디버깅

---

## 8. Spring 생태계 — 이론

### 8-1. Spring Core
- [ ] IoC (제어의 역전) 개념
- [ ] DI (의존성 주입) 3가지 방법 (생성자, 세터, 필드) & 생성자 주입 권장 이유
- [ ] Bean 등록 방법 (@Component, @Bean, @Configuration)
- [ ] Bean 생명주기 (초기화, 소멸 콜백)
- [ ] Bean 스코프 (singleton, prototype, request, session)
- [ ] AOP 개념 (횡단 관심사 분리)
- [ ] AOP 프록시 동작 원리 (JDK 동적 프록시 vs CGLIB)
- [ ] @Transactional 동작 원리
- [ ] @Transactional 주의사항 (self-invocation, checked exception)
- [ ] 트랜잭션 전파 수준 (REQUIRED, REQUIRES_NEW 등)

### 8-2. Spring MVC
- [ ] DispatcherServlet 요청 처리 흐름
- [ ] @Controller vs @RestController
- [ ] @RequestMapping, @GetMapping 등 매핑 어노테이션
- [ ] @RequestBody, @ResponseBody, @PathVariable, @RequestParam
- [ ] 필터 vs 인터셉터 vs AOP 차이와 사용 시점
- [ ] HandlerMethodArgumentResolver 기초

### 8-3. Spring Boot
- [ ] Spring Boot 자동 설정 원리 (@EnableAutoConfiguration)
- [ ] application.yml / application.properties 설정 구조
- [ ] 프로파일 분리 (dev / prod)
- [ ] @ConfigurationProperties 사용법
- [ ] Actuator 기초 (health, info 엔드포인트)

---

## 9. Spring 생태계 — 구현

### 9-1. 인증 & 보안
- [ ] Spring Security 필터 체인 구조 이해
- [ ] JWT 발급 & 검증 구현 (Access Token / Refresh Token)
- [ ] Spring Security + JWT 통합 구현
- [ ] OAuth2 소셜 로그인 기초 (Google, Kakao)
- [ ] 비밀번호 암호화 (BCryptPasswordEncoder)
- [ ] CORS 설정 방법

### 9-2. API 개발
- [ ] 회원가입 / 로그인 API 구현
- [ ] 게시판 CRUD API 구현 (JPA + REST)
- [ ] 댓글 기능 구현 (연관관계 매핑 활용)
- [ ] 파일 업로드 구현 (Multipart + S3)
- [ ] 페이징 & 정렬 처리 (Pageable, Sort)
- [ ] 검색 기능 구현 (QueryDSL 동적 쿼리)
- [ ] 전역 예외 처리 (@ControllerAdvice, @ExceptionHandler)
- [ ] 입력값 검증 (@Valid, @Validated, ConstraintValidator)
- [ ] DTO / VO / Entity 분리 설계
- [ ] Swagger / OpenAPI 문서화

### 9-3. 고급 구현
- [ ] 이메일 인증 구현 (JavaMailSender + Redis TTL)
- [ ] Redis 캐싱 구현 (@Cacheable, @CacheEvict)
- [ ] 스케줄러 구현 (@Scheduled)
- [ ] 이벤트 기반 처리 (@EventListener, ApplicationEventPublisher)
- [ ] WebSocket 기초 구현 (실시간 알림)

---

## 10. JPA / ORM

- [ ] 영속성 컨텍스트 개념 & 1차 캐시
- [ ] 엔티티 생명주기 (비영속, 영속, 준영속, 삭제)
- [ ] 변경 감지 (dirty checking)
- [ ] 지연로딩 vs 즉시로딩
- [ ] N+1 문제 원인 & 해결 (fetch join, @EntityGraph, batch size)
- [ ] 연관관계 매핑 (@OneToMany, @ManyToOne, @ManyToMany)
- [ ] 양방향 연관관계 & 연관관계 편의 메서드
- [ ] @Inheritance 상속 전략
- [ ] JPQL 기본 문법
- [ ] 네이티브 쿼리 사용법
- [ ] QueryDSL 기본 설정 & 동적 쿼리 작성
- [ ] 벌크 연산 & @Modifying

---

## 11. 데이터베이스

### 11-1. SQL
- [ ] SELECT, INSERT, UPDATE, DELETE 기본
- [ ] JOIN (INNER, LEFT, RIGHT, FULL)
- [ ] GROUP BY, HAVING, ORDER BY
- [ ] 서브쿼리 (스칼라, 인라인 뷰, WHERE 서브쿼리)
- [ ] 윈도우 함수 기초 (ROW_NUMBER, RANK)
- [ ] 트랜잭션 직접 제어 (BEGIN, COMMIT, ROLLBACK)

### 11-2. 설계 & 최적화
- [ ] 정규화 1NF ~ 3NF
- [ ] ERD 설계 및 작성
- [ ] 인덱스 원리 (B-Tree 구조)
- [ ] 복합 인덱스 & 선택 기준
- [ ] 쿼리 실행 계획 분석 (EXPLAIN)
- [ ] 커버링 인덱스
- [ ] 페이징 최적화 (offset vs cursor 방식)

### 11-3. 트랜잭션 & 동시성
- [ ] ACID 속성
- [ ] 트랜잭션 격리 수준 4단계
- [ ] Dirty Read, Non-Repeatable Read, Phantom Read
- [ ] 낙관적 락 vs 비관적 락
- [ ] DB 커넥션 풀 (HikariCP) 설정

---

## 12. 보안

- [ ] HTTPS / TLS 기초
- [ ] CORS 원리 & 설정
- [ ] SQL Injection 공격 원리 & 방어
- [ ] XSS 공격 원리 & 방어
- [ ] CSRF 공격 원리 & 방어
- [ ] JWT 보안 주의사항 (알고리즘, 만료시간, 저장 위치)
- [ ] 비밀번호 해싱 (BCrypt, Salt)
- [ ] 환경변수로 민감 정보 관리 (.env, yml 분리)

---

## 13. 테스팅

- [ ] 테스트 종류 (단위 / 통합 / E2E) 차이
- [ ] JUnit5 기본 어노테이션 (@Test, @BeforeEach, @DisplayName)
- [ ] Mockito 모킹 (@Mock, @InjectMocks, when/thenReturn)
- [ ] @SpringBootTest 통합 테스트
- [ ] @WebMvcTest (컨트롤러 슬라이스 테스트)
- [ ] @DataJpaTest (JPA 슬라이스 테스트)
- [ ] MockMvc 사용법
- [ ] 테스트 커버리지 개념 & JaCoCo 기초

---

## 14. 로깅

- [ ] SLF4J + Logback 구조
- [ ] 로그 레벨 (TRACE, DEBUG, INFO, WARN, ERROR) 전략
- [ ] logback-spring.xml 설정 (파일 출력, 롤링)
- [ ] MDC (요청 추적 로그, traceId)
- [ ] 운영 환경 로그 전략 (에러만 파일 저장 등)

---

## 15. 인프라 & DevOps

### 15-1. Docker
- [ ] 이미지 & 컨테이너 개념
- [ ] Dockerfile 작성 (Spring Boot 앱 이미지화)
- [ ] docker-compose 작성 (앱 + DB + Redis)
- [ ] 볼륨 & 네트워크 설정
- [ ] 컨테이너 로그 확인 & 디버깅

### 15-2. AWS
- [ ] EC2 인스턴스 생성 & SSH 접속
- [ ] RDS 생성 & Spring Boot 연결
- [ ] S3 버킷 생성 & 파일 업로드 연동
- [ ] IAM 역할 & 보안 그룹 기초
- [ ] Elastic IP 설정
- [ ] 도메인 연결 기초 (Route53 또는 외부 도메인)

### 15-3. CI/CD
- [ ] CI/CD 개념 (지속 통합 / 지속 배포)
- [ ] GitHub Actions 워크플로우 작성
- [ ] 빌드 → 테스트 → Docker 이미지 빌드 → EC2 배포 자동화
- [ ] Nginx 리버스 프록시 설정 (포트 포워딩)
- [ ] 무중단 배포 기초 (Blue-Green 개념)

---

## 16. 아키텍처 & 설계

- [ ] 레이어드 아키텍처 (Controller - Service - Repository)
- [ ] DTO / VO / Entity 분리 원칙
- [ ] REST API URL 설계 규칙
- [ ] 빌더 패턴 (@Builder 활용)
- [ ] 디자인 패턴: 싱글톤
- [ ] 디자인 패턴: 팩토리 메서드
- [ ] 디자인 패턴: 전략 패턴
- [ ] 디자인 패턴: 템플릿 메서드
- [ ] 디자인 패턴: 옵저버 패턴
- [ ] 도메인 모델 설계 기초

---

## 17. 성능 & 최적화

- [ ] Redis 기본 자료구조 (String, List, Hash, Set, ZSet)
- [ ] Redis 캐싱 전략 (Cache-Aside, Write-Through)
- [ ] Redis TTL & 만료 전략
- [ ] DB 쿼리 최적화 (실행계획 분석, 인덱스 활용)
- [ ] 커넥션 풀 튜닝 기초 (HikariCP 설정)
- [ ] 페이징 쿼리 최적화 (offset vs cursor)
- [ ] JVM 튜닝 기초 (힙 사이즈 설정)

---

## 📌 면접 빈출 주제 별도 정리

> 아래 항목은 위 체크리스트와 중복되지만, 면접에서 특히 자주 나오는 것들만 별도 표시

- [ ] Java에서 `==` vs `equals()` 차이
- [ ] HashMap 내부 동작 원리
- [ ] 싱글톤 패턴의 문제점과 Spring에서의 해결
- [ ] Spring Bean 주입 방식과 생성자 주입 권장 이유
- [ ] @Transactional 동작 원리 & 주의사항
- [ ] JPA N+1 문제 원인과 해결 방법
- [ ] 인덱스가 있어도 쿼리가 느린 이유
- [ ] 트랜잭션 격리 수준 4단계
- [ ] JWT vs 세션 방식 비교
- [ ] HTTP vs HTTPS 차이
- [ ] TCP 3-way handshake
- [ ] 프로세스 vs 스레드
- [ ] Deadlock 조건과 해결 방법
- [ ] RESTful API 설계 원칙
- [ ] Docker를 사용하는 이유

---

*마지막 업데이트: 2026-04*
