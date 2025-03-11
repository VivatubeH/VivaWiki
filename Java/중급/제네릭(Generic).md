제네릭(Generic)의 필요성
--------------------------------
- 다양한 타입을 담는 박스가 필요하다면, 각각의 타입별로 별도의 Box 클래스들을 새로 만들어야 하는 문제가 있었습니다.
- 예를들면, 단순히 숫자와 문자열을 담고 제공만 하는 경우에 StringBox, IntegerBox 등 클래스를 계속 만들어야 했습니다.

Object 타입을 사용하면 해결되지 않을까
------------------------------------
- Object를 사용하면 모든 타입을 담을 수 있으므로, Object로 담으면 다 해결될 것만 같습니다.

```java
ObjectBox integerBox = new ObjectBox();
integerBox.set(10);
Integer integer = (Integer) integerBox.get(); //Object -> Integer 캐스팅
System.out.println("integer = " + integer);

ObjectBox stringBox = new ObjectBox();
stringBox.set("hello");
String str = (String) stringBox.get(); //Object -> String 캐스팅
System.out.println("str = " + str);

//잘못된 타입의 인수 전달시
integerBox.set("문자100");
Integer result = (Integer) integerBox.get(); // String -> Integer 캐스팅 예외
System.out.println("result = " + result);
```
- 그러나, 담은 값을 꺼낼 때 자식에 부모를 담을 수 없기 때문에 자식 타입으로 (Integer)와 같이 다운캐스팅을 해야만 하는 문제가 있었습니다.
- 또한 개발자가 integerBox에는 숫자 타입을 입력하기 원하더라도 잘못된 타입을 전달해도 컴파일 시에는 자바 입장에서 아무 문제가 없는 걸로 인식이 되었습니다.

정리
-------------------------------------
- 다형성을 활용해서 코드 중복을 제거하고, 기존 코드를 재사용할 수 있었습니다.
- 하지만 이런 방식으로는 의도하지 않은 타입의 입력 및 위험한 다운 캐스팅을 매번 시도해야 하는 타입 안전성 문제까지 해결할 수는 없었습니다.

제네릭의 적용
-----------------------------------------
```java
package generic.ex1;

public class GenericBox<T> {

    private T value;

    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}
```
- 위처럼 <>를 사용한 클래스를 제네릭 클래스라고 합니다. 보통 <> 기호를 다이아몬드라고 부릅니다.
- 제네릭 클래스에서는 Integer, String 같은 타입을 미리 결정하지 않고 클래스명 우측에 <T>와 같이 선언하면 제네릭 클래스가 됩니다.
- T를 타입 매개변수라고 하는데, 타입 매개변수는 이후에 Integer, String으로 변할 수 있고 클래스 내부에 T 타입이 필요한 곳에 타입 매개변수를 적으면 됩니다.

```java
package generic.ex1;

public class BoxMain3 {
    public static void main(String[] args) {
        GenericBox<Integer> integerBox = new GenericBox<Integer>(); // 생성 시점에 T의 타입을 Integer로 결정했습니다.
        integerBox.set(10); // Integer 타입은 허용됩니다.
//        integerBox.set("문자100"); // Integer 타입만 허용되므로 컴파일 오류가 발생합니다.
        Integer integer = integerBox.get(); // Integer 타입 변환이 casting 없이 이루어집니다.
        System.out.println("integer = " + integer);

        GenericBox<String> stringBox = new GenericBox<String>(); // 생성 시점에 T의 타입을 String으로 결정했습니다.
        stringBox.set("hello"); // String 타입은 허용됩니다.
        String str = stringBox.get(); // String 타입만 변환됩니다.
        System.out.println("str = " + str);

        // 원하는 모든 타입을 사용할 수 있습니다.
        GenericBox<Double> doubleBox = new GenericBox<Double>();
        doubleBox.set(10.5);
        Double doubleValue = doubleBox.get();
        System.out.println("doubleValue = " + doubleValue);

        // 타입 추론 : 생성하는 제네릭 타입도 생략 가능합니다.
        GenericBox<Integer> integerBox2 = new GenericBox<>();
    }
}
```

- 제네릭 클래스를 사용하면 생성 시점에 원하는 타입을 지정할 수 있습니다. <> 안에 매개변수를 정의하면 됩니다.
- 참고로, 제네릭 타입을 적용한다고 해서 실제로 GenericBox<String>과 같은 코드가 만들어지는 것은 아니고, 컴파일러가 입력한 타입 정보를 기반으로 컴파일시에 타입 정보를 반영하는 것입니다.
- 타입 추론 : 자바가 스스로 타입 정보를 추론해서 개발자가 타입 정보를 생략할 수 있는 것을 타입 추론이라고 합니다.

제네릭의 핵심과 장점
---------------------------------------
- 제네릭의 핵심은 사용할 타입을 미리 결정하지 않고, 실제 사용하는 생성 시점에 타입을 결정한다는 점입니다. ( 메서드의 매개변수와 유사합니다. )
- 메서드가 매개변수에 인자를 전달해서 사용할 값을 결정한다면, 제네릭 클래스는 타입 매개변수에 타입 인자를 전달해서 사용할 타입을 결정하게 됩니다.
- 이러한 제네릭의 핵심적인 특징 때문에 개발자는 재사용성과 타입 안정성을 모두 확보할 수 있습니다.

제네릭 타입(Generic Type)
--------------------------------------
- 클래스나 인터페이스를 정의할 때 타입 매개변수를 사용하는 것을 제네릭 타입이라고 합니다.
- 참고로, 타입은 클래스 인터페이스 기본형 등을 통칭해서 부르는 말입니다.

제네릭 명명 관례
----------------------------------------------
- 일반적으로 용도에 맞는 단어의 첫 글자를 대문자로 사용하는 것이 관례입니다.
- E : Element
- K : Key
- N : Number
- T : Type
- V : Value
- S,U,V etc. : 2nd, 3th, 4th types..

제네릭 기타
-------------------------------------------------
![image](https://github.com/user-attachments/assets/061dbb50-2d8c-44da-9668-1684d2bd02b5)

- 타입 인자로 기본형의 사용은 불가능합니다. 대신 래퍼 클래스(Integer, Double 등...)의 사용은 가능합니다.

로 타입(raw type)
-------------------------------------------------
```java
package generic.ex1;
public class RawTypeMain {
  public static void main(String[] args) {
    GenericBox integerBox = new GenericBox();
    //GenericBox<Object> integerBox = new GenericBox<>(); // 권장
    integerBox.set(10);
    Integer result = (Integer) integerBox.get();
    System.out.println("result = " + result);
  }
}
```
- 제네릭 타입 사용시 <>로 타입을 지정하지 않을 수도 있는데, 이런 것을 raw type(원시타입)이라고 합니다.
- 원시타입을 사용할 경우, 내부 타입 매개변수는 Object로 사용됩니다.
- 단, 이러한 raw type은 과거 제네릭이 없던 시절의 코드와 호환을 위한 것이니 사용하지 않아야 합니다. ( Object를 사용해야 하면 <Object>로 지정해야 합니다. )



