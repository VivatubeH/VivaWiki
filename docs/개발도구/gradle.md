# Gradle 빌드 스크립트 기본

> PHASE 1 | 개발 환경 & 도구  
> 키워드: `build.gradle`, `plugins`, `dependencies`, `implementation`, `testImplementation`, `runtimeOnly`, `DSL`, `증분 빌드`, `빌드 캐시`

---

## Gradle이란?

Spring Boot 프로젝트를 **빌드하고 의존성을 관리하는 도구**.  
Maven과 함께 Java 생태계에서 가장 많이 쓰이며, 요즘 Spring Boot 프로젝트는 대부분 Gradle을 사용한다.

---

## build.gradle 핵심 구조

```groovy
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.2.0'
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    runtimeOnly 'com.mysql:mysql-connector-j'
}
```

---

## plugins vs dependencies

| | plugins | dependencies |
|---|---|---|
| **역할** | Gradle(빌드 도구) 자체에 기능 추가 | 애플리케이션 코드 실행에 필요한 라이브러리 |
| **비유** | 공장 설비 | 제품 재료 |
| **예시** | Spring Boot 플러그인 → `bootJar` 명령어 활성화 | `spring-boot-starter-web` → `@RestController` 사용 가능 |

Spring Boot **플러그인**은 Gradle이 Spring Boot 앱을 빌드하는 방법을 알게 해준다.  
Spring Boot **스타터**는 내 코드가 동작할 때 실제로 필요한 라이브러리다.

> **비유:** plugins는 공장 설비, dependencies는 제품 재료.  
> 설비(plugins)는 공장이 돌아가기 위한 것이고, 재료(dependencies)는 실제 제품을 만들기 위한 것이다.

---

## dependencies 키워드 3가지

### implementation
- 컴파일 시점 + 런타임 시점 **모두** 필요한 라이브러리
- 내 코드에서 직접 `import`해서 사용하는 것들
- 예: `spring-boot-starter-web`, `spring-boot-starter-data-jpa`

### testImplementation
- **테스트 코드에서만** 사용하는 라이브러리
- 실제 배포 파일(jar)에는 포함되지 않음
- 예: `spring-boot-starter-test` (JUnit5, Mockito 포함)

### runtimeOnly
- 코드 작성 시에는 불필요하지만 **실행 시점에 반드시 필요**한 라이브러리
- 코드에서 직접 `import`하지 않음
- 예: `mysql-connector-j` (MySQL 드라이버)

> **왜 MySQL 드라이버가 runtimeOnly인가?**  
> 내 코드는 JDBC 인터페이스를 통해 DB에 접근한다. MySQL 드라이버를 직접 import하지 않지만,  
> 실행 시 실제 MySQL 연결이 필요하므로 그때 드라이버가 필요하다.

---

## DSL이란?

DSL(Domain Specific Language)은 **특정 목적에 특화된 언어**다.  
Gradle은 빌드 스크립트 작성을 위해 Groovy 또는 Kotlin 기반의 DSL을 사용한다.

| | Groovy DSL | Kotlin DSL |
|---|---|---|
| 파일명 | `build.gradle` | `build.gradle.kts` |
| 타입 | 동적 타입 | 정적 타입 |
| 자동완성 / 오류 감지 | 약함 | 강함 |
| 트렌드 | 기존 프로젝트 | 신규 프로젝트 |

XML(Maven)과 비교하면 같은 의존성을 훨씬 간결하게 표현할 수 있다.

```groovy
// Gradle DSL
implementation 'org.springframework.boot:spring-boot-starter-web'
```

```xml
<!-- Maven XML -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

---

## Gradle vs Maven 비교

| | Gradle | Maven |
|---|---|---|
| 스크립트 형식 | Groovy / Kotlin DSL | XML |
| 가독성 | 높음 | 낮음 (XML 장황함) |
| 빌드 속도 | 빠름 (증분 빌드, 캐시 지원) | 상대적으로 느림 |
| 현재 트렌드 | Spring Boot 프로젝트 표준 | 레거시 프로젝트에 많음 |

### 증분 빌드 (Incremental Build)
전체를 다시 빌드하지 않고 **변경된 부분만** 빌드한다.  
Maven은 기본적으로 매번 전체를 다시 빌드하기 때문에 프로젝트가 커질수록 속도 차이가 커진다.

### 빌드 캐시 (Build Cache)
한 번 빌드한 결과를 저장해뒀다가 **동일한 입력이면 다시 빌드하지 않고 캐시에서 가져온다.**  
팀 단위 개발에서 특히 효과적이다.

> 증분 빌드와 빌드 캐시는 별개의 기능이다.  
> 증분 빌드는 "변경된 것만 빌드", 캐시는 "동일한 입력이면 빌드 자체를 생략".