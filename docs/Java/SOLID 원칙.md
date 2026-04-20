# SOLID 원칙

> PHASE 2 | Java 핵심 — 객체지향  
> 키워드: `SRP`, `OCP`, `LSP`, `ISP`, `DIP`, `단일 책임`, `개방 폐쇄`, `리스코프 치환`, `인터페이스 분리`, `의존성 역전`

---

## SOLID란?

객체지향 설계의 5가지 원칙. **유지보수하기 좋은 코드를 만들기 위한 가이드라인**이다.  
5가지 원칙의 앞글자를 따서 SOLID라고 부른다.

---

## S — 단일 책임 원칙 (Single Responsibility Principle)

**하나의 클래스는 하나의 책임(역할)만 가져야 한다.**

```java
// 나쁜 예 - 하나의 클래스가 너무 많은 책임
public class UserService {
    public void join() { ... }       // 회원가입
    public void sendEmail() { ... }  // 이메일 발송
    public void saveLog() { ... }    // 로그 저장
}

// 좋은 예 - 책임 분리
public class UserService {
    public void join() { ... }
}
public class EmailService {
    public void sendEmail() { ... }
}
public class LogService {
    public void saveLog() { ... }
}
```

> 기준은 **메서드 개수가 아니라 책임(역할)의 개수**다.  
> 메서드가 여러 개여도 전부 "회원 관련 로직"이면 SRP를 지키는 것이다.  
> 이메일 로직이 바뀌었을 때 UserService를 건드려야 한다면 SRP 위반 신호다.

---

## O — 개방-폐쇄 원칙 (Open/Closed Principle)

**확장에는 열려 있고, 수정에는 닫혀 있어야 한다.**

- **확장에 열려있다** → 새 기능을 추가할 수 있다 (새 클래스, 새 구현체 추가)
- **수정에 닫혀있다** → 기존 코드를 건드리지 않아도 된다

```java
// 나쁜 예 - 결제 수단 추가할 때마다 기존 코드 수정
public class PaymentService {
    public void pay(String type) {
        if (type.equals("card")) { ... }
        else if (type.equals("kakao")) { ... }
        // 새 결제 수단 추가 시 여기를 계속 수정해야 함
    }
}

// 좋은 예 - 새 구현체만 추가하면 됨
public interface PaymentStrategy {
    void pay(int amount);
}

public class CardPayment implements PaymentStrategy { ... }
public class KakaoPayment implements PaymentStrategy { ... }
// 새 결제 수단 추가 시 클래스만 하나 더 만들면 됨
```

> 새 결제 수단 추가할 때 기존 `PaymentService` 코드를 수정하지 않고,  
> 새 클래스만 추가하면 되는 것이 OCP다.  
> 인터페이스가 OCP를 지키는 핵심 수단이다.

---

## L — 리스코프 치환 원칙 (Liskov Substitution Principle)

**자식 클래스는 부모 클래스를 완전히 대체할 수 있어야 한다.**

오버라이딩 자체는 괜찮다. 단, **부모가 보장하던 동작의 전제(계약)를 깨는 오버라이딩은 LSP 위반**이다.

```java
// 나쁜 예 - Square가 Rectangle의 전제를 깨버림
Rectangle rect = new Square();
rect.setWidth(5);   // Square라서 height도 5로 바뀜
rect.setHeight(3);  // height만 3이 되는 게 아니라 width도 3으로 바뀜
// 기대: 5 * 3 = 15, 실제: 3 * 3 = 9 ← 전제가 깨짐

// 좋은 예 - 부모의 전제를 지키는 오버라이딩
public class Animal {
    public void sound() { System.out.println("소리낸다"); }
}
public class Dog extends Animal {
    @Override
    public void sound() { System.out.println("멍멍"); }
    // "소리낸다"는 전제는 지키면서 내용만 바꿈 → LSP 준수
}
```

> 부모를 믿고 짠 코드가, 자식으로 교체해도 그 믿음이 깨지면 안 된다.  
> 오버라이딩은 OK, 부모가 보장하던 동작의 전제/계약을 깨는 오버라이딩은 LSP 위반이다.

---

## I — 인터페이스 분리 원칙 (Interface Segregation Principle)

**구현하는 쪽이 필요없는 메서드를 강제로 구현하게 되면 안 된다.**

