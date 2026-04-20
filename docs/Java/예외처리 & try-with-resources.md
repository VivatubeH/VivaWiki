# 예외 처리 & try-with-resources

> PHASE 2 | Java 핵심 — 객체지향  
> 키워드: `예외`, `Exception`, `RuntimeException`, `checked exception`, `unchecked exception`, `try-catch-finally`, `throw`, `throws`, `커스텀 예외`, `try-with-resources`, `AutoCloseable`

---

## 예외(Exception)란?

**프로그램 실행 중에 발생하는 오류**. 처리하지 않으면 프로그램이 죽어버린다.

```java
int[] arr = new int[3];
arr[5] = 10;  // ArrayIndexOutOfBoundsException 발생 → 프로그램 종료
```

---

## 예외 계층 구조

```
Throwable
├── Error          (시스템 수준 오류 - 개발자가 처리하지 않음)
│   └── OutOfMemoryError, StackOverflowError 등
└── Exception      (개발자가 처리해야 하는 예외)
    ├── IOException, SQLException 등       → checked exception
    └── RuntimeException                   → unchecked exception
        └── NullPointerException, IllegalArgumentException 등
```

### checked exception vs unchecked exception

| | checked exception | unchecked exception |
|---|---|---|
| 상속 | `Exception` 직접 상속 | `RuntimeException` 상속 |
| 처리 강제 | 컴파일러가 강제 | 강제 안 함 |
| 대표 예시 | `IOException`, `SQLException` | `NullPointerException`, `IllegalArgumentException` |
| 실무 사용 | 외부 자원 (파일, DB, 네트워크) | 비즈니스 로직 예외, 개발자 실수 |

> checked exception은 컴파일러가 처리를 강제한다.  
> try-catch로 잡거나 throws로 호출자에게 넘기지 않으면 컴파일 에러가 난다.

> **@Transactional 주의사항과 연결:**  
> Spring의 @Transactional은 기본적으로 unchecked exception(RuntimeException)이 발생할 때만 롤백한다.  
> checked exception은 rollbackFor 옵션을 명시해야 롤백된다.

---

## try-catch-finally 구조

```java
try {
    // 예외가 발생할 수 있는 코드
    FileReader reader = new FileReader("file.txt");

} catch (FileNotFoundException e) {
    // 예외 발생 시 처리
    System.out.println("파일을 찾을 수 없습니다: " + e.getMessage());

} finally {
    // 예외 발생 여부와 관계없이 항상 실행
    // 자원 정리 코드 (파일 닫기, DB 연결 종료 등)
    if (reader != null) reader.close();
}
```

> `try` → 예외가 날 수 있는 코드  
> `catch` → 예외 발생 시 처리  
> `finally` → 무조건 실행 (주로 자원 정리용)

### 여러 예외 처리

```java
try {
    // 코드
} catch (FileNotFoundException e) {
    // 파일 없을 때
} catch (IOException e) {
    // 그 외 IO 오류
} catch (Exception e) {
    // 나머지 모든 예외
}
```

---

## throw vs throws

### throw — 예외를 직접 던진다

```java
public void validateAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("나이는 0 이상이어야 합니다");
    }
}
```

### throws — 예외 처리를 호출자에게 넘긴다

```java
public void readFile(String path) throws IOException {
    // IOException을 여기서 처리하지 않고 호출자에게 넘김
    FileReader reader = new FileReader(path);
}
```

> `throw` = 예외를 실제로 발생시킨다  
> `throws` = 이 메서드는 이 예외가 날 수 있으니 호출자가 처리하라는 선언

---

## 커스텀 예외

실무에서는 비즈니스 로직에 맞는 예외를 직접 만들어서 쓴다.

```java
// 커스텀 예외 정의
public class UserNotFoundException extends RuntimeException {

    public UserNotFoundException(String message) {
        super(message);
    }
}

// 사용
public User findUser(Long id) {
    return userRepository.findById(id)
        .orElseThrow(() -> new UserNotFoundException("사용자를 찾을 수 없습니다. id=" + id));
}
```

