#### final 지역변수
- final이 붙은 지역변수는 최초 한 번만 값 할당이 가능합니다. -> 이후 변경시 컴파일 오류가 발생합니다.
- final이 붙은 매개변수는 호출 시점에 값이 할당되기 때문에 이후 변경할 수 없습니다.

#### final 멤버변수
- final 변수는 필드에서 초기화하게 되면, 이미 값이 설정되었기 때문에 생성자를 통한 초기화가 불가능합니다.
- static 변수에도 final을 선언할 수 있습니다.

#### static final
- final : 한 번 정해진 값이 더 이상 값이 변하지 않습니다.
- static : JVM 내에서 하나만 존재합니다.

#### Constant(상수)
- 상수는 보통 단 하나만 존재하고 변하지 않는 값을 말합니다.
- 그래서 자바에서는 static final을 상수에 붙입니다.
- 단, 구분을 위해 변수명은 대문자를 사용하고 언더스코어(_)로 구분합니다.
- 그리고, 값 변경이 불가능하기 때문에 접근 제한을 할 필요는 없습니다.

```java
//수학 상수
public static final double PI = 3.14;
//시간 상수
public static final int HOURS_IN_DAY = 24;
public static final int MINUTES_IN_HOUR = 60;
public static final int SECONDS_IN_MINUTE = 60;
//애플리케이션 설정 상수
public static final int MAX_USERS = 1000;
```

#### final을 참조변수에 사용할 때
- 이런 경우라면, 참조값을 변경할 수 없습니다. ( 즉, 원래 가리키던 변수를 가리켜야 합니다. )
- 그러나, 참조하는 변수의 값은 얼마든지 변경가능합니다.
