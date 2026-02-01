# List 자료구조 (Array vs ArrayList vs LinkedList)

## 핵심 개념
리스트는 순서가 있는 데이터 집합. 배열(Array)은 크기 고정, 리스트(List)는 크기 동적 조절 가능.
코딩테스트에서는 ArrayList가 90% 이상 사용되며, 양방향 삽입/삭제가 필요할 때만 LinkedList 사용.

**시간복잡도 (핵심만 암기)**
- ArrayList 조회: O(1), 중간 삽입/삭제: O(n)
- LinkedList 조회: O(n), 양 끝 삽입/삭제: O(1)

---

## 표준 코드 템플릿

### 1. ArrayList 생성 및 기본 연산
```java
import java.util.*;

// 생성
List<Integer> list = new ArrayList<>();

// 추가
list.add(10);              // 끝에 추가 O(1)
list.add(0, 5);           // 인덱스 0에 삽입 O(n) - 뒤 요소들 shift

// 조회
int value = list.get(0);   // 인덱스 접근 O(1)
int size = list.size();    // 크기 O(1)

// 삭제
list.remove(0);            // 인덱스로 삭제 O(n) - 뒤 요소들 shift
list.remove(Integer.valueOf(10)); // 값으로 삭제 O(n)
list.clear();              // 전체 삭제 O(n)

// 검색
boolean exists = list.contains(10);  // O(n)
int idx = list.indexOf(10);          // O(n), 없으면 -1
```

### 2. LinkedList (양방향 큐로 사용)
```java
LinkedList<Integer> deque = new LinkedList<>();

// 양 끝 추가/삭제 O(1)
deque.addFirst(1);    // 앞에 추가
deque.addLast(2);     // 뒤에 추가
deque.removeFirst();  // 앞에서 제거
deque.removeLast();   // 뒤에서 제거

// 조회 (느림 주의!)
deque.get(0);         // O(n) - 순차 탐색
```

### 3. 리스트 순회 (3가지 방법)
```java
// ✅ 방법 1: for-each (가장 빠르고 간결)
for (int x : list) {
    System.out.println(x);
}

// ✅ 방법 2: 인덱스 (수정 필요 시)
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}

// ✅ 방법 3: Iterator (삭제 시)
Iterator<Integer> it = list.iterator();
while (it.hasNext()) {
    int x = it.next();
    if (조건) it.remove();  // 안전한 삭제
}
```

---

## 주요 변형 패턴

### 패턴 1: 중간 요소 삭제 (뒤에서부터!)
```java
// ❌ 잘못된 예 - 앞에서부터 삭제 (인덱스 밀림 버그)
for (int i = 0; i < list.size(); i++) {
    if (list.get(i) % 2 == 0) {
        list.remove(i);  // 삭제 후 인덱스 꼬임
    }
}

// ✅ 올바른 예 - 뒤에서부터 삭제
for (int i = list.size() - 1; i >= 0; i--) {
    if (list.get(i) % 2 == 0) {
        list.remove(i);  // 안전
    }
}
```

### 패턴 2: 원형 리스트 처리
```java
// 백준 1158 요세푸스 문제 스타일
List<Integer> list = new ArrayList<>();
int idx = 0;

while (!list.isEmpty()) {
    idx = (idx + K - 1) % list.size();  // 원형 인덱스
    System.out.println(list.remove(idx));
}
```

### 패턴 3: LinkedList를 Deque처럼 사용
```java
// 백준 1406 에디터 문제 스타일
LinkedList<Character> left = new LinkedList<>();
LinkedList<Character> right = new LinkedList<>();

// 커서 기준 좌우로 분할
left.addLast('A');      // 커서 왼쪽
right.addFirst('B');    // 커서 오른쪽

// 커서 이동
char c = left.removeLast();
right.addFirst(c);
```

---

## 실수 포인트 & 디버깅 팁

### ❌ 흔한 실수 1: 삭제 중 size() 캐싱
```java
// ❌ 잘못된 코드
int n = list.size();
for (int i = 0; i < n; i++) {
    list.remove(0);  // size가 줄어드는데 n은 고정
}

// ✅ 올바른 코드
while (!list.isEmpty()) {
    list.remove(0);
}
```

### ❌ 흔한 실수 2: remove() 오버로딩 헷갈림
```java
List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3));

list.remove(1);              // 인덱스 1 삭제 → [1, 3]
list.remove(Integer.valueOf(1)); // 값 1 삭제 → [2, 3]
```

### ❌ 흔한 실수 3: LinkedList로 인덱스 접근
```java
LinkedList<Integer> list = new LinkedList<>();
// ... 데이터 1000개 추가

// ❌ 매우 느림 - O(n) × 반복 = O(n²)
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}

// ✅ for-each 사용 - O(n)
for (int x : list) {
    System.out.println(x);
}
```

---

## 시간복잡도 정리표

| 연산 | ArrayList | LinkedList |
|------|-----------|------------|
| add(끝) | O(1) | O(1) |
| add(i, e) | O(n) | O(n)* |
| get(i) | O(1) | O(n) |
| remove(i) | O(n) | O(n)* |
| removeFirst() | O(n) | O(1) |
| removeLast() | O(1) | O(1) |

*LinkedList는 인덱스 찾기 O(n) + 삭제 O(1) = O(n)

---

## 면접 대비 핵심 Q&A

**Q1. ArrayList와 LinkedList의 내부 구조 차이는?**
- ArrayList: 내부에 Object 배열을 가지고 있으며, 용량 초과 시 1.5배 크기의 새 배열을 만들어 복사
- LinkedList: 각 노드가 prev/next 포인터로 연결된 이중 연결 리스트 구조

**Q2. ArrayList의 중간 삽입이 O(n)인 이유는?**
- 삽입 위치 이후의 모든 요소를 한 칸씩 뒤로 이동(shift)해야 하기 때문
- 예: [1,2,3,4,5]에서 인덱스 2에 삽입 시 → [1,2,?,3,4,5] (3,4,5를 shift)

**Q3. 코딩테스트에서 ArrayList를 주로 쓰는 이유는?**
- 대부분 문제가 조회 중심이며, 캐시 지역성이 좋아 실제 성능이 우수
- LinkedList는 포인터 오버헤드로 메모리도 더 사용

**Q4. List를 사용할 때 주의할 점은?**
- 중간 삭제 시 뒤에서부터 또는 Iterator 사용
- remove()는 인덱스/객체 두 가지 오버로딩이 있으므로 Integer 타입 주의
- 순회 중 size() 변경되므로 조건문에서 직접 호출

**Q5. 언제 LinkedList를 사용하나?**
- 양방향 큐(Deque) 동작이 필요할 때: addFirst/Last, removeFirst/Last
- 예: 백준 1406 에디터, 5430 AC (양방향 삭제)

---

## 핵심 정리
- **기본 선택**: ArrayList (조회 O(1), 실전 90%)
- **양방향 삽입/삭제**: LinkedList (Deque 용도)
- **중간 삭제**: 뒤에서부터 또는 Iterator
- **순회**: for-each > 인덱스 > Iterator
- **디버깅**: remove() 오버로딩, size() 변경 주의
