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

제네릭 클래스의 타입 매개변수를 특정 타입으로 제한하지 않을 때 문제점
---------------------------------------------
```java
package generic.ex3;

public class AnimalHospitalV2<T> {

    private T animal;

    public void set(T animal) {
        this.animal = animal;
    }

    public void checkup() {
        animal.toString();
        animal.equals(null);

//        System.out.println("동물 이름: " + animal.getName());
        // 메서드 정의 시점에서는 T의 타입을 모르므로, Object의 기능만 쓸 수 있습니다.
//        animal.sound();
    }

    public T getBigger(T target) {
        // return animal.getSize() > target.getSize() ? animal : target;
        return null;
    }
}
```

- 메서드를 정의하는 시점에서는 T의 타입을 알 수 없어서, Object의 기능만 쓸 수 있다는 단점이 있었습니다.
- 자바 컴파일러는 T를 어떤 타입이든 받을 수 있는 모든 객체의 최종 부모인 Object로 가정하기 때문에 Object가 제공하는 메서드만 호출 가능했습니다.
- 또 어떤 타입이든 들어올 수 있어서 개발자의 의도와 다른 결과를 낳을 수 있다는 문제점도 있었습니다.

제네릭 클래스의 타입 매개변수의 제한
------------------------------------------
```java
package generic.ex3;

import generic.animal.Animal;

// Animal을 상속받은 클래스로 제네릭의 타입 매개변수를 제한합니다.
public class AnimalHospitalV3<T extends Animal>{

    private T animal;

    public void set(T animal) {
        this.animal = animal;
    }
    public void checkup() {
        System.out.println("동물 이름: " + animal.getName());
        System.out.println("동물 크기: " + animal.getSize());
        animal.sound();
    }
    public T getBigger(T target) {
        return animal.getSize() > target.getSize() ? animal : target;
    }
}
```
- 위 코드에서는 제네릭 타입 매개변수를 Animal을 상속받은 클래스로 제한했습니다.
- 이렇게 하면 자바 컴파일러는 T에 입력될 수 있는 값의 범위를 예측할 수 있기 때문에 Animal이 제공하는 기능도 사용할 수 있습니다.
- 동시에 Animal 및 그 자손만 제네릭 클래스의 타입매개변수로 들어올 수 있게 해서 타입 안전성도 같이 확보했습니다.

제네릭의 명시적 타입 인자 전달
-----------------------------------
```java
// 타입 인자(Type Argument) 명시적 전달
        System.out.println("명시적 타입 인자 전달");
        Integer result = GenericMethod.<Integer>genericMethod(i);
        Integer integerValue = GenericMethod.<Integer>numberMethod(10);
        Double doubleValue = GenericMethod.<Double>numberMethod(20.0);
```
- 사실 명시적으로 타입인자를 전달하지 않아도, 자바 컴파일러는 타입 추론을 합니다.
- 하지만, 명시적으로 타입인자를 적어주면 코드 가독성을 높이고 실수를 예방하는데 도움을 줍니다.

제네릭 메서드 쉽게 받아들이기
---------------------------------
```java
public static <T> T genericMethod(T t) {
        System.out.println("generic print: " + t);
        return t;
    }

    public static <T extends Number> T numberMethod(T t) {
        System.out.println("bound print: " + t);
        return t;
    }
```
- 이렇게 되어 있을 때 <T>와 같은 부분은 타입만 제한하는 부분이니 없다고 생각하고 보면 더 편하게 받아들일 수 있습니다.
- <T>가 없다면 위의 메서드는 public static T genericMethod(T t)가 되고 아래 메서드는 public static T numberMethod(T t)가 됩니다.
- <T>로 위는 모든 타입이 다 들어올 수 있게, 아래는 Number의 자손인 타입이나 Number 타입만 들어올 수 있게 한 것일 뿐입니다.

