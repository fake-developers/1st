# Map Collection Class

:bulb:***여기에 나오는 설명의 전반적인 내용을 알기위해서는 Collection인터페이스에 대해 먼저 공부하고 오는 것을 권장 합니다. [여기 ](./Collection.md) 클릭***

- Map 인터페이스를 구현한 클래스

  - **데이터의 저장 순서를 유지 하지 않음**
  - **키는 중복을 허용하지 않지만, 값의 중복은 허용**
    - 만약, 기존에 저장된 키와 동일한 키로 값을 저장하면 기존 값이 사라지고 새로운 값으로 대체된다.

- Map 인터페이스는 Collection 인터페이스와는 다른 저장 방식을 가진다.

- Map 인터페이스를 구현한 Map 컬렉션 클래스들은 **키와 값을 하나의 쌍으로 저장하는 방식(key-value 방식)**을 사용한다.

  - 여기서 키(key)는 실질적인 값(value)을 찾기위한 이름의 역할이다.
  - 키와 값은 모두 객체

  <img src="https://user-images.githubusercontent.com/58902042/110233716-37d60a80-7f69-11eb-9fa0-51d0704657d3.png" height=270>  

- 주요 메서드

  | **기능**      | **메소드**                                                   | **설명**                                                     |
  | ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | **객체 추가** | - V put(K key, V value)                                      | - 주어진 객체를 저장(객체가 성공적으로 저장되면 true 리턴 중복 객체면 false 리턴) |
  | **객체 검색** | - boolean containsKey(Object key)<br>- boolean containsValue(Object value)<br>- Set<Map.Entry<K,V> entrySet()<br>- V get(Object key)<br>- Set\<L> keySet<br>- int size()<br><br>- Collection\<V> values()<br>- Object toArray() | - 주어진 키가 저장되어 있는지 여부 <br>- 주어진 값이 있는지 여부<br>- 컬렉션이 비어 있는지 조사<br>- 키와 값의 쌍으로 구성된 모든 Map.Entry 객체를 Set에 담아서 리턴 <br>- 주어진 키가 있는 값을 리턴<br>- 모든 키를 Set 객체에 담아서 리턴<br>- 저장되어 있는 전체 객체 수 리턴<br>- 저장된 모든 값을 Collection에 담아서 리턴<br>- 저장된 객체들을 객체 배열의 형태로 반환 |
  | **객체 삭제** | - void clear()<br>- boolean remove(Object o)                 | - 저장된 모든 객체를 삭제<br>- 주어진 객체를 삭제 / boolean removeAll(Collection<?> c) |

  - 메서드의 매개 변수의 타입과 리턴 타입이 K,V 타입 파라미터로 지정됨

  - 제네릭 타입을 사용하기 때문에 구체적인 타입은 구현 객체를 생성할 때 결정

  - **Key와 Value값 찾기**

    - 키를 알고 있다면 get() 메서드로 간단히 객체를 찾을 수 있다.

    - 하지만, 저장된 객체 대상으로 하나씩 얻고 싶을 경우에 사용하는 경우,

      1. keySet()메소드 이용

         - keySet() 메서드로 모든 키를 Set 컬렉션으로 얻는다.
         - 반복자를 통해 키를 하나씩 얻고
         - get() 메서드를 통해 값을 얻는다.

         ~~~java
         Map<K, V> map = ...; //생략
         Set<K> keySet = map.keySet();
         Iterator<K> keyIterator = keySet.iterator();
         while(keyIterator.hasNext()) {
         	K key = keyIterator.next();
             V value = map.get(key);
         }
         ~~~

      2. entrySet() 메서드 이용

         - entrySet() 메소드로 모든 Map.Entry를 Set 컬렉션으로 얻는다.
         - 반복자를 통해 Map.Entry를 하나씩 얻고,
         - getKey()와 getValue() 메소드를 이용해 키와 값을 얻으면 된다.

         ~~~java
         Set<Map.Entry<K, V>> entrySet = map.entrySet();
         Iterator<Map.Entry<K,V>> entryIterator = entrySet.iterator();
         while(entryIterator.hasNext()) {
         	Map.Entry<K, V> entry = entryIterator.next();
             K key = entry.getKey();
             V value = entry.getValue();
         }
         ~~~

- 대표적인 Map 컬렉션 클래스

  1. HashMap<K, V>
2. Hashtable<K, V>
  3. TreeMap<K, V>

<br>

## HashMap\<K,V>

- Map 컬렉션 클래스에서 가장 많이 사용되는 클래스 중 하나

- JDK 1.2부터 제공된 HashMap 클래스는 *해시 알고리즘*을 사용하여 검색 속도가 매우 빠르다. 

