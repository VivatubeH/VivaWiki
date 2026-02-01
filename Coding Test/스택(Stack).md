# 스택 (Stack)

## 핵심 개념
후입선출(LIFO) 구조로, 마지막에 들어온 원소가 먼저 나온다.
현재 진행 중인 작업을 잠시 멈추고 새로운 작업을 처리한 후 다시 돌아오는 상황에 쓰는 자료구조이다.
코딩테스트에서 **괄호 검증, 수식 계산, 단조스택** 유형의 핵심 수단이다.

## 표준 코드 템플릿
```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        // ① 스택 선언 (Deque를 스택으로 사용 — Stack 클래스는 금지)
        Deque<Integer> stack = new ArrayDeque<>();

        // ② push — 원소 추가 (스택 = addFirst / push)
        stack.push(10);   // [10]
        stack.push(20);   // [20, 10]  ← 앞이 top

        // ③ peek — top 원소 조회 (제거하지 않음)
        int top = stack.peek();  // 20

        // ④ pop — top 원소 제거 및 반환
        int val = stack.pop();   // 20, stack = [10]

        // ⑤ isEmpty 체크 — pop 전에 반드시 확인
        if (!stack.isEmpty()) {
            stack.pop();
        }

        // ⑥ size 확인
        int size = stack.size();
    }
}
```

## 시간 / 공간 복잡도
| 연산 | 시간복잡도 |
|------|-----------|
| push | O(1) |
| pop | O(1) |
| peek | O(1) |
| 공간 | O(N) — 최대 원소 수 |

## 주요 변형 패턴

### 패턴 1 — 괄호 검증
조건: 열린 괄호는 push, 닫힌 괄호가 오면 top과 매칭 검증
```java
// 핵심 로직만
Deque<Character> stack = new ArrayDeque<>();
for (char c : s.toCharArray()) {
    if (c == '(' || c == '[' || c == '{') {
        stack.push(c);                        // 열린 괄호 → push
    } else {
        if (stack.isEmpty()) return false;    // 닫힌 괄호인데 스택 빈 경우 → 불균형
        char top = stack.pop();
        if (!isMatch(top, c)) return false;   // 매칭 실패 시 불균형
    }
}
return stack.isEmpty();                       // 남은 열린 괄호가 없어야 균형
```

### 패턴 2 — 단조스택 (Monotonic Stack)
조건: 스택 내 원소를 항상 단조증가 또는 단조감소로 유지.
**"오른쪽(또는 왼쪽)에서 처음 작은(또는 큰) 원소"** 를 찾는 유형에서 사용.
시간복잡도가 O(N)으로 brute-force O(N²)보다 압도적으로 빠름.
```java
// 패턴: 각 원소의 "오른쪽 첫 번째로 작은 값" 찾기
// stack에 인덱스를 저장하며, 단조증가 유지
Deque<Integer> stack = new ArrayDeque<>();   // 인덱스 저장
int[] result = new int[arr.length];
Arrays.fill(result, -1);                     // 기본값 -1 (작은 값 없음)

for (int i = 0; i < arr.length; i++) {
    // 현재 값이 스택 top의 값보다 작으면 → top의 "오른쪽 첫 작은 값" = 현재
    while (!stack.isEmpty() && arr[stack.peek()] > arr[i]) {
        result[stack.pop()] = arr[i];        // pop된 인덱스의 답 확정
    }
    stack.push(i);                           // 현재 인덱스를 스택에 추가
}
```

## 실수 포인트 & 디버깅 팁

**① Stack<Integer> 사용 금지**
`java.util.Stack`은 Vector 기반이어서 synchronized 오버헤드가 있다.
코딩테스트에서도 TLE 원인이 될 수 있으므로 반드시 `Deque<Integer> stack = new ArrayDeque<>()` 사용.

**② pop 전 isEmpty 체크 필수**
빈 스택에서 pop하면 NoSuchElementException이 발생한다.
괄호 검증처럼 닫힌 괄호가 먼저 오는 케이스를 놓치지 않도록 항상 체크.

**③ 단조스택에서 인덱스 저장 실수**
값 자체를 push하면 "어떤 위치의 원소인지" 추적이 불가능하다.
반드시 인덱스를 push하고, 값은 arr[stack.peek()]로 접근.

**④ 괄호 검증 마지막 체크 실수**
루프 끝에서 stack.isEmpty() 최종 확인을 빠뜨리면 "(((" 같은 열린 괄호만 남은 케이스를 통과시킬 수 있다.

## 면접 대비 핵심

**Q1. Stack 대신 Deque를 사용하는 이유?**
- Stack은 Vector를 상속받아 모든 연산이 synchronized이다. 단일 스레드 환경에서는 불필요한 lock 오버헤드가 발생하여 성능이 저하된다. Deque(ArrayDeque)는 이런 제약 없이 O(1)로 push/pop이 가능하므로 스택 구현의 표준 선택지이다.

**Q2. 단조스택이 O(N)인 이유?**
- 각 원소는 push와 pop을 각각 최대 1번씩 수행한다. 전체 루프가 N회라고 해도 while 안의 pop은 총 N번을 넘지 않아 전체 시간복잡도가 O(N)이다.

**Q3. 스택으로 수식 계산을 처리하는 흐름?**
- 피연산자는 스택에 push, 연산자는 우선순위를 비교하여 스택 top보다 낮은 연산자가 오면 먼저 계산 후 결과를 push한다. 이렇게 연산자 우선순위를 스택으로 관리하는 것이 수식 평가의 핵심 원리이다.
