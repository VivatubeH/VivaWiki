```mathematica
Collection
├── List
│   ├── ArrayList
│   ├── LinkedList
│   └── Vector
├── Set
│   ├── HashSet
│   ├── LinkedHashSet
│   └── TreeSet
└── Queue
    ├── LinkedList
    ├── PriorityQueue
    └── ArrayDeque
```

- Collection 인터페이스 : 자바의 컬렉션 프레임워크의 가장 최상위 인터페이스입니다.
- Collection 인터페이스의 하위에 List 인터페이스, SET 인터페이스, Queue 인터페이스들이 존재합니다.

List와 Set의 직접적인 형변환은 불가능하다.
------------------------------------------------
- List<String>은 순서가 있는 컬렉션이므로 중복도 허용되고, 인덱스를 통한 접근도 가능합니다.
- Set<String>은 순서도 보장되지 않고, 중복도 허용되지 않는 컬렉션입니다.
- 이 둘은 저장방식 자체가 다르기 때문에 서로 직접적인 형변환이 불가능합니다.
- 사실 본질적으로는 List와 Set이 애초에 상속관계가 아니기 때문에 둘은 서로 변환할 수가 없습니다.

List<String>과 Set<String>을 그럼 어떻게 변환하는 걸까?
----------------------------------------------------------
```java
import java.util.*;

public class ListToSetConversion {
    public static void main(String[] args) {
        // List 생성
        List<String> list = new ArrayList<>(Arrays.asList("apple", "banana", "apple", "cherry"));

        // List를 Set으로 변환
        Set<String> set = new HashSet<>(list);

        // 변환된 Set 출력
        System.out.println(set); // 출력: [banana, apple, cherry]
    }
}
```
- List를 Set으로 변환할 때는 Set의 생성자를 통해서 명시적으로 변환할 수 있습니다.
- 이 때, Set은 중복을 허용하지 않아서 중복된 값인 apple이 제거되게 됩니다.

```java
import java.util.*;

public class SetToListConversion {
    public static void main(String[] args) {
        // Set 생성
        Set<String> set = new HashSet<>(Arrays.asList("apple", "banana", "cherry"));

        // Set을 List로 변환
        List<String> list = new ArrayList<>(set);

        // 변환된 List 출력
        System.out.println(list); // 출력: [banana, apple, cherry]
    }
}
```

각 생성자의 선언부 ( 본질적으로 변환이 가능한 이유 )
----------------------------------------------------
```java
public ArrayList(Collection<? extends E> c) { }
public HashSet(Collection<? extends E> c) { }
```
- Collection<? extends E>을 사용함으로써, Collection이라는 조상 타입에 List나 Set과 관련된 클래스를 저장할 수 있는 것입니다.
- 이는 다형성 때문에 가능합니다.
