# equals() & hashCode() 재정의 원칙

> PHASE 2 | Java 핵심 — 객체지향  
> 키워드: `equals()`, `hashCode()`, `Object`, `주소값 비교`, `동등성`, `HashSet`, `HashMap`, `Objects.hash()`

---

## equals()란?

**두 객체가 같은지 비교하는 메서드**. 기본적으로 `Object` 클래스에 정의되어 있다.

```java
// Object의 기본 equals() - 주소값(참조) 비교
public boolean equals(Object obj) {
    return (this == obj);
}
```

기본 `equals()`는 **주소값 비교**다. 내용이 같아도 다른 객체면 `false`가 나온다.

```java
String a = new String("hello");
String b = new String("hello");

System.out.println(a == b);       // false (주소값 다름)
System.out.println(a.equals(b));  // true  (String은 equals 재정의함)
```

> 재정의가 필요한 이유: 내용이 같아도 다른 객체면 false가 나오기 때문에,  
> 객체의 의미(내용)로 비교하려면 반드시 재정의해야 한다.

---

## hashCode()란?

**객체를 숫자(해시값)로 변환하는 메서드**. `HashMap`, `HashSet` 같은 자료구조에서 객체를 빠르게 찾기 위해 사용한다.

```java
// 기본 hashCode() - 주소값 기반으로 생성
Object obj = new Object();
System.out.println(obj.hashCode());  // 주소 기반 숫자
```

---

## 왜 같이 재정의해야 하나?

Java의 규칙:

> **equals()가 true면 hashCode()도 반드시 같아야 한다.**

`equals()`만 재정의하고 `hashCode()`를 재정의하지 않으면:

```java
public class User {
    private String email;

    @Override
    public boolean equals(Object o) {
        User user = (User) o;
        return email.equals(user.email);
    }
    // hashCode는 재정의 안 함 → 주소값 기반 해시값 사용
}

User u1 = new User("test@test.com");
User u2 = new User("test@test.com");

System.out.println(u1.equals(u2));  // true (같다고 판단)

Set<User> set = new HashSet<>();
set.add(u1);
set.add(u2);
System.out.println(set.size());  // 2 ← 같은 유저인데 둘 다 들어감!
```

`HashSet`은 내부적으로 `hashCode()`로 먼저 버킷을 찾고, 그 다음 `equals()`로 비교한다.  
`hashCode()`가 다르면 아예 다른 버킷에 들어가서 중복 체크를 못 한다.

> equals()만 재정의하면 HashSet, HashMap 같은 자료구조에서  
> 의미상 같은 객체임에도 별도로 저장되는 문제가 발생한다.

---

## 올바른 재정의

### 단일 필드 기준

```java
public class User {
    private String email;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof User)) return false;
        User user = (User) o;
        return email.equals(user.email);
    }

    @Override
    public int hashCode() {
        return Objects.hash(email);  // equals에서 쓴 필드와 동일하게
    }
}
```

### 여러 필드 기준

```java
public class User {
    private String email;
    private String name;
    private int age;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof User)) return false;
        User user = (User) o;
        return age == user.age &&
               email.equals(user.email) &&
               name.equals(user.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(email, name, age);  // equals에서 쓴 필드 전부
    }
}
```

> `Objects.hash()`가 여러 필드를 조합해서 해시값을 만들어준다.  
> equals()에서 비교한 필드를 전부 똑같이 넣으면 된다.

---

## 재정의 시 주의사항

1. **equals()와 hashCode()는 항상 같이 재정의**해야 한다.
2. **같은 필드 기준으로 재정의**해야 한다.

```java
// 잘못된 예 - 다른 필드 기준으로 재정의
public boolean equals(Object o) {
    return email.equals(((User)o).email);  // email 기준
}

public int hashCode() {
    return Objects.hash(name);  // name 기준 ← 다른 필드!
}
// equals()는 true인데 hashCode()는 다른 경우가 생겨
// HashSet/HashMap에서 중복 체크 실패
```

---

## 실무에서는?

Lombok을 쓰면 자동으로 해결된다.

```java
@EqualsAndHashCode
public class User {
    private String email;
    private String name;
}
```

또는 IntelliJ에서 `Alt + Insert` → `equals() and hashCode()` 자동 생성도 가능하다.

> 실무에서 직접 구현하는 경우는 드물지만,  
> **왜 같이 재정의해야 하는지 이유**는 면접에서 반드시 나온다.

---

## 면접 포인트

**Q. equals()를 재정의할 때 hashCode()도 같이 재정의해야 하는 이유는?**
> equals()만 재정의하면 HashSet, HashMap 같은 자료구조에서  
> 의미상 같은 객체임에도 hashCode()가 달라 다른 버킷에 저장되어 중복 체크가 실패한다.

**Q. equals()와 hashCode() 재정의 시 주의점은?**
> 항상 같이 재정의해야 하고, 두 메서드 모두 같은 필드 기준으로 재정의해야 한다.  
> 다른 필드 기준으로 재정의하면 equals()는 true인데 hashCode()가 다른 경우가 생긴다.

**Q. 기본 equals()는 뭘 비교하나요?**
> Object에 정의된 기본 equals()는 주소값(참조)을 비교한다.  
> 내용이 같아도 다른 객체면 false가 나오기 때문에 내용 비교가 필요하면 재정의해야 한다.