Set
-------------------------------- 
- 중복을 허용하지 않는 데이터 집합을 저장할 수 있는 인터페이스가 Set 입니다.
- Set은 인터페이스라서 직접적인 객체 생성은 불가능하기 때문에 HashSet, TreeSet, LinkedHashSet과 같은 구현 객체를 사용해야 합니다.
- 즉 Set에는 규칙이 정의 되어 있고, 구현은 HashSet이나 TreeSet등으로 합니다.

HashSet
------------------------------
- HashSet은 중복을 허용하지 않는 Set 인터페이스의 구현 클래스입니다.
- HashSet의 특징으로는 저장된 순서를 유지하지는 않지만, 해시코드(hash code)와 해시 테이블을 이용해서 데이터를 저장하기 때문에 빠른 검색이 가능합니다. ( 해싱 알고리즘 사용 )

TreeSet
-------------------------------
- TreeSet은 중복을 허용하지 않는 Set 인터페이스의 구현 클래스입니다.
- TreeSet의 특징으로는 "오름차순"으로 자동 정렬이 된다는 장점이 있지만, 이진 탐색 트리를 기반으로 하기 때문에 HashSet보다는 검색 속도가 느릴 수 있다는 단점이 있습니다.
- TreeSet에서 Comparator를 활용하면 정렬 기준을 직접 지정하는 것도 가능합니다.

```java
public class SetExample {
    public static void main(String[] args) {
        // Set은 인터페이스이기 때문에 객체 생성은 HashSet이나 TreeSet 같은 구현 클래스의 인스턴스를 생성해야 합니다.
        Set<String> set = new HashSet<>();

        set.add("apple");
        set.add("cherry");
        set.add("banana");
        set.add("apple"); // 중복된 값을 추가하려고 한다고 해봅시다.

        System.out.println(set);
    }
}
```
![image](https://github.com/user-attachments/assets/3ef3aa76-6974-4d8e-ab5d-99b43638eb6b)

- Set 인터페이스를 구현했기 때문에 중복된 값을 저장하려고 하면, 저장이 되지 않는다는 특징이 있습니다.
- 그리고 HashSet을 이용하면 출력시에 순서 보장이 되지 않음을 알 수 있습니다.

```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<Integer> numbers = new HashSet<>();

        numbers.add(10);
        numbers.add(20);
        numbers.add(30);
        numbers.add(10); // 중복 추가 (무시됨)

        System.out.println(numbers); // [20, 10, 30] (순서 보장 X)
    }
}
```
- HashSet은 Set을 구현했기 때문에 직접적인 객체 생성이 가능합니다.

```java
package codingtest.gptsteaching;

import java.util.Set;
import java.util.TreeSet;

public class TreeSetExample {
    public static void main(String[] args) {
        Set<Integer> treeSet = new TreeSet<>();

        // 값을 무작위로 추가해봅시다.
        treeSet.add(10);
        treeSet.add(50);
        treeSet.add(30);
        treeSet.add(40);
        treeSet.add(20);
        treeSet.add(50);

        System.out.println(treeSet);
    }
}
```
- TreeSet은 Set 인터페이스를 구현했기 때문에 마찬가지로 중복은 허용되지 않습니다.
- 그러나 TreeSet은 입력한 순서와 관계없이 오름차순으로 정렬이 되는 것을 확인할 수 있습니다.

```java
package codingtest.gptsteaching;

import java.util.TreeSet;

public class TreeSetStringExample {
    public static void main(String[] args) {
        TreeSet<String> words = new TreeSet<>();

        words.add("banana");
        words.add("apple");
        words.add("cherry");
        words.add("grape");
        words.add("APPLE");
        words.add("banana");

        System.out.println(words);
    }
}
```
- TreeSet에 문자열을 저장하려고 한 경우에도 마찬가지로 중복은 허용되지 않고, 입력 순서와 관계없이 오름차순으로 정렬이 됩니다.
- 대소문자는 구분되기 때문에 apple과 APPLE 모두 저장이 가능합니다.


