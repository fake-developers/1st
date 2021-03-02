# 컬렉션(Collection)

- 컬렉션은 여러 요소들을 담을 수 있는 자료구조이다.
- 즉, 다수의 데이터 그룹이며 다른 말로는 컨테이너라고도 부른다.
- 배열과 비슷하지만 크기가 고정된 배열의 문제점을 보완하였다.

</br>

## Java Collection Framework(JCF)

- 컬렉션 프레임워크는 이러한 데이터 즉, 컬렉션을 다루기 위한 표준화 프로그래밍 방식

- 자바 초기에는 Vector, Stack, HashTable 등의 컬렉션 클래스만 제공하였으나, 자바 1.2이후로 컬렉션을 다루기 위해 컬렉션 프레임워크가 등장하였다.

  - 컬렉션 내의 모든 클래스명은 구현한 인터페이스명을 포함하지만, 컬렉션 프레임워크 이전부터 존재하던 크래스들을은 이러한 명명법을 따르지 않는다.

- 배열의 문제점을 해결하고, 널리 알려져 있는 자료구조를 바탕으로 객체들을 효율적으로 추가, 삭제, 검색할 수 있도록 한다.

- 컬렉션 프레임워크는 몇 가지 인터페이스를 통해 다양한 컬렉션 클래스를 이용할 수 있도록 한다.

- java.util 패키지에 컬렉션과 관련된 인터페이스와 클래스들을 포함시켜 놓았다.

  - 컬렉션 인터페이스 : java.util 패키지
  - 컬렉션 클래스 : java.util 또는 java.util.concurrent 패키지

- #### 컬렉션 프레임워크 상속 구조

  - Collection 인터페이스는 크게 List, Set, Queue로 3개의 상위 인터페이스로 분류할 수 있다.
  - 또한 Map의 경우 Collection 인터페이스를 상속받고 있지 않지 만 Collection으로 분류한다.
    - Map은 구조상의 차이(Key-Value)로 인해 별도로 정의

  <img src="https://user-images.githubusercontent.com/58902042/109483408-89dae400-7ac2-11eb-8fde-510d29be2969.png">

  - Collection Interface : 데이터를 순서, 집합 형태의 저장공간에 담는다.
    1. Set : 순서를 유지하지 않은 상태로 데이터를 저장, 동일한 데이터를 중복 저장할 수 없음.
    2. List : 순서를 유지한 상태로 데이터를 저장, 중복 저장 가능
    3. Queue : List와 흡사, 처리 전 요소를 보유하는데 사용

  <img src="https://user-images.githubusercontent.com/58902042/109483475-a0813b00-7ac2-11eb-9251-3c81371d0eae.png">

  - Map Interface : Key - Value 형태의 저장공간에 데이터를 담는다.
    1. Map : Key와 Value를 하나의 쌍으로 묶어서 관리, Key는 중복 저장 불가

  

  <img src="https://user-images.githubusercontent.com/58902042/109483510-ad9e2a00-7ac2-11eb-9e7f-81e62f6982d9.png" height=350>

  </br>

- #### 컬렉션 인터페이스(Collection Interface)

  - **제네릭**으로 표현

    - 즉, 클래스를 자료형에 상관없이 사용할 수 있다.
    - 컴파일 시점에서 객체의 타입을 체크하기 때문에 런타임 에러를 줄이는데 도움된다.

  - 대표적인 인터페이스

    | **인터페이스 ** | **특징**                                                     | **구현 클래스**                               |
    | --------------- | ------------------------------------------------------------ | --------------------------------------------- |
    | **List**        | - 순서가 있는 데이터의 집합<br>- 데이터 중복 허용            | ArrayList<br>LinkedList<br>Vector             |
    | **Set**         | - 순서를 유지하지 않는 데이터의 집합<br>- 데이터 중복 허용하지 않음 | HashSet<br>TreeSet                            |
    | **Map**         | - 키와 값의 쌍으로 저장<br>-키는 중복 저장 안 됨             | HashMap<br>Hashtable<br>TreeMap<br>Properties |


1. **Collection 인터페이스 그룹**

   - Collection 인터페이스

     \- Collection 인터페이스는 직접적인 구현은 제공하지 않으며 모든 컬렉션 클래스가 구현해야 하는 메서드들을 포함한다.

     - boolean add(E e) : 해당 컬렉션에 전달된 요소를 추가
     - boolean remove(Object o) : 해당 컬렉션에서 전달된 객체를 제거
     - void clear() : 해당 컬렉션의 모든 요소를 제거
     - boolean contains(Object o) : 해당 컬렉션이 전달된 객체의 존재 여부
     - boolean equals(Object o) : 해당 컬렉션과 전달된 객체가 같은지 확인
     - boolean isEmpty() : 해당 컬렉션이 비어있는지 확인
     - Iterator\<E> iterator() : 해당 컬렉션의 반복자(iterator)를 반환
     - int size() : 해당 컬렉션의 요소의 총개수를 반환
     - Object [] toArray() : 해당 컬렉션의 모든 요소를 Object 타입의 배열로 반환

   - List 인터페이스

     \- 순서가 있는 컬렉션이며 중복 요소를 포함한다.

     \- 인덱스로 모든 요소에 접근 가능하다.

   - Set 인터페이스

     \- 중복 요소를 허용하지 않으며, 랜덤 액세스를 허용하지 않는다.

     \- iterator 또는 foreach를 이용하여 요소 탐색 가능

   - SortedSet 인터페이스

     \- 요소를 오름차순으로 유지하는 Set

   - Queue 인터페이스

     \- 처리전의 요소를 보유하는데 사용

     \- FIFO 정렬, 예외적으로 우선순위 큐가 존재

   - Deque 인터페이스

     \- 양쪽 끝에 요소 삽입 및 제거를 지원한다.

