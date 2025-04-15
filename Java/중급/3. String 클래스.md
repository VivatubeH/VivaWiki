String 클래스
-----------------------------
- 자바에서 문자열을 다루기 위해 사용됩니다. 
- char[]로 문자열을 다루는 방식은 비효율적이라 보통 String 클래스를 사용합니다.
  
String 클래스의 객체 생성 방법
-----------------------------------------------
```java
String str1 = "hello"; // 이렇게만 작성해도
String str1 = new String("hello"); // 자바 언어에서는 new String()으로 변경해줍니다.
```

- 자바에서는 문자열을 자주 사용하기 때문에, 큰따옴표로만 써도 new String으로 변경해줍니다.

String 클래스의 구조
---------------------------------------
```java
public final class String {
  //문자열 보관
  private final char[] value;// 자바 9 이전 
  private final byte[] value;// 자바 9 이후
  //여러 메서드
  public String concat(String str) {...}
  public int length() {...}
  ...
}
```
- String 클래스라고 char[]를 사용하지 않는 것이 아니라, char[]를 내부에 감추고 String을 클래스로 제공하는 방식입니다.
- 자바 9부터는 char[] 대신 byte[]를 사용합니다. 이는 char는 2바이트인데 비해서 영어, 숫자는 1byte로 표현 가능하기 때문에 메모리를 더 효율적으로 사용할 수 있습니다.

String의 메서드
-------------------------------------------------
- length() : 문자열의 길이를 반환합니다.
- charAt(int index) : 특정 인덱스를 문자를 반환합니다.
- substring(int beginIndex, int endIndx) : 문자열의 부분 문자열을 반환합니다.
- indexOf(String str) : 특정 문자열이 시작되는 인덱스를 반환합니다.
- toLowerCase(), toUpperCase() : 문자열을 소문자 또는 대문자로 변환합니다.
- trim() : 문자열 양 끝의 공백을 제거합니다.
- concat(String str) : 문자열을 이어 붙입니다.

String의 + 연산자 사용
---------------------------------------------------------
- 원래 참조형에는 x001처럼 계산할 수 없는 참조값이 들어있습니다. 그래서 원칙적으로는 + 연산을 사용할 수 없습니다.
- 그러나 자바에서 문자열 결합은 워낙 자주 다루어지기에 편의상 + 연산이 제공됩니다.

String 클래스의 비교
----------------------------------------------------------
- 동일성(Identity) : == 연산자를 이용해서 두 객체의 참조가 동일한 객체를 가리키는지를 확인합니다.
- 동등성(Equality) : equals() 메서드를 이용해서 두 객체가 논리적으로 같은 지를 확인합니다.
- 따라서 String 클래스의 비교에는 ==이 아닌 equals()를 사용합니다.

```java
public class StringEqualsMain1 {
  public static void main(String[] args) {
    String str1 = new String("hello");
    String str2 = new String("hello");
    System.out.println("new String() == 비교: " + (str1 == str2));
    System.out.println("new String() equals 비교: " + (str1.equals(str2)));
    String str3 = "hello";
    String str4 = "hello";
    System.out.println("리터럴 == 비교: " + (str3 == str4));
    System.out.println("리터럴 equals 비교: " + (str3.equals(str4)));
  }
}
```

자바의 문자열 풀(String Pool)
------------------------------------------------------------------------------------------
- 자바에서는 String str3 = "hello"와 같이 문자열 리터럴을 사용하는 경우, 메모리 효율성과 성능 최적화를 위해 문자열 풀이라는 것을 사용합니다. -> 힙 영역을 사용합니다.
- 만약 자바 실행 시점에 클래스에 문자열 리터럴이 있다면, 문자열 풀에 해당 String 인스턴스를 미리 생성해둡니다.
- 만약 이미 같은 문자열이 있다면 만들지 않습니다.

