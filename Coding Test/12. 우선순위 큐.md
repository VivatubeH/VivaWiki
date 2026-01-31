# 우선순위 큐 (PriorityQueue)

## 핵심 개념
- **힙(Heap) 기반 자료구조**: 최소값 또는 최대값을 빠르게 꺼낼 수 있는 큐
- **언제 사용?**: 최소/최대값 빠르게 찾기, 다익스트라, 작업 스케줄링, K번째 큰/작은 수
- **시간복잡도**: 삽입 O(log n), 삭제 O(log n), 조회(peek) O(1)

## Java에서 PriorityQueue 사용법

### 1. 기본 선언 및 주요 메서드
```java
import java.util.*;

// 기본: 최소 힙 (작은 값이 우선순위 높음)
PriorityQueue<Integer> minHeap = new PriorityQueue<>();

// 주요 메서드
minHeap.offer(10);    // 삽입 O(log n)
minHeap.add(20);      // 삽입 (offer 권장)
minHeap.poll();       // 최소값 제거 후 반환 O(log n)
minHeap.peek();       // 최소값 조회만 (제거X) O(1)
minHeap.isEmpty();    // 비어있는지 확인
minHeap.size();       // 크기 반환
```

### 2. 최소 힙 (기본)
```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();

minHeap.offer(5);
minHeap.offer(2);
minHeap.offer(8);
minHeap.offer(1);

System.out.println(minHeap.poll());  // 1
System.out.println(minHeap.poll());  // 2
System.out.println(minHeap.poll());  // 5
System.out.println(minHeap.poll());  // 8
```

### 3. 최대 힙
```java
// Collections.reverseOrder() 사용
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

maxHeap.offer(5);
maxHeap.offer(2);
maxHeap.offer(8);
maxHeap.offer(1);

System.out.println(maxHeap.poll());  // 8
System.out.println(maxHeap.poll());  // 5
System.out.println(maxHeap.poll());  // 2
System.out.println(maxHeap.poll());  // 1
```

## 커스텀 우선순위 설정

### 1. 절댓값 기준 (백준 11286)
```java
// 절댓값이 작은 순, 같으면 실제 값이 작은 순
PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> {
    if (Math.abs(a) == Math.abs(b)) {
        return a - b;  // 실제 값 비교 (오름차순)
    }
    return Math.abs(a) - Math.abs(b);  // 절댓값 비교
});

pq.offer(-3);
pq.offer(3);
pq.offer(-1);
pq.offer(5);

System.out.println(pq.poll());  // -1 (절댓값 1이 최소)
System.out.println(pq.poll());  // -3 (절댓값 3, 음수가 먼저)
System.out.println(pq.poll());  // 3
```

### 2. 객체 비교 (실전 예제)
```java
class Task {
    int priority;  // 우선순위 (낮을수록 먼저)
    String name;
    
    Task(int priority, String name) {
        this.priority = priority;
        this.name = name;
    }
}

// 우선순위가 낮은 숫자가 먼저 처리
PriorityQueue<Task> pq = new PriorityQueue<>((a, b) -> a.priority - b.priority);

pq.offer(new Task(3, "작업C"));
pq.offer(new Task(1, "작업A"));
pq.offer(new Task(2, "작업B"));

System.out.println(pq.poll().name);  // 작업A (우선순위 1)
System.out.println(pq.poll().name);  // 작업B (우선순위 2)
```

### 3. 다중 조건 정렬
```java
class Student {
    String name;
    int score;
    int age;
    
    Student(String name, int score, int age) {
        this.name = name;
        this.score = score;
        this.age = age;
    }
}

// 점수 높은 순 → 같으면 나이 어린 순
PriorityQueue<Student> pq = new PriorityQueue<>((a, b) -> {
    if (a.score == b.score) {
        return a.age - b.age;  // 나이 오름차순
    }
    return b.score - a.score;  // 점수 내림차순
});

pq.offer(new Student("철수", 90, 20));
pq.offer(new Student("영희", 90, 18));
pq.offer(new Student("민수", 85, 19));

Student top = pq.poll();  // 영희 (점수 90, 나이 18)
```

## 실전 코드 템플릿

### 1. 최소/최대값 K개 찾기
```java
// 배열에서 K번째 큰 수 찾기
public int findKthLargest(int[] nums, int k) {
    // 최소 힙으로 K개만 유지
    PriorityQueue<Integer> pq = new PriorityQueue<>();
    
    for (int num : nums) {
        pq.offer(num);
        if (pq.size() > k) {
            pq.poll();  // 작은 값 제거
        }
    }
    
    return pq.peek();  // K번째 큰 값
}
```

