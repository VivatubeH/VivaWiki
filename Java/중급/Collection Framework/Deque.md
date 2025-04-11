덱(Deque) 자료구조
----------------------------------------
- Deque는 Double Ended Queue라는 이름에서도 알 수 있듯이, 양쪽 끝에서 요소를 추가하거나 제거할 수 있는 자료구조입니다.
- Deque는 일반적인 큐(Queue)와 스택(Stack)의 기능을 모두 포함하고 있어서, 매우 유연한 자료구조입니다.
- 데크, 덱으로 불립니다.

덱(Deque)의 메서드
---------------------------------------
- 앞에 값을 추가할 때 : offerFirst()
- 뒤에 값을 추가할 때 : offerLast();
- 앞에서 값을 꺼낼 때 : pollFirst();
- 뒤에서 값을 꺼낼 때 : pollLast();

자바 코드로 보는 덱(Deque)
---------------------------------------
```java
package deque;
import java.util.*;

public class DequeMain {
    public static void main(String[] args) {
        Deque<Integer> deque = new ArrayDeque<>();

        // 데이터를 앞에 추가합니다.
        deque.offerFirst(1);
        System.out.println(deque);
        deque.offerFirst(2);
        System.out.println(deque);
        deque.offerLast(3);
        System.out.println(deque);
        deque.offerLast(4);
        System.out.println(deque);

        // 다음에 꺼낼 데이터를 단순히 조회만 하겠습니다.
        System.out.println("deque.peekFirst() = " + deque.peekFirst());
        System.out.println("deque.peekLast() = " + deque.peekLast());

        // 실제로 데이터를 꺼냅니다.
        System.out.println("pollFirst = " + deque.pollFirst());
        System.out.println("pollFirst = " + deque.pollFirst());
        System.out.println("pollLast = " + deque.pollLast());
        System.out.println("pollLast = " + deque.pollLast());
        System.out.println(deque);
    }
}
```

Deque 구현체와 성능 테스트
-----------------------------------------
- Deque의 대표적인 구현체인 ArrayDeque과 LinkedList 둘 중에서는 ArrayDeque이 모든 면에서 더 빠릅니다.

- 100만건 입력의 경우 (앞, 뒤 평균)
- ArrayDequqe : 110ms
- LinkedList : 480ms

- 100만건 조회의 경우(앞, 뒤 평균)
- ArrayDeque : 9ms
- LinkedList : 20ms

- 둘의 속도 차이는 ArrayList vs LinkedList와 비슷한데 이는 둘 중 하나는 배열을, 하나는 동적 노드 링크를 사용하기 때문입니다.
- 참고로 ArrayDeque은 특별한 원형 큐 자료구조를 사용하기 때문에 앞 뒤 입력 모두 O(1)의 성능을 제공합니다. ( LinkedList도 O(1)의 성능을 제공하긴 합니다. )
- 이론적으로는 LinkedList가 삽입 삭제가 자주 발생 시 더 효율적일 것처럼 보이지만, 현재 컴퓨터 시스템의 메모리 접근 패턴, CPU 캐시 최적화를 고려하면 ArrayDequqe이 더 나은 성능을 보여주는 경우가 많습니다.

Deque과 Stack, Queue의 관계
-------------------------------------------
- Deque을 통해 양쪽으로 데이터를 입력하고, 출력할 수 있기 때문에 스택과 큐의 역할을 모두 수행할 수 있습니다.
- 따라서 Deque을 Stack, Queue로 사용하기 위한 메서드 이름까지 제공합니다.
  
![image](https://github.com/user-attachments/assets/12147b51-0aff-4e58-9f7d-6f348e540795)

- Deque을 덱으로 사용할 때는 offerFirst(), offerLast(), pollFirst(), pollLast()를 사용합니다.
- Deque을 스택으로 사용할 때는 push(), pop()을 사용합니다. ( 앞에서 입력하고, 앞에서 꺼냅니다. )
- Dequqe을 큐로서 사용할 때는 offer(), poll()을 사용합니다. ( 뒤에서 입력하고, 앞에서 꺼냅니다. )

자바 코드로 보는 Deque - Stack
--------------------------------
```java
package deque;

import java.util.*;

public class DequeStackMain {
    public static void main(String[] args) {
        Deque<Integer> deque = new ArrayDeque<>();

        // 데이터 추가
        deque.push(1);
        deque.push(2);
        deque.push(3);
        System.out.println(deque);

        // 다음 꺼낼 데이터를 확인하기 ( 단순히 조회만 )
        System.out.println("deque.peek() = " + deque.peek());

        // 데이터를 꺼냅니다.
        System.out.println("pop = " + deque.pop());
        System.out.println("pop = " + deque.pop());
        System.out.println("pop = " + deque.pop());
        System.out.println(deque);
    }
}

```
