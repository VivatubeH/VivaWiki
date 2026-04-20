# 인터페이스 vs 추상클래스

> PHASE 2 | Java 핵심 — 객체지향  
> 키워드: `interface`, `abstract class`, `implements`, `extends`, `default 메서드`, `is-a`, `can-do`, `다중 구현`, `단일 상속`, `템플릿 메서드 패턴`

---

## 인터페이스 (Interface)

**구현을 강제하는 계약서**. 무엇을 해야 하는지만 정의하고, 어떻게 할지는 구현체가 결정한다.

```java
public interface Flyable {
    void fly();  // 구현 강제

    default void land() {  // 기본 구현 제공 (선택적 오버라이딩)
        System.out.println("착륙한다");
    }
}

public class Bird implements Flyable {
    public void fly() {
        System.out.println("날개로 난다");
    }
    // land()는 오버라이딩 안 해도 동작함
}
```

### 인터페이스 필드는 상수만 가능

인터페이스는 객체를 만들 수 없어서 인스턴스 필드가 의미가 없다.  
따라서 모든 필드는 자동으로 `public static final` (상수)로 처리된다.

```java
public interface Constants {
    int MAX_SIZE = 100;
    // 위 코드는 아래와 동일
    // public static final int MAX_SIZE = 100;
}
```

### default 메서드란?

Java 8 이전에는 인터페이스에 구현 코드를 넣을 수 없었다.  
인터페이스에 메서드를 추가하면 모든 구현체가 깨지는 문제가 있었기 때문에 `default` 메서드가 도입됐다.

```java
public interface Flyable {
    void fly();

    default void land() {  // 기본 구현 제공
        System.out.println("착륙한다");
    }
}
```

> 구현체가 `default` 메서드를 오버라이딩하지 않으면 기본 동작이 실행된다.  
> 오버라이딩하면 자신의 구현으로 덮어쓸 수 있다.

### 실무에서 인터페이스 사용 예시

Spring에서 Service 계층을 인터페이스로 정의하고 구현체를 주입받는 패턴이 일반적이다.

```java
public interface UserService {
    void join(String username);
}

@Service
public class UserServiceImpl implements UserService {
    public void join(String username) {
        // 실제 구현
    }
}

@RestController
public class UserController {
    private final UserService userService;  // 구현체가 뭔지 몰라도 됨

    public UserController(UserService userService) {
        this.userService = userService;
    }
}
```

> Controller는 `UserService` 인터페이스만 알면 된다.  
> 구현체가 바뀌어도 Controller 코드는 수정할 필요가 없다.  
> 테스트 시 Mock 구현체로 쉽게 교체할 수 있어 테스트가 편해진다.

---

## 추상클래스 (Abstract Class)

**미완성 클래스**. 공통 구현은 부모에 두고, 일부만 자식이 구현하도록 강제한다.

```java
public abstract class Animal {
    private String name;  // 공통 필드

    public Animal(String name) {  // 생성자 (자식이 super()로 호출)
        this.name = name;
    }

    public void eat() {           // 공통 구현
        System.out.println("먹는다");
    }

    public abstract void sound(); // 구현 강제
}

public class Dog extends Animal {
    public Dog(String name) {
        super(name);  // 부모 생성자 호출
    }

    public void sound() {
        System.out.println("멍멍");
    }
}
```

### 추상클래스가 생성자를 가질 수 있는 이유

추상클래스는 직접 `new`로 객체를 만들 수는 없다.  
하지만 자식 클래스가 객체를 생성할 때 `super()`로 부모 생성자를 호출하기 때문에  
공통 초기화 로직을 부모 생성자에 담을 수 있다.

> 추상클래스 자체는 인스턴스화 불가 → 그러나 자식 객체 생성 시 부모 생성자가 실행됨.

### 실무에서 추상클래스 사용 예시

결제 흐름처럼 **전체 흐름은 같고 일부 단계만 다를 때** 템플릿 메서드 패턴으로 활용한다.