### 2. 다익스트라 알고리즘
```java
// 최단 경로 찾기
class Node {
    int vertex;
    int cost;
    
    Node(int vertex, int cost) {
        this.vertex = vertex;
        this.cost = cost;
    }
}

public void dijkstra(int start, List<List<Node>> graph, int n) {
    PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> a.cost - b.cost);
    int[] dist = new int[n + 1];
    Arrays.fill(dist, Integer.MAX_VALUE);
    
    pq.offer(new Node(start, 0));
    dist[start] = 0;
    
    while (!pq.isEmpty()) {
        Node current = pq.poll();
        
        if (current.cost > dist[current.vertex]) continue;
        
        for (Node next : graph.get(current.vertex)) {
            int newCost = dist[current.vertex] + next.cost;
            if (newCost < dist[next.vertex]) {
                dist[next.vertex] = newCost;
                pq.offer(new Node(next.vertex, newCost));
            }
        }
    }
}
```

## 실수하기 쉬운 포인트

### 1. Comparator 부호 주의
```java
// ❌ 최대 힙 만들려다 잘못된 경우
PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> a - b);
// 이건 최소 힙! (기본과 동일)

// ✅ 최대 힙
PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> b - a);
// 또는
PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
```

### 2. poll() 전 isEmpty() 체크
```java
// ❌ 빈 힙에서 poll() → null 반환
int x = pq.poll();  // NullPointerException 가능

// ✅ 체크 필수
if (!pq.isEmpty()) {
    int x = pq.poll();
}
```

### 3. 힙은 완전 정렬이 아님
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(3);
pq.offer(1);
pq.offer(2);

System.out.println(pq);  // [1, 3, 2] ← 완전 정렬 아님!
// 힙 구조: 부모 ≤ 자식만 보장
// poll()로 꺼낼 때만 1 → 2 → 3 순서
```

### 4. 객체 비교 시 null 주의
```java
class Data {
    Integer value;
}

// ❌ null 값이 있으면 NullPointerException
PriorityQueue<Data> pq = new PriorityQueue<>((a, b) -> a.value - b.value);

// ✅ null 체크
PriorityQueue<Data> pq = new PriorityQueue<>((a, b) -> {
    if (a.value == null) return 1;
    if (b.value == null) return -1;
    return a.value - b.value;
});
```

## 디버깅 팁

### 1. 현재 힙 상태 확인
```java
// 힙 내부 확인 (디버깅용)
System.out.println(pq);  // [1, 3, 2] (힙 구조)

// 실제 정렬된 순서 확인
while (!pq.isEmpty()) {
    System.out.print(pq.poll() + " ");  // 1 2 3
}
```

### 2. Comparator 동작 확인
```java
PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> {
    System.out.println("비교: " + a + " vs " + b);
    return a - b;
});

pq.offer(5);
pq.offer(2);
pq.offer(8);
// 비교 로그로 우선순위 확인 가능
```

## 면접 대비 핵심

**Q1. PriorityQueue의 내부 구조는?**
- 이진 힙(Binary Heap)으로 구현됨
- 완전 이진 트리 구조를 배열로 표현
- 부모 노드 인덱스 i → 왼쪽 자식 2i+1, 오른쪽 자식 2i+2

**Q2. 왜 삽입/삭제가 O(log n)인가?**
- 힙의 높이가 log n
- 삽입: 맨 끝에 추가 후 부모와 비교하며 위로 이동 (최대 log n번)
- 삭제: 루트 제거 후 맨 끝 노드를 루트로, 자식과 비교하며 아래로 이동 (최대 log n번)

**Q3. 언제 PriorityQueue를 쓰나?**
- 항상 최소/최대값이 필요할 때
- 다익스트라, 프림 알고리즘 (그래프)
- K번째 큰/작은 수 찾기
- 중앙값 구하기 (두 개 힙 사용)

**Q4. Collections.reverseOrder()는 어떻게 동작?**
- 기본 Comparator를 반대로 뒤집은 Comparator 반환
- a.compareTo(b)를 b.compareTo(a)로 변경

**Q5. PriorityQueue vs TreeSet 차이는?**
- PriorityQueue: 최소/최대값만 빠르게, 중복 허용, 부분 정렬
- TreeSet: 전체 정렬 유지, 중복 불허, 범위 검색 가능

**Q6. Comparator에서 오버플로우 주의사항은?**
```java
// ❌ a - b는 오버플로우 위험
(a, b) -> a - b

// ✅ Integer.compare 사용
(a, b) -> Integer.compare(a, b)
```