- Map 인터페이스를 구현하므로, 중복된 키로는 값을 저장할 수 없다.

  - 하지만, 같은 값을 다른 키로 저장하는 것은 가능하다.

- Set 인터페이스를 구현하는 HashSet 클래스와 마찬가지로 hashCode()와 equals()를 재정의하여 동등 객체가 될 조건을 정한다. 자세한 내용은 [여기](./Collection-Set.md)에서 확인

- ex_)

  ~~~java
  HashMap<String, Integer> hm = new HashMap<String, Integer>();
   
  
  // put() 메소드를 이용한 요소의 저장
  hm.put("삼십", 30);
  hm.put("십", 10);
  hm.put("사십", 40);
  hm.put("이십", 20);
   
  // Enhanced for 문과 get() 메소드를 이용한 요소의 출력
  System.out.println("맵에 저장된 키들의 집합 : " + hm.keySet());
  for (String key : hm.keySet()) {
      System.out.println(String.format("키 : %s, 값 : %s", key, hm.get(key)));
  }
  
  // remove() 메소드를 이용한 요소의 제거
  hm.remove("사십");
  
  
  // iterator() 메소드와 get() 메소드를 이용한 요소의 출력
  Iterator<String> keys = hm.keySet().iterator();
  while (keys.hasNext()) {
      String key = keys.next();
      System.out.println(String.format("키 : %s, 값 : %s", key, hm.get(key)));
  }
  
  
  // replace() 메소드를 이용한 요소의 수정
  hm.replace("이십", 200);
  for (String key : hm.keySet()) {
      System.out.println(String.format("키 : %s, 값 : %s", key, hm.get(key)));
  }
  
   
  
  // size() 메소드를 이용한 요소의 총 개수
  System.out.println("맵의 크기 : " + hm.size());
  
  //실행결과
  //맵에 저장된 키들의 집합 : [이십, 삼십, 사십, 십]
  //키 : 이십, 값 : 20
  //키 : 삼십, 값 : 30
  //키 : 사십, 값 : 40
  //키 : 십, 값 : 10
  
  //키 : 이십, 값 : 20
  //키 : 삼십, 값 : 30
  //키 : 십, 값 : 10 
  
  //키 : 이십, 값 : 200
  //키 : 삼십, 값 : 30
  //키 : 십, 값 : 10
   
  //맵의 크기 : 3
  ~~~

  - HashMap을 생성하기 위해서는 키 타입과 값 타입을 파라미터로 주고 기본 생성자를 호출
  - **키와 값의 타입**은 기본 타입(byte, shortm int, float, double, boolean, char)을 사용할 수 없고 **클래스 및 인터페이스 타입만 가능**하다.
  - 위의 예제에서 사용된 Enhanced for문은 JDK 1.5부터 추가되었다.
    - 이 반복문은 배열과 컬렉션 프레임워크에서 해당 인스턴스에 저장된 모든 요소를 순회해야할 경우에 자주 사용된다.

<BR>

## Hashtable<K, V>

- JDK 1.0부터 사용해 온 HashMap 클래스와 같은 동작을 하는 클래스

  - 따라서 동일한 구조를 가지고 있다.

  - HashMap과 마찬가지로 hashCode()와 equals()를 재정의하여 동등 객체가 될 조건을 정한다. 자세한 내용은 [여기](./Collection-Set.md)에서 확인

  - HashMap과의 차이점은 Hashtable은 `동기화된(Synchronized) 메소드`로 구성되어있다.

    - 하나의 스레드가 실행을 완료해야만 다른 스레드를 실행할 수 있다.

    - thread safe 하다. 

      \+) ArrayList와 Vector의 관꼐와 유사하다.

    <img src="https://user-images.githubusercontent.com/58902042/110234539-60143800-7f6e-11eb-880d-9beb42ea588a.png" height=180> 

- #### Properties

  - Hashtable의 하위 클래스
    -     따라서 Hashtable의 모든 특징을 그대로 가지고 있다.
  - Hashtable과의 차이점
    - Hashtable :  키와 값을 다양한 타입으로 지정이 가능
    - Properties :  키와 값을 String 타입으로 제한한 컬렉션
  - Properties는 애플리케이션의 옵션 정보, 데이터베이스 연결 정보 그리고 국제화(다국어) 정보가 저장된 프로퍼티(~. Properties) 파일을 읽을 때 주로 사용

<BR>

## TreeMap

- **키와 값을 한 쌍으로 하는 데이터**를 **이진 검색 트리(binary search tree)의 형태로 저장**

- JDK 1.2부터 제공된 TreeMap 클래스는 NavigableMap 인터페이스를 기존의 이진 검색 트리의 성능을 향상시킨 **레드-블랙 트리(Red-Black tree)**로 구현