![image](https://github.com/user-attachments/assets/61f63164-2fdb-4912-8d08-27bc65be0036)

제네릭 메서드
-------------------------------------------------
- 클래스 전체가 아닌 특정 메서드 단위로 제네릭을 도입할 때 사용합니다.
- 제네릭 메서드의 정의 시에는 메서드의 반환 타입 앞쪽에 다이아몬드를 사용해서 타입 매개변수를 적어줍니다.
- 제네릭 메서드는 메서드를 호출하는 시점에 다이아몬드를 사용해서 <Integer>와 같이 타입을 정해서 호출합니다.

인스턴스 메서드와 static 메서드도 제네릭 메서드가 될까요?
---------------------------------------------------------
```java
class Box<T> {
    T instanceMethod(T t) {
        return t;
    }
}
```
- 인스턴스 메서드에서는 제네릭 타입 T를 사용할 수 있습니다. 이는 클래스 인스턴스를 생성할 때 타입이 정해지고, 인스턴스를 통한 메서드 호출이 이루어지기 때문입니다.

```java
class Box<T> {
    static <V> V staticMethod2(V v) {
        return v;
    }
}
```
- 반면 스태틱 메서드에서는 클래스 자체에서 호출되므로 객체와는 무관합니다. 따라서 static 메서드에서 제네릭 사용을 원한다면 메서드 호출시에 타입을 지정해주는 제네릭 메서드를 사용해야 합니다.

```java
class Box<T> {
    T instanceMethod(T t) {} // 가능합니다.
    static T staticMethod(T t) {} // 제네릭 타입의 T 사용은 불가능합니다.
}
```
- 위 예시에서 T가 정해지는 시점은 객체가 생성되는 시점이므로 static 메서드와는 무관합니다. 따라서 위와 같이 제네릭 사용은 불가합니다.

제네릭 타입 vs 제네릭 메서드
------------------------------------------
- 제네릭 타입 : 클래스나 인터페이스 수준에서 여러 타입을 처리할 수 있게 하는 것입니다. 
- 제네릭 메서드 : 메서드 단위에서만 타입을 정할 수 있게 하는 것입니다.

- 즉, 제네릭 타입은 클래스나 인터페이스가 타입을 여러 개 처리하는 것이고 제네릭 메서드는 메서드가 타입을 그때그때 다르게 처리하는 것입니다.

제네릭 메서드의 타입 매개변수 제한과 타입 추론
---------------------------------------------
```java
public static <T extends Number> T numberMethod(T t) {}
//GenericMethod.numberMethod("Hello"); // 컴파일 오류 Number의 자식만 입력 가능
```
- 위와 같이 사용하면 타입 매개변수를 Number와 그 자식들로 제한하는 것입니다.

```java
Integer result = GenericMethod.<Integer>genericMethod(i); // 타입 인자를 전달하는 경우
Integer result2 = GenericMethod.genericMethod(i); // 타입 추론
```
- 아래와 같이 타입 인자를 자바 컴파일러가 추론해서 처리하는 것이 타입 추론입니다. ( 실제로는 타입 인자가 전달됩니다. ) 

제네릭 메서드로 변환한 예시
--------------------------------
```java
 public static <T extends Animal> void checkup(T t) {
    System.out.println("동물 이름: " + t.getName());
    System.out.println("동물 크기: " + t.getSize());
    t.sound();
}
public static <T extends Animal> T getBigger(T t1, T t2) {
    return t1.getSize() > t2.getSize() ? t1 : t2;
}
```

제네릭 타입과 제네릭 메서드가 같은 이름의 타입변수를 사용할 때 우선순위
--------------------------------------------------------------------
- 제네릭 메서드가 제네릭 타입보다 더 높은 우선순위를 갖게 됩니다.
- 하지만, 이렇게 이름이 겹치는 경우 다른 이름을 쓰는 것이 당연히 권장됩니다.

와일드카드(WildCard)
-----------------------------------------------
```java
public class WildcardEx {
    static <T> void printGenericV1(Box<T> box) {
        System.out.println("T = " + box.get());
    }
    static void printWildcardV1(Box<?> box) {
        System.out.println("? = " + box.get());
    }
    static <T extends Animal> void printGenericV2(Box<T> box) {
        T t = box.get();
        System.out.println("이름 = " + t.getName());
    }
    static void printWildcardV2(Box<? extends Animal> box) {
        Animal animal = box.get();
        System.out.println("이름 = " + animal.getName());
    }
    static <T extends Animal> T printAndReturnGeneric(Box<T> box) {
        T t = box.get();
        System.out.println("이름 = " + t.getName());
        return t;
    }
    static Animal printAndReturnWildcard(Box<? extends Animal> box) {
        Animal animal = box.get();
        System.out.println("이름 = " + animal.getName());
        return animal;
    }
}
```
- 제네릭 메서드와 와일드 카드 메서드를 하나씩 사용했습니다.
- 와일드 카드는 이미 만들어진 제네릭 타입을 활용하기 위해서 사용합니다. ( 제네릭 타입이나 메서드의 선언이 아닙니다. )

```java
// 제네릭 메서드이며, Box<Dog> dogBox를 전달하는 경우
// 타입 추론에 의해 타입 T가 dog가 됩니다.
static <T> void printGenericV1(Box<T> box) {
    System.out.println("T = " + box.get());
}

// 제네릭 메서드가 아닌 일반적인 메서드입니다.
// Box<Dog> dobBox가 전달되는 경우이고
// 와일드카드 ?를 사용하면 모든 타입을 다 받을 수 있게 됩니다.
static void printWildcarV1(Box<?> box) {
    System.out.println("? = " + box.get());
}
```
- 와일드 카드는 Box<Dog> 처럼 타입 인자가 정해진 제네릭 타입을 전달받아서 활용할 때 사용할 수 있습니다.
- 와일드카드 ?는 모든 타입을 다 받을 수 있다는 뜻으로 ?는 <? extends Object>로 해석할 수 있습니다.
- 비제한 와일드카드 : ?만 사용해서 제한 없이 모든 타입을 다 받을 수 있는 와일드카드를 말합니다.

제네릭 메서드와 와일드카드의 실행 절차
---------------------------------------
```java
//1. 전달
printGenericV1(dogBox)
//2. 제네릭 타입 결정 dogBox는 Box<Dog> 타입, 타입 추론 -> T의 타입은 Dog
static <T> void printGenericV1(Box<T> box) {
System.out.println("T = " + box.get());
}
//3. 타입 인자 결정
static <Dog> void printGenericV1(Box<Dog> box) {
System.out.println("T = " + box.get());
}
//4. 최종 실행 메서드
static void printGenericV1(Box<Dog> box) {
System.out.println("T = " + box.get());
}
```

```java
//1. 전달
printWildcardV1(dogBox)
//이것은 제네릭 메서드가 아니다. 일반적인 메서드이다.
//2. 최종 실행 메서드, 와일드카드 ?는 모든 타입을 받을 수 있다.
static void printWildcardV1(Box<?> box) {
System.out.println("? = " + box.get());
}
```

와일드카드의 장점
---------------------------------------
- 제네릭 메서드는 타입 매개변수가 존재해서 특정 시점에 타입 매개변수에 타입 인자를 전달해서 타입 결정을 해야합니다.
- 하지만, 와일드카드는 일반적인 메서드에도 사용할 수 있고 단순히 매개변수로 제네릭 타입을 받을 수 있습니다. ( 즉, 일반 메서드에 제네릭 타입을 받을 수 있는 매개변수가 있는 것입니다. )

상한 와일드카드
----------------------------------------
- 와일드카드도 제네릭 메서드처럼 상한 제한을 둘 수 있습니다.

와일드카드의 본질
--------------------------------------
- 어떤 타입이든 특정 클래스와 관련만 있으면 처리할 수 있도록 타입의 유연성을 제공하자.
- 타입을 미리 정할 수 없는 경우에 사용하면 좋습니다.

```java
static <T extends Animal> void printGenericV2(Box<T> box) {
T t = box.get();
System.out.println("이름 = " + t.getName());
}
static void printWildcardV2(Box<? extends Animal> box) {
Animal animal = box.get(); // Animal 타입으로 조회 가능한 기능을 호출할 수 있습니다.
System.out.println("이름 = " + animal.getName());
}
```

타입 매개변수가 꼭 필요한 경우
--------------------------------------
```java
static <T extends Animal> T printAndReturnGeneric(Box<T> box) {
T t = box.get();
System.out.println("이름 = " + t.getName());
return t;
}

Dog dog = WilcardEx.printAndRetrunGeneric(dogBox);

static Animal printAndReturnWildcard(Box<? extends Animal> box) {
Animal animal = box.get();
System.out.println("이름 = " + animal.getName());
return animal;
}

Animal animal = WildcardEx.printAndReturnWildCard(dogBox);

```
- 제네릭을 사용한 위의 경우, 전달한 타입을 명확하게 반환할 수 있습니다.
- 하지만 와일드카드를 사용한 경우 전달한 타입을 명확하게 반환할 수 없습니다.

하한 와일드카드
--------------------------------------------------
```java
package generic.ex5;
import generic.animal.Animal;
import generic.animal.Cat;
import generic.animal.Dog;
public class WildcardMain2 {
public static void main(String[] args) {
Box<Object> objBox = new Box<>();
Box<Animal> animalBox = new Box<>();
Box<Dog> dogBox = new Box<>();
Box<Cat> catBox = new Box<>();
// Animal 포함 상위 타입 전달 가능
writeBox(objBox);
writeBox(animalBox);
//writeBox(dogBox); // 하한이 Animal
//writeBox(catBox); // 하한이 Animal
Animal animal = animalBox.get();
System.out.println("animal = " + animal);
}

static void writeBox(Box<? super Animal> box) {
        box.set(new Dog("멍멍이", 100));
    }
}
```
- 하한 와일드카드를 사용하면 ?가 Animal을 포함한 Animal의 상위 타입만 입력받을 수 있습니다.

타입 이레이저
---------------------------------------------------
- 제네릭은 컴파일 단계에서만 사용되고, 컴파일 이후 런타임에는 제네릭 정보는 삭제됩니다.
- 즉, 컴파일 전인 .java에는 제네릭의 타입 매개변수가 존재하지만 컴파일 이후인 .class에는 타입 매개변수가 존재하지 않습니다.
- 핵심은 개발자가 캐스팅 하는 코드를 쓰는 대신 컴파일러가 대신 처리해준다는 것입니다.

타입 이레이저의 한계
--------------------------------------
```java
class EraserBox<T> {
    public boolean instanceCheck(Object param) {
        return param instanceof T; // 오류
    }
    public T create() {
        return new T(); // 오류
    }
}
```
- 위와 같이 소스코드를 작성하게 되면,
```java
class EraserBox {
    public boolean instanceCheck(Object param) {
        return param instanceof Object; // 오류
    }
    public T create() {
        return new Object(); // 오류
    }
}
```
- 런타임에는 T가 모두 Object가 되어버립니다. ( 런타임 시에는 타입이 지워져버립니다. )
- instanceof는 Object와 비교하면 항상 참이되는 문제가 있고, new Object는 개발자의 의도와 다르기 때문에 둘 다 자바에서는 허용하지 않습니다.

제네릭 메서드의 타입 파라미터의 위치
---------------------------------------------------
- 제네릭 메서드에서 타입 파라미터는 반환타입 앞에 명시하는 것이 규칙입니다.


