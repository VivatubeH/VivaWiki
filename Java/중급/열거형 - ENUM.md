열거형(ENUM)의 필요성
----------------------------
```java
// 존재하지 않는 등급
int vip = discountService.discount("VIP", price);
System.out.println("VIP 등급의 할인 금액: " + vip);
// 오타
int diamondd = discountService.discount("DIAMONDD", price);
System.out.println("DIAMONDD 등급의 할인 금액: " + diamondd);
// 소문자 입력
int gold = discountService.discount("gold", price);
System.out.println("gold 등급의 할인 금액: " + gold);
```
- 기존에 문자열을 사용하는 방식은 오타가 나도 오류 검출이 안 되어서, 오타인지도 알 수 없었습니다.
- 즉, 타입 안정성이 부족하고 데이터의 일관성이 떨어졌습니다.
- 그에 따라 특정 범위로 값을 제한해야만 하는데 단순히 문자열로는 범위를 제한할 방법이 없었습니다.

```java
public static final String BASIC = "BASIC";
public static final String GOLD = "GOLD";
public static final String DIAMOND = "DIAMOND";

public int discount(String grade, int price) {}
```

- 그에 따라, 그러면 변경할 수 없는 문자열 상수를 사용하는 방식을 사용할 수 있습니다.
- 이렇게 하면 오류를 컴파일 단계에서 쉽게 찾을 수 있게 됩니다.
- 하지만, 근본적으로 만약 개발자가 문자열 상수를 사용하지 않고 직접 문자열을 사용하는 것은 막을 수 없었습니다.
- 그리고 메서드를 호출하는 개발자가 식별할 수 없다는 한계가 있었습니다.

타입 안전 열거형 패턴 (Type-Safe Enum Pattern)
--------------------------------------------------
말 그대로 타입에 안전한, 항목들을 열거하는 것을 말합니다.

```java
public class ClassGrade {
  public static final ClassGrade BASIC = new ClassGrade();
  public static final ClassGrade GOLD = new ClassGrade();
  public static final ClassGrade DIAMOND = new ClassGrade();
}
```
- 회원 등급을 다루는 클래스에, 등급별로 상수를 선언했습니다.

```java
public int discount(ClassGrade classGrade, int price) {
  int discountPercent = 0;
  if (classGrade == ClassGrade.BASIC) {
    discountPercent = 10;
  } else if (classGrade == ClassGrade.GOLD) {
    discountPercent = 20;
  } else if (classGrade == ClassGrade.DIAMOND) {
    discountPercent = 30;
  } else {
    System.out.println("할인X");
  }
    return price * discountPercent / 100;
  }
```
- 타입 안전 열거형 패턴을 직접 구현했을 때는, 메서드를 사용하려는 개발자도 ClassGrade가 가진 상수 중 하나만을 사용할 수 있습니다.
- 하지만, 이 방법 역시 외부에서 임의로 ClassGrade의 인스턴스를 생성할 수 있다는 문제점이 존재합니다.

```java
public class ClassGrade {
    public static final ClassGrade BASIC = new ClassGrade();
    public static final ClassGrade GOLD = new ClassGrade();
    public static final ClassGrade DIAMOND = new ClassGrade();
    //private 생성자 추가
    private ClassGrade() {}
}
```

- 그런 문제점을 막기 위해 생성자를 private으로 선언하면 더 이상 ClassGrade 타입의 객체를 외부에서 임의로 생성할 수 없게 됩니다.
- 즉, private 생성자까지 사용하면 앞서 열거한 BASIC, GOLD, DIAMOND 상수만 사용 가능합니다.

타입 안전 열거형 패턴(Type-Safe Enum Pattern)의 장단점
------------------------------------------------------
- 장점 : 외부에서는 클래스에서 사전에 정의한 몇 개의 인스턴스와 정의된 값들만 사용하게 되어서, 타입 안정성 및 데이터의 일관성이 보장됩니다.
- 단점 : 코드가 길어지고 private 생성자 추가 등 신경써야 할 부분이 늘어납니다.

열거형(Enum Type)
------------------------------------------------------
열거형은 앞에서 설명한 타입 안전 열거형 패턴을 편리하게 사용할 수 있도록 자바가 지원하는 방법입니다.

