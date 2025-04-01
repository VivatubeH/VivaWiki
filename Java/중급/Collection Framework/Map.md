Map
------------------------------------------------
- Map은 키-값 쌍을 저장하는 자료구조입니다.
- Key는 맵 내에서 유일해야 하며, 검색은 키를 통해 빠르게 이루어집니다.
- Value는 중복이 허용됩니다.
- Map은 별도의 순서를 유지하지 않습니다.

![image](https://github.com/user-attachments/assets/4c6002de-fc7f-4236-833a-9a6a3160ddda)

Map의 상속 계층도
------------------------------------------------------------------------

![image](https://github.com/user-attachments/assets/aead096b-b29a-47b2-b065-06f606e84952)
- 자바는 HashMap, TreeMap, LinkedHashMap 등 다양한 Map 구현체를 제공합니다.
- 이들은 Map 인터페이스의 메서드를 구현하며, 각기 다른 특성과 성능 특징을 가집니다.

Map의 주요 메서드들
-----------------------------------------------------------------------
<table border="1" cellspacing="0" cellpadding="8">
  <thead>
    <tr>
      <th>메서드</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>put(K key, V value)</code></td>
      <td>지정된 키와 값을 맵에 저장한다. (같은 키가 있으면 값을 변경)</td>
    </tr>
    <tr>
      <td><code>putAll(Map&lt;? extends K, ? extends V&gt; m)</code></td>
      <td>지정된 맵의 모든 매핑을 현재 맵에 복사한다.</td>
    </tr>
    <tr>
      <td><code>putIfAbsent(K key, V value)</code></td>
      <td>지정된 키가 없는 경우에 키와 값을 맵에 저장한다.</td>
    </tr>
    <tr>
      <td><code>get(Object key)</code></td>
      <td>지정된 키에 연결된 값을 반환한다.</td>
    </tr>
    <tr>
      <td><code>getOrDefault(Object key, V defaultValue)</code></td>
      <td>지정된 키에 연결된 값을 반환한다. 키가 없는 경우 <code>defaultValue</code>를 반환한다.</td>
    </tr>
    <tr>
      <td><code>remove(Object key)</code></td>
      <td>지정된 키와 그에 연결된 값을 맵에서 제거한다.</td>
    </tr>
    <tr>
      <td><code>clear()</code></td>
      <td>맵에서 모든 키와 값을 제거한다.</td>
    </tr>
    <tr>
      <td><code>containsKey(Object key)</code></td>
      <td>맵이 지정된 키를 포함하고 있는지 여부를 반환한다.</td>
    </tr>
    <tr>
      <td><code>containsValue(Object value)</code></td>
      <td>맵이 하나 이상의 키에 지정된 값을 연결하고 있는지 여부를 반환한다.</td>
    </tr>
    <tr>
      <td><code>keySet()</code></td>
      <td>맵의 키들을 <code>Set</code> 형태로 반환한다.</td>
    </tr>
    <tr>
      <td><code>values()</code></td>
      <td>맵의 값들을 <code>Collection</code> 형태로 반환한다.</td>
    </tr>
    <tr>
      <td><code>entrySet()</code></td>
      <td>맵의 키-값 쌍을 <code>Set&lt;Map.Entry&lt;K, V&gt;&gt;</code> 형태로 반환한다.</td>
    </tr>
    <tr>
      <td><code>size()</code></td>
      <td>맵에 있는 키-값 쌍의 개수를 반환한다.</td>
    </tr>
    <tr>
      <td><code>isEmpty()</code></td>
      <td>맵이 비어 있는지 여부를 반환한다.</td>
    </tr>
  </tbody>
</table>

Map의 사용
---------------------------------------------------------
- 키 목록 조회 : keySet()을 사용하면 Map의 모든 키 목록을 조회합니다. ( 이 때 Map의 키는 중복을 허용하지 않기 때문에 중복을 허용하지 않는 자료구조인 Set을 반환합니다. )

![image](https://github.com/user-attachments/assets/18181967-3afb-40de-86fd-f9477e75b608)

- Entry : 키-값의 쌍으로 이루어진 객체입니다. Map 내부에서 키와 값을 묶어서 저장할 때 사용합니다.
- 즉 우리가 Map에 키와 값으로 데이터를 저장하면, Map 내부에서 키와 값을 하나로 묶는 Entry 객체를 만들어서 보관합니다.

- 값 목록 조회 : Map의 값 목록은 중복을 허용하기 때문에 Set으로 반환할 수 없고, 입력 순서도 보장되지 않기 때문에 순서를 보장하는 List로도 반환할 수 없습니다.
- 그래서 values()를 사용하면 단순한 값의 모음이라는 의미의 상위 인터페이스인 Collection으로 반환됩니다.

Map vs Set
-----------------------------------------------------------
- Map과 Set은 중복을 허용하지 안고, 순서를 보장하지 않는다는 점에서 Map의 키는 Set과 같은 구조입니다.
- 단지 둘의 차이점은 Map은 Key 옆에 Value를 가지고 있다는 것 뿐입니다.

![image](https://github.com/user-attachments/assets/640f3613-bc55-4b20-80a3-c8291f370fc7)

- 그래서 Set의 구현체는 HashSet, LinkedHashSet, TreeSet
- Map의 구현체는 HashMap, LinkedHashMap, TreeMap으로 거의 같습니다.

HashMap, LinkedHashMap, TreeMap
---------------------------------------------------------
- HashMap : 해시를 이용해서 요소를 저장합니다. 키는 해시 함수를 통해 해시 코드로 변환되고, 이 해시코드는 데이터를 저장하고 검색하는 데 사용됩니다.
- 삽입, 삭제, 검색 작업은 해시 자료 구조를 사용하기 때문에 일반적으로 O(1)의 시간 복잡도를 가집니다.
- 순서는 보장되지 않습니다.

- LinkedHashMap : HashMap과 유사하지만 연결 리스트를 사용해서 삽입 순서 또는 최근 접근 순서에 따라 요소를 유지합니다.
- 입력 순서에 따른 순회가 가능하지만, 입력 순서를 링크로 유지해야 하기 때문에 조금 더 무겁습니다.
- HashMap과 유사하게 대부분의 작업은 O(1)의 시간 복잡도를 갖습니다.
- 입력 순서가 보장됩니다.

- TreeMap : 레드-블랙 트리를 기반으로 한 구현이 되어 있습니다.
- 모든 키는 자연 순서 또는 생성자에 제공된 Comparator에 의해 정렬됩니다.
- get, put, remove 등의 주요 작업들은 O(log n)의 시간 복잡도를 갖습니다.
- 키는 정렬된 순서로 저장됩니다.

![image](https://github.com/user-attachments/assets/0404a698-32a0-45d1-90ec-919ee5b66570)

- HashMap은 HashSet처럼 자료를 저장한느데, 키-값 저장을 해야 하므로 Entry 객체를 저장할 뿐입니다.
- 당연히 Map의 Key로 사용되는 객체는 hashCode(), equals()를 반드시 구현해야 합니다.

정리
-----------------------------------------------------------------
- 실무에서 Map이 필요할 때 : HashMap을 많이 사용합니다.
- 순서 유지, 정렬이 필요하다면 : LinkedHashMap, TreeMap 등을 선택합니다.
