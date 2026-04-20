# OOP 4원칙

> PHASE 2 | Java 핵심 — 객체지향  
> 키워드: `캡슐화`, `상속`, `다형성`, `추상화`, `private`, `extends`, `implements`, `오버라이딩`

---

## OOP란?

객체(Object)를 중심으로 프로그램을 설계하는 방식.  
Java는 OOP 언어이며, 4가지 핵심 원칙을 기반으로 한다.

---

## 1. 캡슐화 (Encapsulation)

데이터(필드)와 메서드를 하나의 객체로 묶고, **외부에서 직접 접근하지 못하게 숨기는 것**.

```java
public class User {
    private String password;  // 외부에서 직접 접근 불가

    public void setPassword(String password) {
        // 검증 로직 추가 가능
        this.password = password;
    }
}
```

> 왜 쓰나? 데이터를 외부에서 함부로 변경하지 못하게 보호하고, 변경 시 검증 로직을 넣을 수 있다.

---

## 2. 상속 (Inheritance)

부모 클래스의 필드/메서드를 자식 클래스가 **물려받아 재사용**하는 것.

```java
public class Animal {
    public void eat() { System.out.println("먹는다"); }
}

public class Dog extends Animal {
    public void bark() { System.out.println("짖는다"); }
}
```

> 왜 쓰나? 공통 코드를 부모에 모아 중복을 줄이고 재사용성을 높인다.

---

## 3. 다형성 (Polymorphism)

부모 타입의 참조 변수로 자식 객체를 다룰 수 있는 것. **오버라이딩**이 핵심이다.

```java
Animal animal = new Dog();   // 부모 타입으로 자식 객체 참조
animal.sound();              // 실제로는 Dog의 sound()가 실행됨 (오버라이딩)
```

> 왜 쓰나? 클라이언트 코드는 부모 타입만 알면 되고, 자식 타입이 바뀌거나 추가돼도 기존 코드를 수정하지 않아도 된다.

---

## 4. 추상화 (Abstraction)

복잡한 내부 구현을 숨기고 **필요한 기능만 외부에 노출**하는 것. 인터페이스가 대표적인 예다.

```java
// 인터페이스 (무엇을 하는지만 정의)
public interface PaymentService {
    void pay(int amount);
}

// 구현체
public class KakaoPayService implements PaymentService {
    public void pay(int amount) {
        System.out.println("카카오페이로 " + amount + "원 결제");
    }
}

// 사용하는 쪽
public class OrderService {
    private PaymentService paymentService;  // 구현체가 뭔지 몰라도 됨

    public void order(int amount) {
        paymentService.pay(amount);
    }
}
```

> 왜 쓰나? 사용하는 쪽(클라이언트)은 구체적인 구현을 몰라도 된다.  
> 구현체가 바뀌어도 클라이언트 코드는 수정할 필요가 없다.

---

## 캡슐화 vs 추상화 — 면접 단골 비교

| | 캡슐화 | 추상화 |
|---|---|---|
| **목적** | 데이터 보호 | 구현 숨김 |
| **핵심** | 접근 제어 (`private`) | 인터페이스, 상위 타입 |
| **숨기는 것** | 필드(데이터) | 구현 방법(how) |
| **예시** | `private` 필드 + getter/setter | `PaymentService` 인터페이스 |

> 캡슐화는 **데이터**를 숨기는 것, 추상화는 **구현**을 숨기는 것이다.

---

## 면접 포인트

**Q. OOP 4원칙을 설명해보세요.**
> 캡슐화(데이터 보호), 상속(코드 재사용), 다형성(유연한 타입 처리), 추상화(구현 숨김).

**Q. 다형성에서 오버라이딩이 왜 핵심인가요?**
> 부모 타입으로 참조하더라도 실제 실행은 자식의 오버라이딩된 메서드가 호출되기 때문.  
> 이 덕분에 클라이언트 코드 수정 없이 동작을 바꿀 수 있다.

**Q. 캡슐화와 추상화의 차이는?**
> 캡슐화는 데이터(필드)를 숨기는 것이고, 추상화는 구현 방법을 숨기는 것이다.  
> 캡슐화는 `private` 접근 제어가 핵심이고, 추상화는 인터페이스가 대표적인 수단이다.