> 실무에서는 RuntimeException을 상속하는 커스텀 예외를 주로 만든다.  
> 나중에 @ControllerAdvice에서 이 예외를 잡아서 일관된 에러 응답을 만든다. (PHASE 13)

---

## try-with-resources

### 왜 필요한가?

파일, DB 연결 같은 자원은 **사용 후 반드시 닫아야 한다.** 안 닫으면 메모리 누수가 발생한다.

기존 finally 방식은 코드가 복잡하고 close()를 까먹기 쉽다:

```java
// 기존 방식 - 복잡하고 실수하기 쉬움
FileReader reader = null;
try {
    reader = new FileReader("file.txt");
    // 파일 읽기
} catch (Exception e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try {
            reader.close();  // 직접 닫아야 함, 까먹으면 누수
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### try-with-resources로 개선

```java
// try-with-resources - 자동으로 닫아줌
try (FileReader reader = new FileReader("file.txt")) {
    // 파일 읽기
} catch (Exception e) {
    e.printStackTrace();
}
// try 블록이 끝나면 reader.close() 자동 호출 (정상 종료든 예외든)
```

> `try (자원 선언)` 형태로 쓰면,  
> try 블록이 끝날 때 **정상 종료든 예외 발생이든** 자동으로 `close()`가 호출된다.

---

## AutoCloseable이란?

try-with-resources를 쓰려면 자원 클래스가 **`AutoCloseable` 인터페이스를 구현**해야 한다.

```java
public interface AutoCloseable {
    void close() throws Exception;
}
```

`FileReader`, `Connection`, `InputStream` 등 Java 표준 자원 클래스들은 이미 구현되어 있다.

### 커스텀 자원 클래스

```java
public class DatabaseConnection implements AutoCloseable {

    public DatabaseConnection() {
        System.out.println("DB 연결");
    }

    public void query() {
        System.out.println("쿼리 실행");
    }

    @Override
    public void close() {
        System.out.println("DB 연결 종료");  // 자동 호출됨
    }
}

// 사용
try (DatabaseConnection conn = new DatabaseConnection()) {
    conn.query();
}
// 출력:
// DB 연결
// 쿼리 실행
// DB 연결 종료 ← close() 자동 호출
```

### 여러 자원 동시에 사용

```java
try (FileReader reader = new FileReader("input.txt");
     FileWriter writer = new FileWriter("output.txt")) {
    // 읽고 쓰기
}
// 선언 역순으로 close() 자동 호출
// writer.close() → reader.close() 순서
```

---

## 면접 포인트

**Q. checked exception과 unchecked exception의 차이는?**
> checked exception은 Exception을 직접 상속하며 컴파일러가 처리를 강제한다.  
> unchecked exception은 RuntimeException을 상속하며 처리를 강제하지 않는다.  
> 실무에서는 비즈니스 로직 예외는 unchecked exception으로 만드는 게 일반적이다.

**Q. throw와 throws의 차이는?**
> `throw`는 예외를 실제로 발생시키는 것이고,  
> `throws`는 이 메서드에서 예외가 발생할 수 있으니 호출자가 처리하라는 선언이다.

**Q. try-with-resources를 왜 사용하나요?**
> 자원을 사용 후 반드시 닫아야 하는데, finally에서 직접 close()를 호출하면  
> 코드가 복잡하고 실수로 누락될 수 있다.  
> try-with-resources는 AutoCloseable을 구현한 자원을 자동으로 닫아줘서 누수를 방지한다.

**Q. @Transactional은 어떤 예외에서 롤백되나요?**
> 기본적으로 unchecked exception(RuntimeException)에서만 롤백된다.  
> checked exception은 rollbackFor 옵션을 명시해야 롤백된다.