- Map 인터페이스를 구현하므로, 중복된 키로는 값을 저장할 수 없다.

  - 하지만, 같은 값을 다른 키로 저장하는 것은 가능하다.

- Set 인터페이스를 구현한 TreeSet과 유사하다.

  - TreeSet과의 차이점

    - 키와 값이 저장된 Map.Entry를 저장한다
    - TreeMap에 객체를 저장하면 자동으로 정렬
    - 기본적으로 부모 키값과 비교해서 키 값이 낮은 것은 왼쪽 자식 노드에, 키 값이 높은 것은 오른쪽 자식 노드에 Map.Entry 객체를 저장

    <img src="https://user-images.githubusercontent.com/58902042/110234854-33612000-7f70-11eb-8beb-b1b27c313950.png" height=270> 

- ex_)

  ~~~java
  TreeMap<Integer,String> tm = new TreeMap<Integer,String>();
  
  // put() 메소드를 이용한 요소의 저장
  tm.put(1, "일");
  tm.put(3, "삼");
  tm.put(5, "오");
  tm.put(4, "사");
  
  //NavigableSet을 이용한 정렬키 리턴
  NavigableSet<Integer> navi = tm.navigableKeySet();
  
  // iterator() 메소드와 get() 메소드를 이용한 요소의 출력
  System.out.println("오름차순 출력");
  Iterator<Integer> itr = navi.iterator();
  while(itr.hasNext())
      System.out.println(tm.get(itr.next()));
  
  //실행결과
  //오름차순 출력
  //일
  //삼
  //사
  //오
  ~~~

  - TreeMap을 생성하기 위해서는 키로 저장할 객체 타입과 값으로 저장할 객체 타입을 타입 파라미터로 주고 기본 생성자를 호출
  - Map 인터페이스 타입 변수에 대입해도 된다.
  - TreeMap 클래스 타입으로 대입한 이유
    - 특정 객체를 찾거나 범위 검색과 관련된 메소드를 사용하기 위해서

- **TreeMap의 검색 관련 메서드**

  | 리턴 타입      | 메소드 명           | 설명                                                         |
  | -------------- | ------------------- | ------------------------------------------------------------ |
  | Map.Entry<K,V> | firstEntry()        | 제일 낮은 Map.Entry 리턴                                     |
  | Map.Entry<K,V> | lastEntry()         | 제일 높은 Map.Entry 리턴                                     |
  | Map.Entry<K,V> | lowerEntry(K key)   | 주어진 객체보다 바로 아래 Map.Entry 리턴                     |
  | Map.Entry<K,V> | higherEntry(K key)  | 주어진 객체보다 바로 위 Map.Entry 리턴                       |
  | Map.Entry<K,V> | floorEntry(K key)   | 주어진 객체와 동등한 키가 있으면 해당 Entry 리턴, 만약 없다면 주어진 키 바로 아래의 Entry를 리턴 |
  | Map.Entry<K,V> | ceilingEntry(K key) | 주어진 객체와 동등한 키가 있으면 해당 Entry 리턴, 만약 없다면 주어진 객체 바로 위의 Entry를 리턴 |
  | Map.Entry<K,V> | pollFirstEntry()    | 제일 낮은 Entry를 꺼내오고, 컬렉션에서 제거함                |
  | Map.Entry<K,V> | pollLastEntry()     | 제일 높은 Entry를 꺼내오고, 컬렉션에서 제거함                |

-  **TreeMap의 정렬 관련 메소드**

  | **리턴 타입**      | **메소드**         | **설명**                                            |
  | ------------------ | ------------------ | --------------------------------------------------- |
  | NavigableSet<K>    | descendingKeySet() | 내림차순으로 정렬된 키의 NavigableSet을 리턴        |
  | NavigableMap<K, V> | descendingMap()    | 내림차순으로 정렬된 Map.Entry의 NavigableMap을 리턴 |

  

-----------

**<참조>**

- [[Java] Collection Framework 3 - Map(HashMap / LinkedHashMap / TreeMap / HashTable/ Properties)](https://minhamina.tistory.com/46)

- [[Java] 컬렉션 프레임워크 - List, Set, Queue, ArrayList, LinkedList, Iterator, Stack, Tree, Map](https://butter-shower.tistory.com/89)

- http://www.tcpschool.com/java/java_collectionFramework_map

- [Java/Collection] Java Collection Framework에 대한 이해를 통해 Data Structure 이해하기.](https://postitforhooney.tistory.com/entry/JavaCollection-Java-Collection-Framework%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4%EB%A5%BC-%ED%86%B5%ED%95%B4-Data-Structure-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)