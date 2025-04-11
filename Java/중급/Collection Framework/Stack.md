Stack(스택)
---------------------------------
- 스택은 아래 그림처럼 아래쪽은 막혀있고, 위쪽만 열려있는 자료구조를 말합니다.
- 그에 따라 필연적으로 후입선출(LIFO) 자료구조가 됩니다. ( 즉, 먼저 넣은 데이터는 밑에 깔리기 때문에 나중에 넣은 데이터가 나가야지만 나갈 수 있습니다. )
  
![image](https://github.com/user-attachments/assets/1b0557f5-4590-4319-abb4-1593d0d24c86)

후입선출(LIFO, Last In First Out)
----------------------------------------
- 가장 나중에 넣은 것이 가장 먼저 나오는 것을 후입선출이라고 합니다.
- 전통적으로 스택에 값을 넣는 것을 push, 스택에서 값을 꺼내는 것을 pop이라고 합니다.

자바 스택 예제 코드
---------------------------------------
```java
package stack;
import java.util.*;

public class StackMain {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();

        stack.push(1);
        stack.push(2);
        stack.push(3);
        System.out.println(stack);

        // 스택에서 다음에 꺼낼 요소를 단순히 조회만 할 때는 peek()를 사용합니다.
        System.out.println("stack.peek() = " + stack.peek());

        // 스택 요소를 뽑습니다.
        System.out.println("stack.pop() = " + stack.pop());
        System.out.println("stack.pop() = " + stack.pop());
        System.out.println("stack.pop() = " + stack.pop());
        System.out.println(stack);
    }
}
```

Stack 사용시 주의사항
-------------------------
- 자바의 Stack 클래스는 내부에서 Vector라는 자료 구조를 사용합니다.
- 해당 Vector 자료구조는 자바 1.0에 개발되었는데 지금은 사용되지 않고 하위 호환을 위해 존재합니다.
- 지금은 Stack 보다 더 빠른 자료구조가 많기 때문에 Vector를 사용하는 Stack도 사용하지 않는 것을 권장합니다.