```java
public class Grade extends Enum {
    public static final Grade BASIC = new Grade();
    public static final Grade GOLD = new Grade();
    public static final Grade DIAMOND = new Grade();
    //private 생성자 추가
    private Grade() {}
}
```

- 기존 방식은 이렇게 직접 열거형 패턴을 구현해야만 했습니다.

```java
public enum Grade {
  BASIC, GOLD, DIAMOND
}
```

- 자바의 열거형 사용은 class 대신 enum을 사용해서, 원하는 상수의 이름을 단순히 나열만 하면 됩니다.
- 참고로 열거형 역시 enum 키워드를 사용하지만 클래스입니다.

```java
public class DiscountService {

    public int discount(Grade grade, int price) {
        int discountPercent = 0;

        if (grade == Grade.BASIC) {
            discountPercent = 10;
        } else if (grade == Grade.GOLD) {
            discountPercent = 20;
        } else if (grade == Grade.DIAMOND) {
            discountPercent = 30;
        } else {
            System.out.println("할인X");
        }
        return price * discountPercent / 100;
    }
}

enum Grade {
    BASIC, GOLD, DIAMOND;
}
```

- 사용법은 앞선 타입 안전 열거형 패턴의 구현 코드와 동일합니다.
- 장점으로 열거형은 switch 문에 사용할 수도 있습니다.
- 물론, 직접 열거형 객체를 생성하는 것은 불가능합니다.

```java
Grade myGrade = new Grade(); // enum 생성 불가
```

열거형(ENUM)의 장점
-----------------------------------
- 앞선 타입 안전 열거형 패턴처럼 타입 안정성이 있습니다.
- 또한 간결한 코드 작성이 가능해서 확장성이 좋습니다.
- 참고로 열거형 사용시에는 static import를 잘 쓰면 읽기 좋은 코드를 만들 수 있습니다.


열거형의 주요 메서드
-------------------------------------
- 모든 열거형은 java.lang.Enum 클래스를 자동으로 상속받습니다.
```java
    public static void main(String[] args) {
        //모든 ENUM 반환
        Grade[] values = Grade.values();
        System.out.println("values = " + Arrays.toString(values));
        for (Grade value : values) {
            System.out.println("name=" + value.name() + ", ordinal=" +
                    value.ordinal());
        }
        //String -> ENUM 변환, 잘못된 문자면 IllegalArgumentException 발생
        String input = "GOLD";
        Grade gold = Grade.valueOf(input);
        System.out.println("gold = " + gold); //toString() 오버라v이딩 가능
    }
```
- values() : 모든 ENUM 상수를 포함하는 배열을 반환합니다.
- valueOf(String name) : 주어진 이름과 일치하는 ENUM 상수를 반환합니다.
- name() : ENUM 상수의 이름을 문자열로 반환합니다. 
- ordinal() : ENUM 상수의 선언 순서(0부터 시작)를 반환합니다. ( oridinal 사용은 지양합니다. -> 중간에 상수가 추가되면 값이 달라져버립니다. )
- toString() : ENUM 상수의 이름을 문자열로 반환합니다. ( 오버라이딩이 가능하다는 게 차이점입니다. )

열거형의 특징 정리
-------------------------------------------------
- java.lang.Enum을 자동으로 상속받기 때문에 추가로 다른 클래스는 상속받을 수 없습니다.
- 단, 인터페이스는 구현할 수 있고 추상 메서드 선언 및 구현이 가능합니다. ( 익명 클래스 방식으로 사용합니다. )

```java
enum Grade {
    BASIC(10), GOLD(20), DIAMOND(30);

    private final int discountPercent;

    Grade(int discountPercent) {
        this.discountPercent = discountPercent;
    }
}
```
- 열거형 상수에 괄호를 열고 생성자에 맞는 인수를 전달하면 적절한 생성자가 호출됩니다.
- 이는 열거형 상수가 궁극적으로는 객체이기 때문에 가능합니다.
- 즉, BASIC, GOLD, DIAMOND는 Grade 타입의 객체입니다.
