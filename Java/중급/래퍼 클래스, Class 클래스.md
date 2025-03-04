기본형이 갖는 한계
-----------------------------------------------
- 객체 지향 프로그래밍의 객체에는 다양한 메서드들이 제공됩니다. 하지만, 기본형은 객체가 아니므로 메서드를 제공할 수가 없습니다.
- 데이터가 없을 경우, 참조형은 null로 상태를 나타낼 수 있습니다. 그러나, 기본형은 데이터가 없다는 그 상태를 나타낼 방법이 없습니다.

```java
public static void main(String[] args) {
    int value = 10;
    int i1 = compareTo(value, 5);
    int i2 = compareTo(value, 10);
    int i3 = compareTo(value, 20);
    System.out.println("i1 = " + i1);
    System.out.println("i2 = " + i2);
    System.out.println("i3 = " + i3);
}
public static int compareTo(int value, int target) {
    if (value < target) {
        return -1;
    } else if (value > target) {
        return 1;
    } else {
        return 0;
    }
}
```

- 비교를 위해 외부의 메서드를 찾아서 사용해야 합니다. 만약, 객체라면 자신이 쓸 기능을 만들어서 사용하는 것이 더 유용할 것입니다.

래퍼클래스(Wrapper)
-----------------------------------------
특정한 기본형을 감싸서(Wrap) 만드는 클래스를 래퍼 클래스(Wrapper class)라고 합니다.



