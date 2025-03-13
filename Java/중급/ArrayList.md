List 자료구조의 등장 배경
-----------------------------------
- 기존 배열은 길이를 동적으로 변경할 수 없고, 데이터를 한 칸씩 수동으로 밀어야 해서 추가하기가 불편했습니다.
- 이러한 불편을 해소하기 위해 등장한 것이 바로 List 자료구조입니다.

List 자료 구조란?
----------------------------------
- 순서가 있고, 중복을 허용하는 자료 구조를 List라고 합니다.
- 일반적으로 배열은 크기가 정적으로 고정되지만, 리스트는 크기가 동적으로 변할 수 있다는 점에서 둘은 구분됩니다.

ArrayList란?
--------------------------------
- List라는 자료 구조를 사용하면서, 내부 데이터는 Array(배열)에 보관하는 자료 구조를 말합니다.

ArrayList의 빅오
---------------------------------
- 데이터를 마지막에 추가하는 경우 : O(1)
- 데이터를 앞이나 중간에 추가하는 경우 : O(n)

- 데이터를 마지막에 삭제하는 경우 : O(1)
- 데이터를 앞이나 중간에 삭제하는 경우 : O(n)

- 인덱스를 조회하는 경우 : O(1)
- 데이터를 검색하는 경우 : O(n)

ArrayList 사용이 효율적인 경우
------------------------------------
- 빅오 표기법으로 보듯 ArrayList는 마지막에 데이터를 추가하거나 삭제할 때는 O(1)로 매우 빠릅니다.
- 그렇기 때문에 보통 ArrayList는 데이터를 중간에 추가 및 삭제 변경하는 경우보다 데이터를 순서대로 입력하고, 순서대로 출력하는 경우에 가장 효율적입니다.

ArrayList에 제네릭 없이 사용할 경우
------------------------------------
```java
package collection.array;
public class MyArrayListV3BadMain {
  public static void main(String[] args) {
    MyArrayListV3 numberList = new MyArrayListV3();
    // 숫자만 입력 하기를 기대
    numberList.add(1);
    numberList.add(2);
    numberList.add("문자3"); //문자를 입력
    System.out.println(numberList);
    // Object를 반환하므로 다운 캐스팅 필요
    Integer num1 = (Integer) numberList.get(0);
    Integer num2 = (Integer) numberList.get(1);
    // ClassCastException 발생, 문자를 Integer로 캐스팅
    Integer num3 = (Integer) numberList.get(2);
  }
}
```
- 보통 Object를 그대로 사용하게 되면, 타입 안정성이 떨어지게 됩니다.
- 자료구조라 하면 보통 서로 관련 있는 데이터 타입을 보관하게 되므로 제네릭을 도입하는 것이 효과적일 것입니다.

ArrayList에 제네릭을 도입한 경우
--------------------------------------------
```java
package collection.array;
public class MyArrayListV4Main {
    public static void main(String[] args) {
        MyArrayListV4<String> stringList = new MyArrayListV4<>();
        stringList.add("a");
        stringList.add("b");
        stringList.add("c");
        String string = stringList.get(0);
        System.out.println("string = " + string);
        MyArrayListV4<Integer> intList = new MyArrayListV4<>();
        intList.add(1);
        intList.add(2);
        intList.add(3);
        Integer integer = intList.get(0);
        System.out.println("integer = " + integer);
    }
}
```
- 제네릭을 적용하게 되면 위험한 다운캐스팅 없이 관련있는 데이터 타입만 저장할 수 있게 되었습니다.

ArrayList가 갖는 단점
-------------------------------------------------
- 정확한 크기를 알지 못한다면 메모리가 낭비되게 됩니다.
- 데이터를 추가하거나 삭제하는 것이 비효율적입니다. ( 결국 내부에서 배열을 사용하므로 이런 한계는 극복할 수 없습니다. )
