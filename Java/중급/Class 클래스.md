Class 클래스
--------------------------------------------------
- 자바에서 클래스의 정보(메타데이터)를 다루는 데 사용되는 클래스입니다.
- Class 클래스를 통해서 개발자는 애플리케이션 내에서 필요한 클래스의 속성과 메서드에 대한 정보를 조회하고 조작할 수 있습니다.

Class 클래스의 주요 기능
--------------------------------------------------
- 타입 정보 : 클래스 이름, 슈퍼클래스, 인터페이스, 접근 제한자 등의 정보를 조회할 수 있습니다.
- 리플렉션 : 클래스에 정의된 메서드, 필드, 생성자 등을 조회하고 이를 통해 객체 인스턴스를 생성하거나 메서드 호출 등의 작업을 할 수 있습니다.
- 동적 로딩과 생성 : Class.forName() 메서드를 사용해서 클래스를 동적으로 로드하고, newInstance()를 통해 새로운 인스턴스를 생성할 수 있습니다.
- 애노테이션 처리 : 클래스에 적용된 어노테이션(annotation)을 조회하고 처리하는 기능을 제공합니다.

```java
Class clazz = String.class; // 1. 클래스에서 조회
Class clazz = new String().getClass(); // 2. 인스턴스에서 조회 
Class clazz = Class.forName("java.lang.String"); // 3. 문자열로 조회
```

- class라는 예약어가 있어서 관행으로 clazz라는 이름을 사용해서, 해당 단어가 class를 뜻함을 알아볼 수 있게 합니다.
- 위와 같은 방법으로 Class를 조회할 수 있습니다.

Class 클래스의 메서드들
--------------------------------------
- getDeclaredFields() : 클래스의 모든 필드를 조회합니다.
- getDeclaredMethods() : 클래스의 모든 메서드를 조회합니다.
- getSuperClass() : 클래스의 부모 클래스를 조회합니다.
- getInterfaces() : 클래스의 인터페이스들을 조회합니다.

```java
import java.lang.reflect.Field;
import java.lang.reflect.Method;

public class Main {
    public static void main(String[] args) {
        // 클래스 조회
        Class clazz = String.class;
        // 클래스의 모든 필드를 조회합니다.
        Field[] fields = clazz.getDeclaredFields();
        // 클래스의 모든 메서드들을 조회합니다.
        Method[] methods = clazz.getDeclaredMethods();
        for (Field field : fields) {
            System.out.println("클래스의 필드는 : " + field);
        }

        System.out.println();

        for (Method method : methods) {
            System.out.println("클래스의 메서드는 : " + method);
        }

        System.out.println();

        // 부모 클래스를 조회합니다.
        System.out.println("부모 클래스는 : " + clazz.getSuperclass());

        System.out.println();

        // 인터페이스들을 조회합니다. 
        Class<?>[] classes = clazz.getInterfaces();
        for(Class<?> clazz1 : classes) {
            System.out.println("인터페이스는 : " + clazz1);
        }
   }
}
```

<img width="1049" alt="image" src="https://github.com/user-attachments/assets/1931ecab-c2af-4d4a-9fa2-59acc9063856" />
<img width="597" alt="image" src="https://github.com/user-attachments/assets/1fda3f5d-8799-44f4-ab17-9ebe11a0b35f" />

Class를 기반으로 클래스 생성하기
------------------------------------
```java
package lang.clazz;
        
   public class Hello {
      public String hello() {
          return "hello!";
      }
}
```
```java
package lang.clazz;
public class ClassCreateMain {
  public static void main(String[] args) throws Exception {
    //Class helloClass = Hello.class;
    Class helloClass = Class.forName("lang.clazz.Hello"); // Class.forName을 통해 해당 클래스의 객체를 생성합니다.
    Hello hello = (Hello) helloClass.getDeclaredConstructor().newInstance(); 
    String result = hello.hello();
    System.out.println("result = " + result);
  }
}
```
- getDeclaredConstructor() : 생성자를 선택합니다.
- newInstance() : 선택한 생성자를 기반해서 인스턴스를 생성합니다.

리플렉션(reflection)
------------------------------------------
- Class를 통해 클래스의 메타 정보를 기반으로해서 클래스의 세부 내용을 조회 및 객체 생성 및 메서드 호출 작업등이 가능합니다.
- 이러한 작업들을 리플렉션이라고 합니다. ( 추가로 어노테이션을 읽어서 특별한 기능을 수행할 수도 있습니다. )

System 클래스
---------------------------------------
System과 관련된 기본 기능들을 제공하는 클래스입니다.

