큐(Queue) 자료구조
-------------------------------------
- 아래 그림과 같이, 스택과 달리 양쪽이 뚫려있어서 가장 먼저 넣은 것이 가장 먼저 나올 수 있는 자료구조를 큐(Queue)라고 합니다.

![image](https://github.com/user-attachments/assets/4ff0a177-a0c0-4ffc-a590-b1412eb17fa1)

- 전통적으로 큐에 값을 넣는 것을 offer(), 큐에서 값을 꺼내는 것을 poll이라고 합니다.

Queue 자료구조의 계층구조
--------------------------------------
![image](https://github.com/user-attachments/assets/207fb725-ff97-462e-baba-65890941fb39)

- Queue 인터페이스도 List, Set처럼 Collection의 자식입니다.
- Queue를 구현한 대표적인 구현체로는 ArrayDeque, LinkedList가 있습니다. ( 참고로 LinkedLists는 Deque과 List 인터페이스를 모두 구현합니다. )

자바 코드로 보는 Queue
---------------------------------------
```java
package deque;
import java.util.*;

public class QueueMain {
    public static void main(String[] args) {
        Queue<Integer> queue = new ArrayDeque<>();

        // 큐에 데이터를 추가할 때는 offer()를 사용합니다.
        queue.offer(1);
        queue.offer(2);
        queue.offer(3);
        System.out.println(queue);

        // 다음에 꺼낼 데잍러를 확인할 때는 Stack과 마찬가지로 peek()으로 확인합니다.
        System.out.println(queue.peek());

        // Queue에서 데이터를 꺼낼 때는 poll()을 사용합니다.
        System.out.println("poll = " + queue.poll());
        System.out.println("poll = " + queue.poll());
        System.out.println("poll = " + queue.poll());
        System.out.println(queue);
    }
}
```
