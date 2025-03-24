Comparable, Comparator을 언제 사용할까요?
---------------------------------------------------
자바 컬렉션(ArrayList, TreeSet) 등에서 사용자가 정의한 객체를 정렬하고 싶을 때, Comparator와 Comparable이라는 인터페이스들을 사용할 수 있습니다.

정렬 기준 설정
----------------------------------------------
- HashSet : 저장된 순서도 보장되지 않기에, 정렬 기준 설정이 불가능합니다. 정렬을 원하면 List로 변환해서 정렬해야 합니다.
- TreeSet : 최초 객체 생성시에 Comparator를 통해 정렬 기준을 정의할 수 있습니다. 이후 변경은 불가합니다.
```java
package codingtest.gptsteaching;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class ComparatorComparbleMain {
    public static void main(String[] args) {
        List<Person> people = new ArrayList<>();
        people.add(new Person("Alice", 25));
        people.add(new Person("Bob", 30));
        people.add(new Person("Charlie", 20));
//        Collections.sort(people); 사용자 정의 클래스는 정렬 기준이 없어서 정렬이 불가능합니다.

        System.out.println(people);
    }
}
class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}
```
- 사용자 정의 클래스는 정렬 기준이 별도로 없기 때문에 정렬을 할 수 없습니다.

compareTo 메서드
---------------------------------
- compareTo 메서드는 두 객체의 크기나 순서를 비교할 때 사용되며, 비교 결과로 0, 양수, 음수 중 하나의 값을 반환하도록 되어 있습니다.
- 해당 메서드를 재정의함으로써 사용자 정의 객체의 정렬기준을 부여할 수 있습니다.

```java
public int compareTo(T o);
```
- 현재 객체가 비교 대상 객체보다 크다면 : 양수를 반환합니다.
- 현재 객체와 비교 대상 객체가 같다면 : 0을 반환합니다.
- 현재 객체와 비교 대상 객체보다 작다면 : 음수를 반환합니다.

```
양수가 반환되면 -> 현재 객체가 비교 대상 객체보다 크네? -> 현재 객체를 뒤로 보내버립니다.
음수가 반환되면 -> 현재 객체가 비교 대상 객체보다 작네? -> 비교 대상 객체를 앞으로 가져옵니다.
```

Comparable 인터페이스
-------------------------------------------
- Comparable 인터페이스는 클래스 자체에 기본 정렬 기준을 정의할 때 사용합니다.
- 한 가지의 기본 정렬 방식만 설정할 수 있습니다.

```java
package codingtest.gptsteaching;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

class Student implements Comparable<Student> {
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 나이를 기준으로 기본 정렬 기준을 오름차순으로 가져가 보겠습니다.
    @Override
    public int compareTo(Student other) {
        return this.age - other.age;
    }

    @Override
    public String toString() {
        return name + ", " + age;
    }
}
public class ComparableExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 25));
        students.add(new Student("Bob", 30));
        students.add(new Student("Charlie", 20));

        Collections.sort(students); // 나이순 정렬 ( 기본 정렬 )
        System.out.println(students);
    }
}
```
- 나이라는 클래스 자체의 정렬 기준을 compareTo 메서드를 통해 구현했습니다.
- Student라는 클래스 자체에 정렬 기준을 설정한 경우입니다.

Comparator 인터페이스
----------------------------------------------------
- Comparator는 여러 개의 정렬 기준을 유연하게 적용할 때 사용합니다.

```java
package codingtest.gptsteaching;

import java.sql.Array;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class Student {
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String toString() {
        return name + " (" + age + "세)";
    }
}

class NameComparator implements Comparator<Student> {
    @Override
    public int compare(Student o1, Student o2) {
        return o1.name.compareTo(o2.name); // String의 기본적인 오름차순 정렬 compareTo를 활용합니다.
    }
}

class AgeCompartor implements Comparator<Student> {
    @Override
    public int compare(Student o1, Student o2) {
        return o1.age - o2.age;
    }
}

public class ComparatorExample {
    public static void main(String[] args) {
        ArrayList<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 22));
        students.add(new Student("Bob", 18));
        students.add(new Student("Charlie", 25));

        System.out.println("정렬 전: " + students);

        // 이름을 기준으로 정렬하려고 할 때
        Collections.sort(students, new NameComparator()); // NameCompartor라는 정렬 기준 클래스를 기준으로 정렬합니다.
        System.out.println(students);

        // 나이를 기준으로 정렬하려고 할 때
        Collections.sort(students, new AgeCompartor());
        System.out.println(students);
    }
}
```
- 정렬 기준을 제공하는 클래스들을 여러 개 정의함으로써 여러 개의 정렬 기준을 유연하게 적용할 수 있게 되었습니다.
