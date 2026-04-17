# enum 활용법

> PHASE 2 | Java 핵심 — 객체지향  
> 키워드: `enum`, `상수`, `타입 안정성`, `static final`, `에러 코드`, `상태값 관리`, `values()`, `valueOf()`

---

## enum이란?

**관련된 상수들을 묶어서 정의하는 타입**.  
단순한 상수 나열이 아니라, **미리 만들어둔 객체를 static final로 고정해서 상수처럼 쓰는 것**이다.

---

## int 상수 방식의 문제점

enum이 없던 시절엔 상수를 int로 정의했다.

```java
public class OrderStatus {
    public static final int PENDING = 0;
    public static final int PAID = 1;
    public static final int SHIPPED = 2;
}
```

문제점:
```java
void processOrder(int status) { ... }

processOrder(1);    // 뭘 의미하는지 알 수가 없음
processOrder(999);  // 잘못된 값인데 컴파일 에러 안 남 → 런타임에 문제 발생
```

> int는 아무 숫자나 들어올 수 있어서 **잘못된 값을 컴파일 시점에 막을 수 없다**.  
> 이것이 **타입 안정성**이 없다는 의미다.

---

## enum으로 개선

```java
public enum OrderStatus {
    PENDING,
    PAID,
    SHIPPED,
    DELIVERED
}
```

```java
void processOrder(OrderStatus status) { ... }

processOrder(OrderStatus.PAID);  // 명확하게 의미 전달
processOrder(999);               // 컴파일 에러 → 잘못된 값 원천 차단
```

> enum을 쓰면 **타입 안정성**이 생긴다.  
> 정해진 값만 받을 수 있어서 잘못된 값을 컴파일 시점에 차단할 수 있다.

---

## enum의 내부 구조

enum 상수 하나하나는 **해당 enum 타입의 객체**다.  
내부적으로 `static final`로 딱 하나씩만 존재한다.

```java
// enum이 내부적으로 하는 일
public static final OrderStatus PENDING = new OrderStatus();
public static final OrderStatus PAID    = new OrderStatus();
```

> **"미리 만들어둔 객체를 static final로 딱 하나씩 고정해서 상수처럼 쓰는 것"** 이 enum이다.

enum 상수는 `static final` 객체이기 때문에 클래스명으로 바로 접근한다:

```java
OrderStatus.PAID   // 클래스명.static변수 → enum 상수 접근
```

---

## enum에 필드와 메서드 추가

enum은 단순 상수 나열 이상으로, **필드와 메서드를 추가**할 수 있다.

```java
public enum OrderStatus {
    PENDING("주문 대기"),
    PAID("결제 완료"),
    SHIPPED("배송 중"),
    DELIVERED("배송 완료");

    private final String description;  // 필드

    OrderStatus(String description) {  // 생성자
        this.description = description;
    }

    public String getDescription() {   // 메서드
        return description;
    }
}
```

```java
OrderStatus status = OrderStatus.PAID;
status.getDescription();  // "결제 완료"
```

---

## enum 기본 메서드

```java
OrderStatus status = OrderStatus.PAID;

status.name();               // "PAID" (enum 상수 이름을 문자열로)
status.ordinal();            // 1 (선언 순서, 0부터 시작)

OrderStatus.valueOf("PAID"); // 해당 문자열 이름의 기존 enum 객체 반환
OrderStatus.values();        // 모든 enum 상수를 배열로 반환
```

---

## 실무에서 enum 활용

### 1. 에러 코드 관리

```java
public enum ErrorCode {
    USER_NOT_FOUND("U001", "사용자를 찾을 수 없습니다"),
    INVALID_PASSWORD("U002", "비밀번호가 올바르지 않습니다"),
    DUPLICATE_EMAIL("U003", "이미 사용 중인 이메일입니다");

    private final String code;
    private final String message;

    ErrorCode(String code, String message) {
        this.code = code;
        this.message = message;
    }

    public String getCode() { return code; }
    public String getMessage() { return message; }
}
```

```java
throw new CustomException(ErrorCode.USER_NOT_FOUND);
```

### 2. 상태값 관리

```java
public enum MemberRole {
    USER, ADMIN, MANAGER
}

public enum PaymentStatus {
    PENDING, PAID, CANCELLED, REFUNDED
}
```

> 에러 코드, 상태값처럼 **"정해진 값들을 한 곳에서 관리"** 할 때 enum이 적합하다.  
> 흩어진 상수들을 enum으로 모으면 유지보수가 훨씬 편해진다.

---

## int 상수 vs enum 비교

| | int 상수 | enum |
|---|---|---|
| 타입 안정성 | 없음 (아무 숫자나 가능) | 있음 (정해진 값만 가능) |
| 가독성 | 낮음 (숫자의 의미 불명확) | 높음 (이름으로 의미 전달) |
| 필드/메서드 | 불가 | 가능 |
| 실무 활용 | 레거시 코드 | 현재 표준 |

---

## 면접 포인트

**Q. enum을 왜 사용하나요?**
> int 상수 방식은 타입 안정성이 없어 잘못된 값이 들어와도 컴파일 시점에 막을 수 없다.  
> enum을 사용하면 정해진 값만 받을 수 있어 컴파일 시점에 잘못된 값을 차단할 수 있다.

**Q. enum 상수는 내부적으로 어떤 구조인가요?**
> enum 상수 하나하나는 해당 enum 타입의 객체다.  
> static final로 딱 하나씩만 존재하기 때문에 상수처럼 사용할 수 있다.

**Q. 실무에서 enum을 어떤 용도로 사용하나요?**
> 에러 코드 관리, 주문 상태/회원 등급 같은 상태값 관리에 주로 사용한다.  
> 정해진 값들을 한 곳에서 관리할 수 있어 유지보수가 편하다.