![image](https://github.com/user-attachments/assets/69d2dbba-3224-4490-b462-1c2821d421ce)

프로그래밍에서의 풀(Pool)
---------------------------------
- 프로그래밍에서 풀(pool)은 보통 공용 자원이 모여있는 곳을 의미합니다.

 String의 불변성
 ------------------------------------
 ```java
  public static void main(String[] args) {
    String str = "hello";
    str.concat(" java"); // 새로운 String 객체가 생성됩니다.
    System.out.println("str = " + str); // 기존의 String 객체의 hello가 출력됩니다.
}
```

- String은 불변 객체이기 때문에 기존 객체의 값은 변하지 않습니다.

String의 메서드 - 문자열 정보 조회
--------------------------------------------
```java
public class StringInfoMain {
  public static void main(String[] args) {
    String str = "Hello, Java!";
    System.out.println("문자열의 길이: " + str.length()); // 12
    System.out.println("문자열이 비어 있는지: " + str.isEmpty()); // false
    System.out.println("문자열이 비어 있거나 공백인지1: " + str.isBlank()); // false
    System.out.println("문자열이 비어 있거나 공백인지2: " + " ".isBlank()); // true
    char c = str.charAt(7); 
    System.out.println("7번 인덱스의 문자: " + c); // J
    }
}
```

- length() : 문자열의 길이를 반환합니다.
- isEmpty() : 문자열이 비어있는지 ( 길이가 0인지 )를 확인합니다.
- isBlank() : 문자열이 비어있는지 ( 길이가 0 또는 공백만 있는지)를 확인합니다. -> 자바 11부터 도입되었습니다.
- charAt(int index) : 지정된 인덱스에 있는 문자를 반환합니다.

String의 메서드 - 문자열 비교
---------------------------------------------------
```java
    public static void main(String[] args) {
        String str1 = "Hello, Java!"; // 대문자 일부 있는 경우
        String str2 = "hello, java!"; // 대문자 없음 모두 소문자
        String str3 = "Hello, World!"; 
        System.out.println("str1 equals str2: " + str1.equals(str2)); // false
        System.out.println("str1 equalsIgnoreCase str2: " + str1.equalsIgnoreCase(str2)); // true
        System.out.println("'b' compareTo 'a': " + "b".compareTo("a")); // 1 
        System.out.println("str1 compareTo str3: " + str1.compareTo(str3)); // -13
        System.out.println("str1 compareToIgnoreCase str2: " + str1.compareToIgnoreCase(str2)); // 0
        System.out.println("str1 starts with 'Hello': " + str1.startsWith("Hello")); // true
        System.out.println("str1 ends with 'Java!': " + str1.endsWith("Java!")); // true
    }
```
- equals(Object anObject) : 두 문자열이 동일한지 확인합니다.
- equalsIgnoreCase(String anotherString) : 두 문자열을 대소문자 구분 없이 비교합니다.
- compareTo(String anotherString) : 두 문자열을 사전 순으로 비교합니다.
- compateToIgnoreCase(String str) : 두 문자열을 대소문자 구분 없이 사전적으로 비교합니다.
- startWith(String prefix) : 문자열이 특정 접두사로 시작하는지 확인합니다.
- endsWith(String suffix) : 문자열이 특정 접미사로 끝나는지 확인합니다.

String의 메서드 - 문자열 검색
------------------------------------------------------------
```java
public class Main {
    public static void main(String[] args) {
        String str = "Hello, Java! Welcome to Java world.";
        System.out.println("문자열에 'Java'가 포함되어 있는지: " + str.contains("Java")); // true
        System.out.println("'Java'의 첫 번째 인덱스: " + str.indexOf("Java")); // 7
        System.out.println("인덱스 10부터 'Java'의 인덱스: " + str.indexOf("Java", 10)); // 24
        System.out.println("'Java'의 마지막 인덱스: " + str.lastIndexOf("Java")); // 24
    }
}
```
- contains(CharSequence s) : 문자열이 특정 문자열을 포함하고 있는지 확인합니다.
- indexOf(String ch) / indexOf(String ch, int fromIndex) : 문자열이 처음 등장하는 위치를 반환합니다.
- lastIndexOf(String ch) : 문자열이 마지막으로 등장하는 위치를 반환합니다.

String의 메서드 - 문자열 조작 및 변환
----------------------------------------------------
```java
public class Main {
    public static void main(String[] args) {
        String str = "Hello, Java! Welcome to Java";
        System.out.println("인덱스 7부터의 부분 문자열: " + str.substring(7)); // Java! Welcome to Java
        System.out.println("인덱스 7부터 12까지의 부분 문자열: " + str.substring(7, 12)); // Java!
        System.out.println("문자열 결합: " + str.concat("!!!")); // Hello, Java! Welcome to Java!!!
        System.out.println("'Java'를 'World'로 대체: " + str.replace("Java", "World")); // Hello, World! Welcome to World
        System.out.println("첫 번째 'Java'를 'World'으로 대체: " + str.replaceFirst("Java", "World")); // Hello, World! Welcome to Java
        
        String strWithSpaces = " Java Programming ";
        System.out.println("소문자로 변환: " + strWithSpaces.toLowerCase()); // java programming
        System.out.println("대문자로 변환: " + strWithSpaces.toUpperCase()); // JAVA PROGRAMMING
        System.out.println("공백 제거(trim): '" + strWithSpaces.trim() + "'"); // 'Java Programming'
        System.out.println("공백 제거(strip): '" + strWithSpaces.strip() + "'"); // 'Java Programming'
        System.out.println("앞 공백 제거(strip): '" + strWithSpaces.stripLeading() + "'"); // 'Java Programming '
        System.out.println("뒤 공백 제거(strip): '" + strWithSpaces.stripTrailing() + "'"); // ' Java Programming'
    }
```

- substring(int beginIndex) / substring(int beginIndex, int endIndex) : 문자열의 부분 문자열을 반환합니다.
- concat(String str) : 문자열 끝에 다른 문자열을 붙입니다.
- replace(CharSequence target, Charsequence replacement) : 특정 문자열을 새 문자열로 대체합니다.
- replaceAll(String regex, String replacement) : 문자열에서 정규 표현식과 일치하는 부분을 새 문자열로 대체합니다.
- replaceFirst(String regex, String replacement) : 문자열에서 정규 표현식과 일치하는 첫 번째 부분을 새 문자열로 대체합니다.
- toLowerCase() / toUpperCase() : 문자열을 소문자나 대문자로 변환합니다.
- trim() : 문자열의 양쪽 끝의 공백을 제거합니다. 단순한 Whitespace만 제거할 수 있습니다.
- strip() : Whitespace와 유니코드 공백을 포함해서 제거합니다. ( 자바 11부터 도입되었습니다. )

String의 메서드 - 문자열 분할 및 조합
------------------------------------------
```java
public class Main {
    public static void main(String[] args) {
        String str = "Apple,Banana,Orange";
        
        String[] splitStr = str.split(",");
        
        for(String s : splitStr) {
            System.out.println(s); // Apple Banana Orange
        }
        // join()
        String joinedStr = String.join("-", "A", "B", "C");
        System.out.println("연결된 문자열: " + joinedStr); // A-B-C
        // 문자열 배열 연결
        String result = String.join("-", splitStr);
        System.out.println("result = " + result); // Apple-Banana-Orange
    }
}
```
- split(String regex) : 문자열을 정규표현식을 기준으로 분할합니다.
- join(charSequence delimiter, CharSequence... elements) : 주어진 구분자로 여러 문자열을 결합합니다.

String의 메서드 - 기타 유틸리티
---------------------------------------------------
```java
public class Main {
    public static void main(String[] args) {
        int num = 100;
        boolean bool = true;
        Object obj = new Object();
        String str = "Hello, Java!";
        // valueOf 메서드
        String numString = String.valueOf(num);
        System.out.println("숫자의 문자열 값: " + numString); // 100
        String boolString = String.valueOf(bool);
        System.out.println("불리언의 문자열 값: " + boolString); // true
        String objString = String.valueOf(obj);
        System.out.println("객체의 문자열 값: " + objString); // java.lang.Object@a09ee92
        //다음과 같이 간단히 변환할 수 있음 (문자 + x -> 문자x)
        String numString2 = "" + num;
        System.out.println("빈문자열 + num:" + numString2); // 100
        // toCharArray 메서드
        char[] strCharArray = str.toCharArray(); 
        System.out.println("문자열을 문자 배열로 변환: " + strCharArray); // [C@30f39991
        for (char c : strCharArray) { 
            System.out.print(c); // Hello, Java!
        }
        System.out.println();
    }
}
```

```java
public static void main(String[] args) {
  int num = 100;
  boolean bool = true;
  String str = "Hello, Java!";
  // format 메서드
  String format1 = String.format("num: %d, bool: %b, str: %s", num, bool, str); // num: 100, bool: true, str: Hello,Java!
  System.out.println(format1);
  String format2 = String.format("숫자: %.2f", 10.1234); // 10.12
  System.out.println(format2);
  // printf
  System.out.printf("숫자: %.2f\n", 10.1234); // 10.12
  // matches 메서드
  String regex = "Hello, (Java!|World!)";
  System.out.println("'str'이 패턴과 일치하는가? " + str.matches(regex)); // true
}
```

- valueOf(Object obj) : 다양한 타입을 문자열로 변환합니다.
- tocharArray() : 문자열을 문자 배열로 변환합니다.
- format(String format, Object... args) : 형식 문자열과 인자를 사용해서 새로운 문자열을 생성합니다.
- matches(String regex) : 문자열이 주어진 정규표현식과 일치하는지를 확인합니다.

String 클래스가 갖는 불변성의 단점
---------------------------------------------------
- 연산 과정에서 String 객체가 계속 생성되면, 결국 최종 문자열 객체를 제외한 나머지 객체들은 불필요한 시스템 자원을 소모하게 됩니다.

StringBuilder 클래스
---------------------------------------------------
- String의 불변성이 갖는 단점들을 극복하기 위한, 가변의 String이라고 보면 됩니다. 내부의 값을 바로 변경할 수 있어서 새로운 객체를 생성할 필요가 없습니다.
- 물론, 그에 따른 사이드이펙트는 주의해서 사용해야 합니다. 보통 문자열을 변경하는 동안은 StringBuilder로 유연성을, 변경이 끝나면 String으로 안정성을 챙깁니다.

StringBuilder 클래스의 구조
--------------------------------------------------
```java
public final class StringBuilder {
  char[] value;// 자바 9 이전
  byte[] value;// 자바 9 이후
  //여러 메서드
  public StringBuilder append(String str) {...}
  public int length() {...}
  ...
}
```

StringBuilder 클래스의 사용 예시
----------------------------------------------------
```java
public class StringBuilderMain1_1 {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder();
        sb.append("A"); 
        sb.append("B");
        sb.append("C");
        sb.append("D");
        System.out.println("sb = " + sb);
        sb.insert(4, "Java");
        System.out.println("insert = " + sb);
        sb.delete(4, 8);
        System.out.println("delete = " + sb);
        sb.reverse();
        System.out.println("reverse = " + sb);
        //StringBuilder -> String
        String string = sb.toString();
        System.out.println("string = " + string);
    }
}
```
- append() : 여러 문자열을 추가합니다.
- insert() : 특정 위치에 문자열을 삽입합니다.
- delete() : 특정 범위의 문자열을 삭제합니다.
- reverse() : 문자열을 뒤집습니다.
- toString() : StringBuilder의 결과를 기반으로 String을 생성해서 반환합니다.

String 최적화 - 문자열 리터럴 최적화
------------------------------------------------------------------
```java
String helloWorld = "Hello, " + "World!"; // 컴파일 전
String helloWorld = "Hello, World!"; // 컴파일 후
```
- 자바 컴파일러는 런타임에 별도의 문자열 결합 연산을 수행하지 않고, 컴파일시에 미리 결합하기 때문에 성능이 향상됩니다.

String 최적화 - String 변수 최적화
------------------------------------------------------------------
```java
String result = str1 + str2;
String result = new StringBuilder.append(str1).append(str2).toString();
```
- 문자열 변수는 컴파일 시점에 내부 값을 알 수 없기 때문에 단순히 결합할 수 없습니다.
- 그럴 때는 위와 같은 방식으로 최적화를 수행합니다. ( 물론, 이러한 최적화 방식은 자바 버전에 따라 달라집니다. ) ( 참고로, 자바 9부터는 StringConcatFactory 라는 것을 통해 최적화합니다. )

String 최적화가 어려운 경우 - 문자열을 루프 내에서 더하는 경우
-----------------------------------------------------------------
```java
  String result = "";
  for (int i = 0; i < 100000; i++) {
    result += "Hello Java ";
  }
```

- 위와 같은 경우 실제로는 new StringBuilder().append(result).append("Hello Java").toString()과 같은 방식으로 최적화가 됩니다.
- 이렇게 되면 반복 횟수만큼 객체를 생성해야 하기 때문에, 최적화가 어렵습니다.

![image](https://github.com/user-attachments/assets/1c5ef4fe-bdec-4c44-95f9-ac3746016452)
- 단순히 + 연산으로 결합하는 경우 100000건의 데이터를 더하는데 2.5초가 걸립니다.

```java
  StringBuilder sb = new StringBuilder();
  for (int i = 0; i < 100000; i++) {
    sb.append("Hello Java ");
  }
```
- 이럴 때는 StringBuilder를 사용하면 시간을 최적화 할 수 있습니다.

![image](https://github.com/user-attachments/assets/1408c138-241b-4210-9ead-10cf18b1bec0)
- StringBuilder를 사용했을 때 0.003초가 걸립니다.

StringBuilder 사용이 더 좋은 경우
------------------------------------------------
- 반복문에서 반복해서 문자를 연결할 때 더 좋습니다.
- 조건을 통해 동적으로 문자열을 조합할 때 더 좋습니다.
- 복잡한 문자열의 특정 부분을 변경해야 할 때 더 좋습니다.
- 매우 긴 대용량의 문자열을 다룰 때 더 좋습니다.

StringBuilder vs StringBuffer
-----------------------------------------------------
- StringBuffer는 StringBuilder와 기능은 동일합니다.
- 멀티스레드 안정성 : StringBuffer는 내부 동기화가 되어 있어서 멀티스레드 상황에 안전하지만, 동기화 오베헤드로 인해 성능이 느립니다. 
- 동기화 오버헤드 : StringBuilder는 동기화 오버헤드가 없기 때문에 속도가 더 빠르지만, 멀티 쓰레드 안정성은 없습니다.

메서드 체이닝(Method Chaining)
----------------------------------------------------
- 메서드 호출의 결과로 자기 자신의 참조값을 반환할 경우, 반환된 참조값을 이용해서 메서드 호출을 계속 이어갈 수 있습니다.
- 코드에서 보면 .을 통해 메서드가 체인처럼 연결된 것처럼 보이는데 이런 기법을 메서드 체이닝이라고 합니다.
- 메서드 체이닝을 통해서 코드를 간결하고 읽기 쉽게 만들 수 있습니다.
  
```java
public class MethodChainingMain3 {
    public static void main(String[] args) {
        ValueAdder adder = new ValueAdder();
        int result = adder.add(1).add(2).add(3).getValue();
        System.out.println("result = " + result);
    }
}
```

StringBuilder의 메서드 체이닝
-----------------------------------------------------
StringBuilder에서 문자열을 변경하는 대부분의 메서드는 자기 자신을 반환합니다. ( insert, append, reverse, delete 등... ) -> 이를 통해 메서드 체이닝이 가능합니다.

```java
public static void main(String[] args) {
    StringBuilder sb = new StringBuilder();
    String string = sb.append("A").append("B").append("C").append("D")
            .insert(4, "Java")
            .delete(4, 8)
            .reverse()
            .toString();
    System.out.println("string = " + string);
}
```




