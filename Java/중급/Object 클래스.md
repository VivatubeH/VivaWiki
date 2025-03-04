java.lang 패키지
--------------------------------------------------
- 자바가 기본으로 제공하는 라이브러리(클래스의 모음) 중 가장 기본이 되는 것이 java.lang 패키지입니다. ( lang = language )
- 따로 import문을 사용하지 않아도 모든 자바 애플리케이션에 자동으로 임포트됩니다.
  
java.lang 패키지의 클래스들
--------------------------------------------------
#### Object : 모든 자바 객체의 부모 클래스입니다.
#### String : 문자열 클래스입니다.
#### Integer, Long, Double : 기본형 데이터 타입을 참조형으로 만든 클래스입니다. ( 래퍼 타입 )
#### Class : 클래스와 관련된 메타 정보를 다루는 클래스입니다.
#### System : 시스템과 관련된 기본 기능을 제공하는 클래스입니다.

```java
package lang;

import java.lang.System; // 해당 import문은 생략 가능합니다.

public class LangMain {
  public static void main(String[] args) {
    System.out.println("hello java");
  }
}
```

Object 클래스
-------------------------------------------------
- 자바에서 모든 클래스의 최상위 클래스입니다.
- 해당 클래스의 부모 클래스가 없다면 묵시적으로 Object 클래스를 상속받도록 되어 있습니다.
- 그래서 보통 extends Object는 생략합니다. ( 자바가 자동으로 넣어줍니다. )

```java
//extends Object 추가
public class Parent extends Object { // extends Object를 생략해도 자바가 묵시적으로 Object를 상속시킵니다.
  public void parentMethod() {
    System.out.println("Parent.parentMethod");
  }
}
```

![image](https://github.com/user-attachments/assets/04bca923-9251-46ec-bd4e-b5186e0dc2bb)

묵시적 vs 명시적
---------------------------------------
- 묵시적(Implicit) : 개발자가 코드에 기술하지 않아도 시스템이나 컴파일러에 의해 자동으로 수행되는 것을 의미합니다.
- 명시적 : 개발자가 직접 코드에 기술해서 작동하는 것을 의미합니다.

Object의 여러 메서드들
---------------------------------
- toString() : 객체의 정보를 문자열 형태로 제공합니다. -> 이 때, 객체 정보는 패키지를 포함한 객체의 이름과 객체의 참조값(해시코드)를 16진수로 제공합니다.
- equals() : 객체의 같음을 비교합니다.
- getClass() : 객체의 클래스 정보를 제공합니다.

```java
public class ToStringMain1 {
  public static void main(String[] args) {
    Object object = new Object();
    String string = object.toString();
    //toString() 반환값 출력
    System.out.println(string); // 결과 java.lang.Object@a09ee92
    //object 직접 출력 
    System.out.println(object); // 결과 java.lang.Object@a09ee92
  }
}

public String toString() {
  return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```
Object 클래스를 최상위 부모 클래스로 사용하는 이유
--------------------------------------------------------------
- 객체마다 공통적으로 필요한 기능들을 일관성 있는 이름으로 통일해서 제공하기 위해서 사용합니다.
- 다형성에 따라, 타입이 다른 객체들을 어딘가에 보관하고 싶다면 -> 최상위 부모클래스인 Object에 담아서 보관할 수 있다는 장점이 있습니다.

Object 배열
--------------------------------------------------------------
- Object[] 배열을 사용하면 세상의 모든 타입의 객체들을 담을 수 있습니다.
- 즉, Object가 있기 때문에 표준화된 방법으로 모든 개발자들이 모든 객체를 다룰 수 있게 됩니다.

```java
public class ObjectPolyExample2 {
  public static void main(String[] args) {
    Dog dog = new Dog();
    Car car = new Car();
    Object object = new Object(); //Object 인스턴스도 만들 수 있다.

    Object[] objects = {dog, car, object};
    size(objects);
}

  private static void size(Object[] objects) {
    System.out.println("전달된 객체의 수는: " + objects.length);
  }
}
```

System.out.println()과 toString()의 관계
----------------------------------------------
- 자식을 포함한 Object 타입이 println()의 인수로 전달되면, 내부에서는 obj.toString()을 호출해서 결과를 출력합니다.
- 그래서 println() 사용 시 toString()을 호출하지 않고 객체를 전달합니다.
  
```java
// println을 호출하게 되면
public void println(Object x) { // 내부적으로 Object 매개변수를 사용합니다. -> 이는 다형성을 활용하는 예시로 볼 수 있습니다.
  String s = String.valueOf(x);
  //...
}
// 내부적으로 toString을 호출하게 됩니다.
public static String valueOf(Object obj) {
  return (obj == null) ? "null" : obj.toString();
}
```

참고) toString()이나 hashCode() 재정의 시 객체의 참조값 출력 방법
---------------------------------------------------------------