2. **Map 인터페이스 그룹**

   - Map 인터페이스

     \- 키와 값을 매핑, 중복 키는 존재할 수 없으며 각 키는 하나의 값만 매핑

     \- Map의 기본 메서드

     - void clear() : 모든 매핑을 삭제
     - boolean containsKey(Object key) : 주어진 키의 존재 여부 반환     
     - boolean containsValue(Object value)  :  주어진 값의 존재 여부 반환    
     - V get(Object key)  : 주어진 키에 해당하는 값 반환
     - boolean isEmpty() : 컬렉션이 비어있는지 여부를 확인
     - V put(K key, V value) : 주어진 키값을 저장하고 값을 반환한다.       
     - V remove(Object key) : 키와 일치하는 원소를 삭제하고 값을 반환한다. 
     - int size() : 컬렉션의 크기를 반환한다.          
     - Set\<K> keySet() :모든 키를 Set 타입으로 반환한다.      
     - Set<Map.Entry<K, V>> entrySet() : 모든 매핑을 Set 타입으로 반환한다.   
     - Collection\<V> values() : 모든 값을 Collection 타입으로 반환한다.  
     
   - SortedMap 인터페이스

     \- 매핑을 오름차순의 키 순서로 유지하는 Map

3. 기타 인터페이스 그룹

   - Iterator 인터페이스

     \- 어떤 컬렉션이든 반복적으로 수행하기 위한 메서드를 제공

     \- List와 Set 인터페이스에서 iterator()메서드 이용가능

     \- iterator 메서드를 통해 컬렉션으로부터 iteraotr instance를 가져올 수 있고, 컬렉션을 순회하는 도중 엘리먼트들을 삭제가능

     - boolean hasNext() : 참조할 다음 번 요소 (element)가 존재하면 true를 반환
     - E next() : 다음 번 요소를 반환
     - void remove() : 현재 위치의 요소를 삭제

     ~~~java
     LinkedList<Integer> lnkList = new LinkedList<Integer>();
      
     lnkList.add(4);
     lnkList.add(2);
     lnkList.add(3);
     lnkList.add(1);
      
     Iterator<Integer> iter = lnkList.iterator();
     
     while (iter.hasNext()) {
         System.out.print(iter.next() + " ");
     }
     //실행결과 4 3 2 1
     ~~~

   - ListIterator 인터페이스

     \- Iterator를 상속한 인터페이스

     \- List에서 제공하는 인터페이스로 Iterator과 달리 양방향으로 목록을 탐색하고 반복하면서 목록을 수정하고, 목록에서 반복자의 현재 위치를 가져올 수 있다.

     \- List인터페이스에서만 listIterator() 메서드 사용가능

     - void add(E e) : 해당 리스트(list)에 전달된 요소 추가(선택적 기능) 
     - boolean hasNext() : 리스트 반복자가 해당 리스트를 순방향으로 순회할 때 다음 요소를 가지고 있으면 true를 반환, 더 이상 다음 요소를 가지고 있지 않으면 false 반환
     - boolean hasPrevious() : 이 리스트 반복자가 해당 리스트를 역방향으로 순회할 때 다음 요소를 가지고 있으면 true를 반환, 더 이상 다음 요소를 가지고 있지 않으면 false를 반환
     - E next() : 리스트의 다음 요소를 반환하고, 커서(cursor)의 위치를 순방향으로 이동
     - int nextIndex() : 다음 next() 메소드를 호출하면 반환될 요소의 인덱스 반환
     - E previous()  : 리스트의 이전 요소를 반환, 커서(cursor)의 위치를 역방향으로 이동
     - int previousIndex() : previous() 메소드를 호출하면 반환될 요소의 인덱스를 반환
     -  void remove() :  next()나 previous() 메소드에 의해 반환된 가장 마지막 요소를 리스트에서 제거(선택적 기능)
     -  void set(E e) : next()나 previous() 메소드에 의해 반환된 가장 마지막 요소를 전달된 객체로 대체(선택적 기능)

     ~~~java
     LinkedList<Integer> lnkList = new LinkedList<Integer>();
     
     lnkList.add(4);
     lnkList.add(2);
     lnkList.add(3);
     lnkList.add(1);
     
     
     ListIterator<Integer> iter = lnkList.listIterator();
     
     while (iter.hasNext()) {
         System.out.print(iter.next() + " ");
     }
     //실행결과 4 2 3 1
      
     
     while (iter.hasPrevious()) {
         System.out.print(iter.previous() + " ");
     }
     //실행결과 1 3 2 4
     ~~~

   - Concurrent 인터페이스 그룹
     - BlockingQueue 인터페이스
     - TransferQueue 인터페이스
     - BlockingDeque 인터페이스
     - ConcurrentMap 인터페이스
     - ConcurrentNavigableMap 인터페이스

   <br>