```java
import java.util.Arrays;
public class Main {
    public static void main(String[] args) {
        // 현재 시간(밀리초)를 가져온다.
        long currentTimeMillis = System.currentTimeMillis();
        System.out.println("currentTimeMillis: " + currentTimeMillis);
        // 현재 시간(나노초)를 가져온다.
        long currentTimeNano = System.nanoTime();
        System.out.println("currentTimeNano: " + currentTimeNano);
        // 환경 변수를 읽는다.
        System.out.println("getenv = " + System.getenv());
        // 시스템 속성을 읽는다.
        System.out.println("properties = " + System.getProperties());
        System.out.println("Java version: " + System.getProperty("java.version"));
        // 배열을 고속으로 복사한다.
        char[] originalArray = new char[]{'h', 'e', 'l', 'l', 'o'};
        // arraycopy를 통해 원래 배열의 0번부터 복사할 배열의 0번으로 배열 크기만큼 복사합니다.
        char[] copiedArray = new char[5];
        System.arraycopy(originalArray, 0, copiedArray, 0, originalArray.length);
        // 배열을 출력합니다.
        System.out.println("copiedArray = " + copiedArray);
        System.out.println("Arrays.toString = " + Arrays.toString(copiedArray));
        //프로그램 종료
        System.exit(0);
    }
}
```

- System.in : 표준 입력 스트림을 나타냅니다.
- System.out : 표준 출력 스트림을 나타냅니다.
- System.err : 표준 오류 스트림을 나타냅니다.
- System.currentTimeMillis(), System.nanoTime() : 현재 시간을 밀리초 또는 나노초 단위로 제공합니다.
- System.getenv() : OS에서 설정한 환경변수의 값을 얻을 수 있습니다.
- System.getProperties(), System.getProperty(String key) : 현재 시스템 속성들을 얻거나 특정 시스템 속성을 얻을 수 있습니다.
- System.exit(int status) : 프로그램을 종료하고, OS에 프로그램 종료 상태 코드를 전달합니다. ( 0 : 정상 종료, 그 외 : 오류나 예외 )
- System.arraycopy : 시스템 레벨에서 최적화된 메모리 복사 연산을 사용합니다. ( 반복문보다 수배 이상 빠릅니다. )

Math
---------------------------
수학 문제를 해결해주는 클래스입니다.

<img width="411" alt="image" src="https://github.com/user-attachments/assets/c6a75e2d-e45a-4e96-8b55-a605d9795f43" />

```java
System.out.println("max(10, 20): " + Math.max(10, 20)); // 최대값
System.out.println("min(10, 20): " + Math.min(10, 20)); // 최소값
System.out.println("abs(-10): " + Math.abs(-10)); // 절대값

System.out.println("ceil(2.1): " + Math.ceil(2.1)); // 올림
System.out.println("floor(2.7): " + Math.floor(2.7)); // 내림
System.out.println("round(2.5): " + Math.round(2.5)); // 반올림

System.out.println("sqrt(4): " + Math.sqrt(4)); //제곱근
System.out.println("random(): " + Math.random()); //0.0 ~ 1.0 사이의 double 값
```

- 참고로 아주 정밀한 숫자와 반올림 계산이 필요할 때는 BigDecimal을 검색해봅시다.

Random 클래스
-----------------------------------
- 랜덤의 경우 Math.random() 보다 Random 클래스를 통하면 더 다양한 랜덤값을 구할 수 있습니다. 
- 참고로, Math.random()도 내부적으로는 Random 클래스를 사용합니다.

```java
// 랜덤 객체를 생성합니다.
Random random = new Random();
random.nextInt(); // 랜덤 int 값을 반환합니다.
random.nextDouble(); // 랜덤 double 값을 반환합니다. ( 0.0d ~ 1.0d 사이의 값입니다. )
random.nextBoolean(); // 랜덤 boolean 값을 반환합니다.
random.nextInt(int bound); // 0에서 bound 미만의 정수를 랜덤으로 반환합니다. ( 3 입력시 0, 1, 2를 반환합니다. )
```
- 따라서 1부터 특정 범위의 int 범위 숫자를 구할 때는 nextInt(int bound)의 결과에 +1을 하면 됩니다.

랜덤의 씨드(Seed)
-----------------------
- 랜덤은 내부에서 씨드(Seed) 값을 이용해서 랜덤값을 구하기 때문에 씨드 값이 같으면 항상 같은 결과가 출력됩니다.

```java
import java.util.Random;
public class Main {
    public static void main(String[] args) {
        Random random1 = new Random(1);
        Random random2 = new Random(1);
        for(int i = 0; i < 10; i++) {
            System.out.println(random1.nextInt(10));
            System.out.println(random2.nextInt(10));
        }
    }
}
```

- 두 랜덤객체가 씨드가 같으니 데칼코마니 같은 결과가 출력되고 있습니다.
<img width="292" alt="image" src="https://github.com/user-attachments/assets/7dce99e7-1407-4a95-b42d-16e3bee2ae4b" />