```java
String refValue = Integer.toHexString(System.identityHashCode(dog1));
System.out.println("refValue = " + refValue);
```

의존한다의 개념
--------------------------------------------------------------
- 보통 클래스에서 A 클래스가 B 클래스를 사용하게 되면, A 클래스는 B 클래스에 의존한다고 표현합니다.

```java
// ObjectPrinter 클래스가 Object 클래스에 의존하고 있습니다.
public class ObjectPrinter {
  public static void print(Object obj) {
    String string = "객체 정보 출력: " + obj.toString();
    System.out.println(string);
  }
}
```

참고) 추상적의 개념
------------------------------------------------------
- 보통은 부모 타입으로 올라갈수록 개념이 더 추상적이고, 하위 타입으로 내려갈수록 개념이 더 구체적이게 됩니다.

참고) 정적 의존관계 vs 동적 의존관계
--------------------------------------------------------
- 정적 의존관계 : 컴파일 시간에 결정되는 의존 관계입니다. ( 주로 클래스간의 관계를 의미합니다. 프로그램 실행 없이도 클래스 내의 타입으로 의존관계 파악이 수비습니다. )
- 동적 의존관계 : 런타임에 확인할 수 있는 의존 관계입니다. ( 예를 들어, ObjectPrinter.print(Object obj)라는 메서드라면 인자로 전달되는 객체는 런타임에 결정됩니다. )
- 보통의 의존관계라고 하면 주로 정적 의존관계를 말합니다.

equals()로 보는 동일성과 동등성
---------------------------------------------
- 동일성(Identity) : == 연산자를 사용해서 두 객체의 '참조가 같은 객체를 가리키고 있는지'를 확인합니다.
- 동등성(Equality) : equals() 메서드를 사용해서 두 객체가 '논리적으로 동등한지'를 확인합니다. 

```java
package lang.object.equals;
public class EqualsMainV1 {
  public static void main(String[] args) {
    UserV1 user1 = new UserV1("id-100");
    UserV1 user2 = new UserV1("id-100");
    System.out.println("identity = " + (user1 == user2)); // false
    System.out.println("equality = " + user1.equals(user2)); // false -> equals()를 오버라이딩 하지 않은 경우 Object의 equals()를 사용하는데, Object.equals()는 ==로 동일성 비교를 제공합니다.
  }
}
```

```java
public class UserV2 {
  private String id;
  public UserV2(String id) {
    this.id = id;
}
@Override 
  public boolean equals(Object obj) { 
    UserV2 user = (UserV2) obj; 
    return id.equals(user.id); // String.equals()는 동등성 비교를 하도록 오버라이딩 되어 있기 때문에 앞선 결과에서 true가 반환될 것입니다.
  }
}
```

참고) equals()의 구현 규칙
------------------------------------------
- 실무에서는 equals()를 IDE가 generator를 통해 만들어주는 걸 사용하니, 읽어보고 넘어갑시다.
- 반사성(Reflexivity) : 객체는 자기 자신과 동등해야 합니다. ( x.equals(x)는 항상 true여야 합니다. )
- 대칭성(Symmetry) : 두 객체가 서로에 대해 동일하다고 판단되면, 양방향을 동일해야 합니다. ( x.equals(y)가 true일 때, y.equals(x)도 true여야 합니다. )
- 추이성(Transitivity) : 1번 객체가 2번 객체와 동일하고, 2번 객체가 3번 객체와 동일하면 1번 객체는 3번 객체와도 동일해야 합니다.
- 일관성(Consistency) : 두 객체의 상태가 변경되지 않는 한 equals()는 항상 동일한 값을 반환해야 합니다.
- null 비교 : 모든 객체는 null과 비교하면 false를 반환해야 합니다.  