- #### 컬렉션 클래스(Collection Class) 

  - 컬렉션 인터페이스에 대한 구현 클래스
  - 컬렉션 클래스의 종류
    - **일반적으로 쓰이는 클래스** : ArrayList, LinkedList, HashSet, TreeSet, PriorityQueue, ArrayDeque, HashMap, TreeMap, LinkedHashMap
    - **Concurrent 클래스** : CopyOnWriteArrayList, ConcurrentHashMap, CopyOnWriteArraySet
    - **Legacy 클래스** : Vector, Stack, Dictionary, Hashtable, Properties
    - **Abstract 클래스** : AbstractList, AbstractSequenctailList, AbstractSet, AbstractQueue
    
1. Collection 인터페이스 그룹 클래스
   - ArrayList 클래스
   - LinkedList 클래스
   - HashSet 클래스
   - TreeSet 클래스
   - PriorityQueue 클래스
   - ArrayDeque 클래스

2. Map 인터페이스 그룹 클래스
   
   - HashMap 클래스
   - TreeMap 클래스
   - LinkedHashMap 클래스
   
3.  기타 인터페이스 그룹 클래스

    - Concurrent 클래스

      \- Java 1.5에서 Concurrent 패키지에는 반복하는 동안 컬렉션을 수정할 수 있는 thread-safe한 컬렉션 클래스가 포함되어 있다. 대표적으로,

      -  CopyOnWriteArrayList
      -  ConcurrentHashMap
      -  CopyOnWriteArraySet

- #### 컬렉션즈 클래스(Collections Class)

  - **Collection 인터페이스를 구현한 클래스에 대한 객체생성, 정렬(sort), 병합(merge), 검색(search)등의 기능을 안정적으로 수행하도록 도와주는 역할**

  - 컬렉션에서 작동하거나 반환하는 정적 메서드로만 구성된다.

    - static 메서드이기 때문에 인스턴스를 생성하지 않고 바로 사용 가능

  - Collections와 Collection은 다르다.

  - 자주 사용되는 알고리즘으로는 `정렬(sorting)`, `섞기(shuffling)`, `탐색(searching)`등이 있다.

  - 주요 메서드

    - max()  : 지정된 컬렉션에서 최대 요소 반환 (인덱스 X) 
    - min() : 지정된 컬렉션에서 최소 요소 반환(인덱스 X)     
    - **sort()** : 지정된 컬렉션을 정렬. 오버로드 메소드들이 존재하며 가장 기본적인 메소드는 자연순서에 따라 내림차순으로 렬 
    - **shuffle()** : 지정된 컬렉션의 요소들의 순서를 무작위로 섞는다.          
    - synchronizedCollection() : 지정된 컬렉션에 의해 지원되는 동기화 된 컬렉션을 재생성해 반환
    - **binarySearch()** : 지정된 컬렉션에서 이진 탐색 알고리즘을 사용해 지정된 객체를 검색해 인덱스 반환
    - disjoint() : 2개의 지정된 컬렉션들에서 공통된 요소가 하나도 없는 경우 true 를 반환
    - copy() : 지정된 켈렉션의 모든 요소를 새로운 컬렉션으로 복사 후 반환
    - reverse()  : 지정된 컬렉션에 있는 순서를 역으로 변경

---------------

**<참조>**

- [[Java] Collection Framework1 - List(ArrayList / Vector / LinkedList)](https://minhamina.tistory.com/14)

- [자바 컬렉션 프레임워크(Java Collection Framework) 정리](https://gbsb.tistory.com/247)

- [[JAVA] Java 컬렉션(Collection) 정리](https://gangnam-americano.tistory.com/41)

- [[Java] 컬렉션 프레임워크 - List, Set, Queue, ArrayList, LinkedList, Iterator, Stack, Tree, Map](https://butter-shower.tistory.com/89)

- [자바공부-5.List 인터페이스와 ListIterator 인터페이스](https://scarlett.tistory.com/entry/%EC%9E%90%EB%B0%94%EA%B3%B5%EB%B6%80-5List-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%99%80-ListIterator-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4)

-  [Collections 클래스](https://velog.io/@gillog/Collections-%ED%81%B4%EB%9E%98%EC%8A%A4)