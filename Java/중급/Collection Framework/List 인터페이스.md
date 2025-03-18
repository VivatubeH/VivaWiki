List 인터페이스
------------------------------------------
순서가 있고 중복을 허용하는 자료구조를 List라고 하는데, 자바에서는 이를 List 인터페이스로 제공합니다.

구체적인 클래스에 의존할 때 가지게 되는 단점
------------------------------------------
```java
public class BatchProcessor {
  private final MyLinkedList<Integer> list = new MyLinkedList<>(); //코드 변경
  public void logic(int size) {
    for (int i = 0; i < size; i++) {
      list.add(0, i); //앞에 추가
    }
  }
}
```
- 위처럼 구체적인 의존 관계를 갖게 된다면, MyArrayList를 사용하고 싶다면 BatchProcessor라는 클라이언트의 코드를 변경해야만 합니다.

추상적인 인터페이스에 의존할 때 갖게 되는 장점
------------------------------------------------------
```java
public class BatchProcessor {
  private final MyList<Integer> list;
  public BatchProcessor(MyList<Integer> list) {
    this.list = list;
}
  public void logic(int size) {
    for (int i = 0; i < size; i++) {
      list.add(0, i); //앞에 추가
    }
  }
}

main() {
  new BatchProcessor(new MyArrayList()); //MyArrayList를 사용하고 싶을 때
  new BatchProcessor(new MyLinkedList()); //MyLinkedList를 사용하고 싶을 때
}
```
- 만약 위처럼 추상적인 의존 관계를 갖게된다면, 클라이언트인 BatchProcessor의 코드는 변경하지 않고 구체적인 클래스는 런타임에 지정할 수 있게 됩니다.

의존관계 주입(Dependency Injection, DI)
-------------------------------------------------
- 의존관계 주입은 의존성 주입이라고도 불립니다.
- 이는 위의 예시 코드처럼 외부에서 의존관계가 결정되어서 주입되는 것 같다고 해서 의존관계 주입이라고 불립니다.

컴파일 타임 의존관계와 런타임 의존관계
----------------------------------------------
- 컴파일 타임(compile time) : 코드 컴파일 시점을 뜻합니다.
- 런타임(runtime) : 프로그램 실행 시점을 뜻합니다.

- 컴파일 타임 의존관계 : 자바 컴파일러가 보는 의존관계를 말합니다. 즉, 실행하지 않은 소스 코드에 정적으로 나타나는 의존관계를 말합니다.
- 런타임 의존관계 : 실제 프로그램이 작동할 때 보이는 의존관계를 말합니다. 주로 생성된 인스턴스와 그 인스턴스를 참조하는 의존관계를 말합니다.

전략 패턴(Strategy Pattern)
---------------------------------------------
- 알고리즘을 클라이언트 코드의 변경 없이 쉽게 교체할 수 있는 패턴을 전략 패턴이라고 합니다.
- 예시 코드에서 MyList 인터페이스가 전략을 정의하는 인터페이스, 구현체인 MyArrayList와 MyLinkedList가 전략의 구체적인 구현이 됩니다.

List 인터페이스의 상속 구조
-------------------------------------------

![image](https://github.com/user-attachments/assets/917bfcec-1cbd-4b71-a746-58408a963882)

- Collection 인터페이스 : 컬렉션들의 상위 인터페이스입니다. 하위 인터페이스로 List, Set, Queue 와 같은 하위 인터페이스를 가지며 데이터 그룹을 다루는 메서드를 정의합니다.
- List 인터페이스 : 객체의 순서가 있고, 중복이 허용되는 자료구조를 다루는 컬렉션이며, 배열과 유사하지만 동적인 크기 변경이 가능합니다.
- ArrayList, LinkedList 클래스 : ArrayList, LinkedList 클래스들은 List 인터페이스의 구현 클래스이므로 List 인터페이스의 메서드를 구현합니다.

List 인터페이스의 주요 메서드들
----------------------------------------------
![image](https://github.com/user-attachments/assets/c3570c1f-2dd4-46f8-a3f7-bcaf7115ffa8)

자바의 ArrayList - 메모리 고속 복사 연산의 사용
----------------------------------------------

![image](https://github.com/user-attachments/assets/1186a6c2-3d9c-47c5-ae2c-66cde80b94b4)

- 원래의 ArrayList라면 데이터를 루프를 돌면서 하나씩 이동해야 하기 때문에, 속도가 매우 느립니다.

![image](https://github.com/user-attachments/assets/b84081e0-b6c7-4fd2-9e87-c548152044c5)

- 그러나 자바가 제공하는 ArrayList에서는 메모리 고속 복사 연산을 사용해서, 배열을 한 번에 아주 빠르게 복사합니다. ( 이는 한 칸씩 이동하는 방식보다 수 배 이상 빠릅니다. )

자바의 LinkedList - 이중 연결 리스트의 사용
---------------------------------------------

![image](https://github.com/user-attachments/assets/b97ce39b-2706-4162-af9e-d956ab16dfde)

- 원래의 LinkedList라면 다음 노드로만 이동할 수 있는 단일 연결 구조입니다. ( 즉, 이전 노드로의 이동이 불가능합니다. )

![image](https://github.com/user-attachments/assets/3a67a546-28d6-4505-b102-8e227f66a0b0)

- 자바가 제공하는 LinkedList는 단일이 아닌 이중 연결 구조를 갖습니다.
- 이는 시작 노드 뿐만 아니라 끝 노드에 대한 참조도 제공할 뿐더러, 노드들은 다음 노드 뿐만 아니라 이전 노드로도 이동할 수 있습니다.
- 이러한 이중 연결 리스트를 통해 인덱스 조회 시 사이즈를 토대로 순회 방향을 최적화할 수 있고, 마지막에 데이터를 추가할 때 O(1)으로 성능이 비약적으로 향상됩니다.

자바의 ArrayList와 LinkedList의 이론적인 시간 복잡도
--------------------------------------
![image](https://github.com/user-attachments/assets/03d97680-a3ef-4d7a-a946-8c4eb96832f1)

실제 컴퓨터에서의 성능을 기반으로 한 ArrayList vs LinkedList
---------------------------------------------------------------------
- LinkedList는 각 요소가 별도의 객체로 존재하고 다음 요소의 참조를 저장하는 방식이라 CPU 캐시 효율성이 떨어지고 메모리 접근 속도가 상대적으로 느려질 수 있습니다.
- ArrayList는 요소들이 메모리상에서 연속적으로 위치하기 때문에 CPU 캐시 효율성이 좋고, 메모리 접근 속도가 상대적으로 빠릅니다.
- 그렇기 때문에 현대 컴퓨터 시스템의 메모리 접근 패턴, CPU 캐시 최적화, 메모리 고속 복사 등을 고려하면 ArrayList가 실제 사용 환경에서 더 나은 성능을 보여주는 경우가 많습니다.

ArrayList와 LinkedList를 사용하는 경우 정리
---------------------------------------------------
- 대부분의 실무 : ArrayList 사용이 권장됩니다.
- 데이터를 앞쪽에서 자주 추가하거나 삭제할 때 : LinkedList 사용이 권장됩니다.