```java
public abstract class PaymentTemplate {

    // 전체 흐름 고정 (템플릿)
    public final void pay(int amount) {
        validate(amount);    // 공통 로직
        processPayment(amount);  // 구현체마다 다름
        sendReceipt();       // 공통 로직
    }

    private void validate(int amount) {
        if (amount <= 0) throw new IllegalArgumentException("금액 오류");
    }

    protected abstract void processPayment(int amount);  // 구현 강제

    private void sendReceipt() {
        System.out.println("영수증 발송");
    }
}

public class CardPayment extends PaymentTemplate {
    protected void processPayment(int amount) {
        System.out.println("카드로 " + amount + "원 결제");
    }
}

public class BankTransfer extends PaymentTemplate {
    protected void processPayment(int amount) {
        System.out.println("계좌이체로 " + amount + "원 결제");
    }
}
```

> 전체 결제 흐름(검증 → 결제 → 영수증)은 부모가 고정하고,  
> 실제 결제 방식만 자식이 구현한다. 중복 코드 없이 흐름을 재사용할 수 있다.

---

## 인터페이스 vs 추상클래스 비교

| | 인터페이스 | 추상클래스 |
|---|---|---|
| 목적 | 기능 계약 (무엇을) | 공통 구현 공유 (어떻게) |
| 관계 | can-do (~할 수 있다) | is-a (~이다) |
| 상속 | 다중 구현 가능 | 단일 상속만 가능 |
| 필드 | 상수(`public static final`)만 가능 | 일반 필드 가능 |
| 생성자 | 없음 | 있음 |
| 메서드 | 추상 메서드 + default 메서드 | 추상 + 일반 메서드 모두 가능 |
| 실무 활용 | Service 계층 추상화, DI | 템플릿 메서드 패턴 |

---

## 사용 기준

### 인터페이스 — can-do 관계

서로 다른 계층의 클래스에 **공통 기능을 부여**하거나, **구현체를 교체 가능하게** 설계할 때 사용한다.

```
Bird      → Flyable  (새는 날 수 있다)
Airplane  → Flyable  (비행기도 날 수 있다)
```

> 인터페이스 이름은 `Flyable`, `Serializable`, `Runnable`처럼 **~able** 형태로 짓는 것이 Java 컨벤션이다.

### 추상클래스 — is-a 관계

**같은 종류의 계층 구조**에서 공통 코드를 공유하거나, 전체 흐름을 고정하고 일부만 다르게 구현할 때 사용한다.

```
Dog  is an Animal  (개는 동물이다)
Cat  is an Animal  (고양이는 동물이다)
```

---

## 면접 포인트

**Q. 인터페이스와 추상클래스의 차이는?**
> 인터페이스는 can-do 관계로 서로 다른 클래스에 공통 기능을 부여할 때 사용하고, 다중 구현이 가능하다.  
> 추상클래스는 is-a 관계로 같은 계층의 클래스들이 공통 코드를 공유할 때 사용하며, 단일 상속만 가능하다.

**Q. 언제 인터페이스를, 언제 추상클래스를 쓰나요?**
> 구현체를 교체 가능하게 설계하거나, 서로 다른 종류의 클래스에 공통 기능을 부여할 때 → 인터페이스.  
> 전체 흐름은 같고 일부 단계만 다르게 구현해야 할 때 → 추상클래스 (템플릿 메서드 패턴).

**Q. Java 8의 default 메서드가 왜 생겼나요?**
> 인터페이스에 메서드를 추가하면 모든 구현체가 깨지는 문제를 해결하기 위해 도입됐다.  
> default 메서드로 기본 구현을 제공하면 기존 구현체를 수정하지 않아도 된다.

**Q. Spring에서 인터페이스를 왜 쓰나요?**
> Controller가 Service 인터페이스만 알면 되기 때문에 구현체가 바뀌어도 Controller 코드를 수정할 필요가 없다.  
> 테스트 시 Mock 구현체로 쉽게 교체할 수 있어 단위 테스트가 편해진다.