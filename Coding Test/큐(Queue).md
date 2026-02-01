# 큐 (Queue)

## 핵심 개념
- **FIFO (First In First Out)**: 먼저 들어온 데이터가 먼저 나가는 선형 자료구조
- **언제 사용?**: BFS, 작업 스케줄링, 프린터 대기열, 레벨 순회 등
- **시간복잡도**: 삽입/삭제 O(1), 탐색 O(n)

## Java에서 Queue 사용법

### 1. 기본 선언 및 주요 메서드
```java
import java.util.*;

// Queue는 인터페이스 → LinkedList로 구현
Queue<Integer> queue = new LinkedList<>();

// 주요 메서드
queue.offer(10);    // 삽입 (추가 성공 true, 실패 false 반환)
queue.add(20);      // 삽입 (실패 시 예외 발생)
queue.poll();       // 제거 후 반환 (비어있으면 null)
queue.remove();     // 제거 후 반환 (비어있으면 예외)
queue.peek();       // 맨 앞 요소 조회 (제거X, 비어있으면 null)
queue.isEmpty();    // 비어있는지 확인
queue.size();       // 크기 반환
```

### 2. 실전 코드 템플릿
```java
import java.util.*;

public class QueueTemplate {
    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();
        
        // 삽입
        queue.offer(1);
        queue.offer(2);
        queue.offer(3);
        
        // 순회 (Queue는 for-each 가능하지만 순서 보장 안 됨)
        // 실전에서는 poll()로 하나씩 꺼내며 처리
        while (!queue.isEmpty()) {
            int current = queue.poll();  // 맨 앞 제거하며 가져옴
            System.out.println(current); // 1 → 2 → 3
        }
    }
}
```

## 주요 변형 패턴

### 1. Deque (양방향 큐)
```java
// 양쪽에서 삽입/삭제 가능
Deque<Integer> deque = new ArrayDeque<>();

deque.offerFirst(1);  // 앞에 삽입
deque.offerLast(2);   // 뒤에 삽입
deque.pollFirst();    // 앞에서 제거
deque.pollLast();     // 뒤에서 제거
```

### 2. 우선순위 큐
```java
// 힙 기반, 최소값이 먼저 나옴
PriorityQueue<Integer> pq = new PriorityQueue<>();

pq.offer(5);
pq.offer(2);
pq.offer(8);
pq.poll();  // 2가 먼저 나옴 (최소값)
```

## 실수하기 쉬운 포인트

### 1. add vs offer
```java
// ❌ add(): 실패 시 예외 발생
queue.add(x);  // IllegalStateException 가능

// ✅ offer(): 실패 시 false 반환 (권장)
if (queue.offer(x)) {
    // 성공
}
```

### 2. poll vs remove
```java
// ❌ remove(): 빈 큐에서 호출 시 예외
int x = queue.remove();  // NoSuchElementException

// ✅ poll(): 빈 큐에서 null 반환
Integer x = queue.poll();
if (x != null) {
    // 처리
}
```

### 3. 순회 시 poll 사용
```java
// ❌ for-each는 내부 순서 보장 안 됨
for (int x : queue) {  
    // 예측 불가능한 순서
}

// ✅ poll()로 하나씩 꺼내기
while (!queue.isEmpty()) {
    int x = queue.poll();  // FIFO 보장
}
```

## 디버깅 팁

### 1. Queue 상태 확인
```java
// 현재 큐 내용 확인 (디버깅용)
System.out.println(queue);  // [1, 2, 3]

// 맨 앞 요소만 확인 (제거 안 함)
System.out.println(queue.peek());
```

### 2. 무한 루프 주의
```java
// ❌ poll() 없이 순회하면 무한 루프
while (!queue.isEmpty()) {
    int x = queue.peek();  // 제거 안 함 → 무한 반복
}

// ✅ 반드시 poll()로 제거
while (!queue.isEmpty()) {
    int x = queue.poll();  // 제거하며 진행
}
```

## 면접 대비 핵심

**Q1. Queue와 Stack의 차이는?**
- Queue: FIFO (먼저 들어온 것이 먼저 나감) → BFS, 작업 스케줄링
- Stack: LIFO (나중에 들어온 것이 먼저 나감) → DFS, 괄호 검사

**Q2. LinkedList vs ArrayDeque 선택 기준은?**
- LinkedList: 메모리 오버헤드 있음 (노드 구조)
- ArrayDeque: 배열 기반, 더 빠름, 메모리 효율적 (Queue/Deque로 사용 시 권장)

**Q3. BFS에서 Queue를 왜 사용하나?**
- 현재 레벨의 모든 노드를 먼저 탐색한 후 다음 레벨로 이동
- FIFO 특성이 레벨 순서 탐색과 일치

**Q4. offer와 add의 차이는?**
- offer: 용량 제한 큐에서 실패 시 false 반환 (예외 없음)
- add: 실패 시 IllegalStateException 발생
- 실전에서는 offer 권장 (안전)

**Q5. Queue는 왜 인터페이스로 선언하나?**
- 구현체 교체 유연성 (LinkedList ↔ ArrayDeque)
- 다형성 활용 (Queue 인터페이스 메서드만 사용)
