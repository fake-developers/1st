## Collection Framework[HashMap, TreeMap]

<br/>

### <u>Map 컬렉션</u>

* 비선형 자료구조
* 대응관계를 쉽게 표현할 수 있게 해주는 자료형
* 키(key)를 값(value)에 매핑하는 기능을 제공
  * 키(key)는 중복으로 저장할 수 없고 값(value)은 중복으로 저장할 수 있다.
  * 중복된 키(key)값이 들어온다면 기조의 값은 없어지고 새로운 값으로 대치된다.

<br/>

#### 주요 메소드

| 메소드                              | 설명                                                       |
| ----------------------------------- | ---------------------------------------------------------- |
| V put(K Key, V value)               | 주어진 키와 값을 추가하여 저장되면 값을 리턴합니다.        |
| boolean containsKey(Object Key)     | 주어진 키가 있는지 확인합니다.                             |
| boolean containsValue(Object value) | 주어진 값이 있는지 확인합니다.                             |
| Set<Map.Entry<K,V>> entrySet()      | 모든 Map.Entry 객체를 Set에 담아 리턴합니다.               |
| Set<K> keySet()                     | 모든 키를 Set객체에 담아서 리턴합니다.                     |
| V get(Object key)                   | 주어진 키에 있는 값을 리턴합니다.                          |
| boolean isEmpty()                   | 컬렉션이 비어있는지 조사합니다.                            |
| int Size()                          | 저장되어 있는 전체 객체의 수를 리턴합니다.                 |
| Collection<V> values()              | 저장된 모든 값을 Collection에 담아서 리턴합니다.           |
| void clear()                        | 저장된 모든 Map.Entry를 삭제합니다.                        |
| V remove(Object Key)                | 주어진 키와 일치하는 Map.Entry를 삭제하고 값을 리턴합니다. |

<br/>

### <u>HashMap</u>

Map 인터페이스를 구현한 대표적인 Map 컬렉션이다. Map 인터페이스를 상속하고 있기에 Map의 성질을 그대로 가지고 있다.

>  **HashMap<E(Key),E(Value)> 객체명 = new HashMap<E(Key),E(Value)>();**

* HashMap은 해시 함수를 통해 '키'와 '값'이 저장되는 위치를 결정하므로, 사용자는 그 위치를 알 수 없고, 삽입되는 순서와 들어 있는 위치 또한 관계가 없다.

<br/>

#### 예제

~~~~java
import java.util.HashMap;

public class HashMapCollection {
    public static void main(String[] args){
        HashMap<Integer, String> map = new HashMap<>();

        // Key-Value 기반 데이터 저장
        map.put(45, "Brown");
        map.put(37, "James");
        map.put(23, "Martin");

        // 데이터 탐색
        System.out.println("23번 : " + map.get(23));
        System.out.println("37번 : " + map.get(37));
        System.out.println("45번 : " + map.get(45));

        // 데이터 삭제
        map.remove(37);

        // 데이터 삭제 확인
        System.out.println("37번 : " + map.get(37));
    }
}

//결과
//23번 : Martin
//37번 : James
//45번 : Brown
//37번 : null
~~~~

<br/>

### <u>TreeMap</u>

TreeMap은 이진트리를 기반으로 한 Map 컬렉션이다.

>  **TreeMap<E(Key),E(Value)> 객체명 = new TreeMap<E(Key),E(Value)>();**

* 같은 Tree구조로 이루어진 TreeSet과의 차이점은 TreeSet은 그냥 값만 저장한다면 TreeMap은 키와 값이 저장된 Map, Etnry를 저장한다.
* 자동 오름차순으로 정렬된다.
  * 숫자 타입일 경우에는 값, 문자열 타입일 경우에는 유니코드로 정렬
  * 정렬 순서는 기본적으로 부모 키값과 비교해서 키 값이 낮은 것은 왼쪽 자식 노드에 키값이 높은 것은 오른쪽 자식 노드에 Map.Etnry 객체를 저장한다.

<br/>

#### 예제

~~~~java
import java.util.Iterator;
import java.util.Set;
import java.util.TreeMap;

public class TreeMapIteration {
    public static void main(String[] args) {
        TreeMap<Integer, String> map = new TreeMap<>();
        // ~~~ 위와 동일 
    }
}

//결과
//23 37 45
//Martin James Brown
//Martin James Brown
~~~~

<br/>



### <u>HashMap과 TreeMap의 성능 비교</u>

* **Map으로써의 성능**

  HashMap > TreeMap

* **많은 양의 데이터를 검색할 때**

  HashMap → Hashing을 사용하기 때문에

* **정렬된 상태로 Map을 유지하거나, 정렬된 데이터를 조회해야하는 범위 검색이 필요할 때**

  TreeMap

<br/>

<br/>

<br/>

### REFERENCE

* [HashMap, TreeMap(1)](https://github.com/fake-developers/1st/blob/JYJ-06/JYJ/HashMapAndTreeMap.md)
* [HashMap, TreeMap(2)](https://github.com/fake-developers/1st/blob/KJY-06/KJY/%5BJAVA%5D%20%EC%BB%AC%EB%A0%89%EC%85%98%20%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%20-%20Map%20%EC%BB%AC%EB%A0%89%EC%85%98.md)
* [HashMap](https://coding-factory.tistory.com/556?category=758267)
* [TreeMap](https://coding-factory.tistory.com/557?category=758267)
* [Collection](https://coding-factory.tistory.com/550)

