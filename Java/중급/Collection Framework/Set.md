Set 인터페이스의 계층구조
---------------------------------------------------------------------
![image](https://github.com/user-attachments/assets/baef4090-21a0-4ff2-8420-fa5e6e87e473)

- Collection 인터페이스 : Collection 인터페이스는 java.util 패키지의 컬렉션 프레임워크의 핵심 인터페이스입니다. List, Set, Queue 등이 하위 인터페이스입니다.
- Set 인터페이스 : 자바의 Set 인터페이스는 중복을 허용하지 않는 유일한 요소의 집합을 나타냅니다. ( 어떤 요소도 Set 내에 두 번 이상 등장할 수 없습니다. 단, 순서는 보장되지 않습니다. )
- HashSet, LinkedHashSet, TreeSet : Set 인터페이스의 구현 클래스들입니다.

Set 인터페이스의 주요 메서드
----------------------------------------------------
![image](https://github.com/user-attachments/assets/9964cbe4-43eb-4d8b-8481-4c4095f0baf9)

HashSet
----------------------------------------------------
- 해시 자료 구조를 사용해서 요소를 저장하는 Set의 구현 클래스입니다.
- 요소들은 순서 없이 저장되며 HashSet의 주요 연산(추가, 삭제, 삽입)은 평균적으로 O(1)의 시간 복잡도를 가집니다.
- 데이터의 유일성만 중요하고 순서가 중요하지 않은 경우에 적합합니다.

![image](https://github.com/user-attachments/assets/6d6cf9bb-f418-4986-9f08-b5ce302475bb)

LinkedHashSet
--------------------------------------------------------
- LinkedHashSet은 HashSet에 연결 리스트를 추가해서 요소들의 순서를 유지하는 Set의 구현 클래스입니다.
- 요소들은 추가된 순서대로 유지되게 되고, 순서대로 조회 시 추가된 순서대로 반환되게 됩니다.
- 마찬가지로 시간 복잡도는 주요 연산에 대해 평균적으로 O(1)을 가집니다.
- 데이터의 유일성과 함께 삽입 순서를 유지해야 한다면 적합합니다.
- 단, 연결 링크를 유지해야 하기 때문에 HashSet보다는 조금 더 무겁습니다.

![image](https://github.com/user-attachments/assets/39b442a6-0af6-43dc-b73e-8027fce6f1aa)

- 실제로는 양방향으로 연결됩니다.

TreeSet
----------------------------------------------------------------
- TreeSet은 이진 탐색 트리를 개선한 레드-블랙 트리를 내부에서 사용합니다.
- 요소들은 정렬된 순서로 저장됩니다. ( 순서의 기준은 Comparator를 통해 변경 가능합니다. )
- 주요 연산의 시간 복잡도는 O(log n)의 시간 복잡도를 가집니다. ( HashSet보다는 느립니다. )
- 요소들을 정렬된 순서대로 유지하면서 집합의 특성도 유지해야 할 때 사용합니다. ( 단, 이 때 순서는 입력된 순서가 아닌 정렬된 데이터 값의 순서입니다. )

트리 구조
-----------------------------------------------------------
![image](https://github.com/user-attachments/assets/f0969137-ae75-45bb-aaef-6afb61dd683c)

- 트리는 기본적으로 부모 노드와 자식 노드로 구성됩니다.
- 가장 높은 조상은 루트(root)라고 합니다.
- 위 그림처럼 자식이 2개까지 올 수 있는 트리를 이진 트리라고 부릅니다.
- 여기에 노드의 왼쪽 자손은 더 작은 값을 가지고, 노드의 오른쪽 자손은 더 큰 값을 가지는 것을 이진 탐색 트리라고 부릅니다.

![image](https://github.com/user-attachments/assets/a70bed73-7c90-4839-9f08-a52a08fc83a7)

- 이진 탐색 트리는 데이터를 입력하는 시점에 정렬해서 보관한다는 특징을 갖습니다.

![image](https://github.com/user-attachments/assets/72f152f0-2fda-4965-bfda-fe417075daed)

- 이진트리는 검색할 때 위와 같은 방식으로 해당 노드보다 큰 지 작은지 검색해가며 탐색해나갑니다.
- 검색 성능은 O(1)인 해시 검색보다는 느리고, O(n)인 리스트 검색보다는 빠릅니다.
- 이진 탐색 트리 계산의 핵심은 한번에 절반을 날린다는 점입니다.
- 이진 탐색트리는 log2(n)의 시간 복잡도를 갖는데, 어차피 시간 복잡도에서 상수는 무시하므로 O(log n)과 같이 나타낼 수 있습니다.

![image](https://github.com/user-attachments/assets/bad91546-1dd3-488e-b122-129acf62bfe1)

- 이진 탐색 트리의 검색, 삽입, 삭제의 평균 성능은 O(log n)이지만,
- 위와 같이 트리의 균형이 맞지 않을 때는 최악의 경우 O(n)의 성능이 나오게 됩니다.

![image](https://github.com/user-attachments/assets/b111994a-4ca4-48f9-98cd-91ee9ff4757a)

- 데이터를 차례로 순회혀려면 중위 순회라는 방법을 사용할 수 있습니다.
- 이 때는 왼쪽 서브트리를 방문한 다음, 현재 노드를 처리하고, 마지막으로 오른쪽 서브트리를 방문하는 방식으로 순회를 합니다.
- 이러한 방식은 이진 탐색 트리 특성상 노드를 오름차순으로 방문하게 합니다.


레드 블랙 트리
----------------------------------------------------------------------------
- 위와 같이 트리의 균형이 깨져서 성능이 저하되는 문제를 해결하는 방안으로 동적으로 균형을 다시 맞추는 방법이 있습니다.

![image](https://github.com/user-attachments/assets/dec0ccba-85c9-47dd-9d34-9485e3a77053)
- 한쪽으로 치우는 경우 위 그림처럼 중간에 있는 6을 기준으로 다시 정렬하는 방법을 사용할 수 있습니다.
- 자바의 TreeSet은 레드-블랙 트리를 이용해서 균형을 지속해서 유지하도록 내부 설계가 되어 있어 최악의 경우에도 O(log n)의 성능을 제공합니다.

실제 코드로 실습하기
---------------------------------------------------------------------------------
```java
package collection.set.javaset;

import java.util.*;

public class JavaSetMain {
    public static void main(String[] args) {
        run(new HashSet<>());
        run(new LinkedHashSet<>());
        run(new TreeSet<>());
    }

    private static void run(Set<String> set) {
        System.out.println("set = " + set.getClass());
        set.add("C");
        set.add("B");
        set.add("A");
        set.add("1");
        set.add("2");

        Iterator<String> iterator = set.iterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next() + " ");
        }
        System.out.println();
    }
}
```
- HashSet : 입력한 순서가 보장되지 않습니다.
- LinkedHashSet : 입력한 순서를 정확히 보장합니다.
- TreeSet : 데이터 값을 기준으로 정렬됩니다.

자바 HashSet의 최적화
----------------------------------------------------------
![image](https://github.com/user-attachments/assets/3bf8cd89-1143-4212-b905-3bb3fc1bcdad)

- 해시 기반 자료 구조는 통계적으로 입력한 데이터의 수가 배열의 크기를 75% 정도 넘어가면 해시 인덱스가 자주 충돌해서 성능이 저하되기 시작합니다.
- 데이터가 동적으로 추가되기 때문에 배열의 크기를 미리 정하는 것이 어렵습니다.
- 자바의 HashSet은 데이터의 양이 배열 크기의 75%를 넘어가게 되면 배열의 크기를 2배 늘리고, 2배 늘어난 크기를 기준으로 모든 요소에 해시 인덱스를 다시 적용하게 됩니다.
- 이 과정을 재해싱(rehashing)이라고 합니다.

정리
-----------------------------------------------------------------
- 실무에서 Set이 필요한 경우 HashSet을 가장 많이 사용합니다.
- 입력 순서 유지, 정렬이 필요하다면 LinkedHashSet이나 TreeSet을 선택하면 됩니다.