```java
// 나쁜 예 - 하나의 인터페이스에 너무 많은 메서드
public interface Animal {
    void eat();
    void fly();   // 날지 못하는 동물도 구현 강제
    void swim();  // 수영 못하는 동물도 구현 강제
}

// 좋은 예 - 인터페이스 분리
public interface Eatable { void eat(); }
public interface Flyable { void fly(); }
public interface Swimmable { void swim(); }

public class Dog implements Eatable { ... }
public class Bird implements Eatable, Flyable { ... }
public class Fish implements Eatable, Swimmable { ... }
```

> 기준은 메서드 개수가 아니라 **"구현하는 쪽 입장에서 필요없는 메서드가 강제되는가"** 다.

### ISP 위반 신호

처음 설계할 때 완벽하게 판단하기 어렵다. 아래 신호가 보이면 인터페이스를 쪼개야 한다는 신호다.

```java
public class Dog implements Animal {
    public void eat() { ... }
    public void fly() { throw new UnsupportedOperationException(); }  // 못하니까 예외
    public void swim() { throw new UnsupportedOperationException(); } // 이것도
}
```

> 구현체가 메서드를 빈 구현이나 예외로 채우고 있다면 → 인터페이스 분리가 필요한 신호다.  
> 처음부터 완벽하게 분리하는 것이 아니라, 이런 신호가 보일 때 리팩토링하는 것이 실무 방식이다.

---

## D — 의존성 역전 원칙 (Dependency Inversion Principle)

**고수준 모듈과 저수준 모듈 모두 추상화(인터페이스)에 의존해야 한다.**

| 구분 | 예시 | 설명 |
|---|---|---|
| 고수준 | `OrderService` | "주문을 처리한다"는 비즈니스 로직 |
| 저수준 | `MySQLRepository` | "MySQL에 저장한다"는 세부 구현 |

```java
// 나쁜 예 - 고수준이 저수준에 직접 의존
public class OrderService {
    private MySQLRepository repository = new MySQLRepository();
    // MySQL → MongoDB로 바꾸면 OrderService를 직접 수정해야 함
}

// 좋은 예 - 둘 다 인터페이스에 의존
public class OrderService {
    private OrderRepository repository;  // 인터페이스에 의존

    public OrderService(OrderRepository repository) {
        this.repository = repository;
    }
}
```

### "역전"의 의미

원래 자연스러운 의존 방향:
```
OrderService → MySQLRepository  (고수준이 저수준을 직접 의존)
```

인터페이스를 끼워서 방향을 뒤집으면:
```
OrderService → OrderRepository(인터페이스) ← MySQLRepository
```

> 원래 고수준이 저수준을 바라보던 방향이,  
> 인터페이스 도입으로 저수준이 추상화를 바라보도록 뒤집힌다. 이것이 "역전"의 의미다.  
> Spring DI가 바로 이 원칙을 구현한 것이다.

---

## SOLID 한눈에 보기

| 원칙 | 핵심 한 줄 | 위반 시 문제 |
|---|---|---|
| SRP | 클래스는 하나의 책임(역할)만 | 변경 영향 범위가 너무 넓어짐 |
| OCP | 확장엔 열려있고 수정엔 닫혀있어야 | 기능 추가 시 기존 코드를 계속 수정 |
| LSP | 자식은 부모의 계약을 깨면 안 됨 | 다형성을 믿고 쓴 코드가 오동작 |
| ISP | 필요없는 메서드 구현을 강제하면 안 됨 | 불필요한 메서드 구현 강제 |
| DIP | 고수준/저수준 모두 추상화에 의존 | 구현체 교체 시 코드 전체 수정 |

---

## 면접 포인트

**Q. SOLID 원칙이 뭔가요?**
> 객체지향 설계의 5가지 원칙으로, 유지보수하기 좋은 코드를 만들기 위한 가이드라인입니다.  
> SRP(단일 책임), OCP(개방 폐쇄), LSP(리스코프 치환), ISP(인터페이스 분리), DIP(의존성 역전)로 구성됩니다.

**Q. OCP를 어떻게 지키나요?**
> 인터페이스를 활용해 새 기능은 새 구현체로 추가하고, 기존 코드는 수정하지 않는 방식으로 지킵니다.

**Q. DIP에서 "역전"이 무슨 의미인가요?**
> 원래 고수준 모듈이 저수준 모듈을 직접 의존하던 방향을,  
> 인터페이스 도입으로 저수준이 추상화를 바라보도록 뒤집는다는 의미입니다.

**Q. Spring에서 SOLID가 어떻게 적용되나요?**
> DI(의존성 주입)가 DIP를 구현한 것입니다.  
> Service 계층을 인터페이스로 만들어 OCP와 DIP를 동시에 지킵니다.