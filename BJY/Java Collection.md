## Java Collection

<br/>

### <u>Java Collection Framework</u>

> **Collection 객체**
>
> 데이터의 집합, 그룹 (컨테이너)
>
> 여러 원소들을 담을 수 있는 자료구조

**JCF(Java Collections Framework)**는 이러한 데이터, 자료구조인 컬렉션과 이를 구성하는 클래스를 정의하는 인터페이스를 제공한다.

**배열의 문제점을 해결하고, 널리 알려져 있는 자료구조를 바탕으로 객체들을 효율적으로 추가, 삭제, 검색할 수 있도록 java.util 패키지에 컬렉션과 관련된 인터페이스와 클래스들을 포함시킨 것이다.**

<br/>

#### <u>컬렉션 프레임워크 계층구조</u>

![collection 계층구조](https://user-images.githubusercontent.com/61674527/109425221-a3c8e800-7a2a-11eb-8ad7-3cff5dee5f89.png)

<br/>

#### <u>장점</u>

- 코딩 시간 감소

- 코드 품질 보장

- 유지보수 시간 감소

- 재사용 가능 & 상호 운용성 보장

  ~~~
  상호 운용성
  
  하나의 시스템이 동일 또는 이기종의 다른 시스템과 아무런 제약이 없이 서로 호환되어 사용할 수 있는 성질
  ~~~

  

### <u>컬렉션 인터페이스(Collection Interface)</u>

#### 제네릭(Generics)으로 표현

컴파일 시점에서 객체의 타입을 체크하기 때문에 런타임 에러를 줄이는 데 도움이 된다. 예를 들어 런타임 시 발생하는 ClassCastException을 컴파일 시점에서 찾아낼 수 있다. 또한 클래스 캐스팅을 하지 않아도 되고 instansof를 사용하지 않아도 되므로 코드를 좀 더 깔끔하게 유지할 수 있다.

**대표적인 인터페이스**

* List 인터페이스
* Set 인터페이스
* Map 인터페이스

#### Collection 인터페이스의 대표적인 메소드

직접적인 구현은 제공하지 않으며 모든 컬렉션 클래스가 구현해야 하는 메서드를 포함하고 있다.

* boolean add(E e) : 해당 컬렉션에 전달된 요소를 추가
* boolean remove(Object o) : 해당 컬렉션에서 전달된 객체를 제거
* void clear() : 해당 컬렉션의 모든 요소를 제거
* boolean contains(Object o) : 해당 컬렉션이 전달된 객체를 포함하고 있는지
* boolean equals(Object o) : 해당 컬렉션과 전달된 객체가 같은지
* boolean isEmpty() : 해당 컬렉션의 반복자(iterator)를 반환
* int size() : 해당 컬렉션의 요소의 총개수를 반환
* Object [] toArray() : 해당 컬렉션의 모든 요소를 Object 타입의 배열로 반환

<br/>

### <u>컬렉션 클래스(Collection Class)</u>

컬렉션 프레임워크는 컬렉션 인터페이스에 대한 구현 클래스를 제공한다. 

* **일반적으로 쓰이는 클래스** : ArrayList, LinkedList, HasSet, TreeStet, PriorityQueue, ArrayDeque, HashMap, TreeMap, LinkedHashMap
* **Concurrent 클래스** : CopyOnWriteArrayList, ConcurrentHashMap, CopyOnWriteArraySet
* **Legacy 클래스** : Vector, Stack, Dictionary, Hashtable, Properties
* **Abstract 클래스** : AbstractList, AbstractSequenctailList, AbstractSet, AbstractQueue

#### 특징

|    컬렉션 클래스     | 순서 | 랜덤 액세스 | 키 - 값 | 중복 요소 | 널 요소 | 스레드 안전 |
| :------------------: | :--: | :---------: | :-----: | :-------: | :-----: | :---------: |
|      ArrayList       |  O   |      O      |         |     O     |    O    |             |
|      LinkedList      |  O   |             |         |     O     |    O    |             |
|       HashSet        |      |             |         |           |    O    |             |
|       TreeSet        |  O   |             |         |           |         |             |
|       Hashmap        |      |      O      |    O    |           |    O    |             |
|       Treemap        |  O   |      O      |    O    |           |         |             |
| CopyOnWriteArrayList |  O   |      O      |         |     O     |    O    |      O      |
| CopyOnWriteArraySet  |      |             |         |           |    O    |      O      |
|  ConcurrentHashMap   |      |      O      |    O    |           |         |      O      |



<br/>

### <u>컬렉션 알고리즘(Collection Algorithm)</u>

Collection 클래스는 모든 컬렉션의 알고리즘을 담당한다. 유틸리티 클래스로, static 메서드로 구성되어 있고 컬렉션들을 컨트롤하는 데 사용된다. Collections 클래스는 정렬, 셔플링, 이진 검색, 뒤집기 등의 메소드를 가지고 있다. **주의할 점은 자바의 Collection은 인터페이스며, Collections는 클래스라는 점이다.**

* **정렬** : 정렬 알고리즘은 요소가 오름차순이 되도록 리스트를 재정렬한다.
* **셔플링** : 셔플링 알고리즘은 랜덤으로 목록을 재정렬한다. 이 알고리즘은 우연한 게임을 구현할 때 유용하다.
* **탐색** : 이진 검색 알고리즘은 정렬된 목록에서 지정된 요소를 검색한다. 

<br/>

### <u>컬렉션 프레임워크의 모범 사례</u>

* 크기(size)가 고정되어 있다면 ArrayList보다 **Array**를 사용하라.
* 맵에 삽입된 순서대로 iterate를 하고 싶으면 **TreeMap**을 사용하는 것이 좋다. 
* 중복을 허용하고 싶지 않으면 **Set**을 사용하면 된다.
* 몇몇 컬렉션 클래스들을 초기 용량을 지정할 수 있다. 만약 저장할 요소들의 사이즈를 알 경우에 **초기 용량**을 지정함으로써 rehashing이나 resizing이 일어나는 것을 회피할 수 있다.
* 코드를 작성할 때, 구현 클래스가 아닌 **인터페이스**를 기반으로 작성해야 나중에 구현체를 변경할 때 코드를 재작성하는 수고를 줄일 수 있다. 
* 런타임에 발생할 수 있는 ClassCastException을 회피하려면 항상 **제네릭(Generics)을** 사용해서 type-safety 한 상태를 유지하라.
* 맵에 키를 사용할 때 JDK에서 제공하는 **immutable** 클래스를 사용하여 사용자 클래스에서 hashCode()와 equals() 구현할 필요가 없게 하라
* 읽기 전용 및 동기화, 빈 컬렉션 등을 만들 때는 자신만의 구현으로 생성하지 말고 Collections에서 제공하는 **유틸리티 클래스**를 사용하라. 이는 코드 재사용성을 높여주고 안정적이며 유지보수 비용을 줄여 준다.

<br/>

<br/>

<br/>

### REFERENCE

* [Java 컬렉션 정리1](https://gangnam-americano.tistory.com/41)
* [Java 컬렉션 정리2](https://www.crocus.co.kr/1553)
* [Java 컬렉션 정리3](https://gbsb.tistory.com/247#java-collections-algorithms)
* [Java 컬렉션 정리4](https://shlee0882.tistory.com/97)
* [상호운용성](https://ko.wikipedia.org/wiki/%EC%83%81%ED%98%B8%EC%9A%B4%EC%9A%A9%EC%84%B1)

