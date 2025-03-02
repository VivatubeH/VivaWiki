if vs if ~ else if
=============================
조건문을 사용할 때, if문을 사용하는 경우와 if ~ else if를 사용하는 경우의 기준을 나누자면   
다름 아닌 상호배타적이냐 아니냐입니다.

상호배타적
-----------------------
상호배타적이라는 것은 쉽게 말해서, '하나의 조건이 참이면 다른 조건은 절대로 참이될 수 없다'입니다.

#### if문
- 각 조건이 독립적일 때는, if문을 여러 개 사용하는 것이 더 적합합니다.
```java
// 공통점이 몇 개인지 찾기
int common = 0;
if ( 혈액형이 A형 )  {
  common++;
} if ( 고향이 부산 ) {
  common++;
} if ( 성별이 남자 ) {
  common++;
}
```
- 예를 들어 공통점 찾기를 한다고 해봅시다. 남자이면서 A형이면서 부산 출생일 수 있기 때문에
- 위 조건들은 상호 배타적이지 않습니다. 이런 경우라면 if문을 사용하는 것이 적합합니다.

#### if ~ else if문
- 상호배타적일 때는 if ~ else if문을 사용하는 것이 더 적합합니다.
```java
// 성별 구분
boolean isMan = false;

if ( 남자 ) {
  isMan = true;  
} else if ( 여자 ) {
  isMan = false;
}
```
- 위 조건에서는 남자가 아니라면 반드시 여자이기 때문에 상호배타적인 조건이라고 할 수 있습니다.
- 이런 경우라면 if ~ else if문을 사용하는 것이 불필요한 조건 검사를 하지 않기 때문에 더 효율적입니다.

#### if ~ else if와 if ~ else의 차이
- if ~ else if : 여러 조건들 중에서 하나만 해당될 때 사용합니다. ( 점수가 100점, 90점대, 80점대, ... )
- if ~ else : ~이거나 ~이 아니거나로 둘 중 하나를 적용할 때 사용합니다. ( 점수가 90점 넘거나, 안 넘거나 )

```java
int score = 85;

if (score >= 90) {
    System.out.println("장학금 받을 수 있습니다.");
} else if (score >= 80) {
    System.out.println("합격입니다.");
} else {
    System.out.println("불합격입니다.");
}
```

```java
int score = 85;

if (score >= 90) {
    System.out.println("장학금 받을 수 있습니다.");
} else {
    System.out.println("장학금 받을 수 없습니다.");
}
```
