# List Collection Class

- List Interface를 구현한 클래스

  - 순서가 있는 데이터의 집합
  - 데이터의 중복 허용

- 객체를 인덱스로 관리하기 때문에 객체를 저장하면 자동 인덱스가 부여되고 인덱스로 객체를 검색, 삭제할 수 있는 기능을 제공한다.

- List는 객체 자체를 저장하는 것이 아니라, 해당 인덱스에 객체의 주소를 참조하여 저장

- 주요 메소드

  | 기능      | 메소드                                                       | 설명                                                         |
  | --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | 객체 추가 | - boolean add(E element)<BR>- void add(int index, E element)<BR>- E set( int index, E element) | - 해당 주어진 객체를 맨 끝 인덱스에 추가<BR>- 해당 인덱스에 객체 추가<BR>- 해당 인덱스에 주어진 객체로 변경 |
  | 객체 검색 | -  boolean contains(Object object)<br>- E get(int index)<br>- boolean isEmpty()<br>- int size() | - 주어진 객체가 저장되어 있는지 여부 확인<br>- 해당 인덱스에 저장된 객체 리턴<br>- 켈렉션이 비어 있는지 조사<br>- 저장되어 있는 전체 객체 수를 리턴 |
  | 객체 삭제 | - void clear()<br>- E remove(int index)<br>- boolean remove(Object o) | - 저장된 모든 객체를 삭제<br>- 해당 인덱스 객체 삭제<br>- 주어진 객체를 삭제 |
  | 기타      | - Iterator\<E> iterator()<br>- boolean equals(Object o)      | - 해당 리스트의 반복자(iterator)를 반환<br>- 해당 리스트와 전달된 객체가 같은지 확인 |

- 대표적인 List 컬렉션 클래스

  1. ArrayList\<E>
2. LinkedList\<E>
  3. Vector\<E>
4. Stack\<E>

<br>

## ArrayList

- 저장 용량을 초과한 객체들이 들어오면 자동적으로 저장용량이 늘어나는 구조

- JDK 1.2 부터 제공된내부적으로 배열을 이용하여 객체 저장

- 동기화를 보장하지 않으며, 동기화가 필요할 때는 `Collections.synchronizeList()`메서드를 통해 동기화가 보장되는 List를 반환받아 사용한다.

- ex_)

  ~~~java
  ArrayList<Integer> arrList = new ArrayList<Integer>();
  
   
  // add() 메소드를 이용한 요소의 저장
  arrList.add(40);
  arrList.add(20);
  arrList.add(30);
  arrList.add(10);
  
  
  // for 문과 get() 메소드를 이용한 요소의 출력
  for (int i = 0; i < arrList.size(); i++) {
      System.out.print(arrList.get(i) + " ");
  }
  
   
  // remove() 메소드를 이용한 요소의 제거
  arrList.remove(1);
  
   
  
  // Enhanced for 문과 get() 메소드를 이용한 요소의 출력
  for (int e : arrList) {
      System.out.print(e + " ");
  }
  
   
  
  // Collections.sort() 메소드를 이용한 요소의 정렬
  Collections.sort(arrList);
  
   
  
  // iterator() 메소드와 get() 메소드를 이용한 요소의 출력
  Iterator<Integer> iter = arrList.iterator();
  
  while (iter.hasNext()) {
      System.out.print(iter.next() + " ");
  }
  
   
  
  // set() 메소드를 이용한 요소의 변경
  
  arrList.set(0, 20);
  
   
  
  for (int e : arrList) {
  
      System.out.print(e + " ");
  
  }
  
   
  
  // size() 메소드를 이용한 요소의 총 개수
  
  System.out.println("리스트의 크기 : " + arrList.size());
  ~~~

  

## LinkedList

- ArrayList가 배열을 이용하여 발생하는 단점을 극복하지 위해 고안

  - ArrayList와 비슷하지만, 선입 선출인 **Queue**와 양쪽 끝에서의 처리를 하는 **Deque**의 속성과 메소드를 가지고 있다.

- JDK 1.2 부터 제공된 LinkedList는 연결리스트를 이용하여 요소 저장

  - 인접 참조를 링크해서 체인처럼 관리 특정 인덱스의 객체를 제거하면 앞뒤 링크만 변경된다.

  - 즉, 삽입/삭제가 빈번할 때 사용하는 적이 효율적

- 동기화를 보장하지 않으며, 동기화가 필요할 때는 `Collections.synchronizeList()`메서드를 통해 동기화가 보장되는 List를 반환받아 사용한다.

## Vector

- ArrayList와 같은 구조를 가지고 있으나 동기화된 메서드로 구성되어 있어 멀티 쓰레딩 구조에 안정적이다.
- 과거에 대용량 처리를 위해 사용했으나, 비교적 성능이 좋지 않고 무거워 잘 쓰지 않는다.

## Stack

- List 컬렉션 클래스의 Vector 클래스를 상속받아, 전형적인 스택 메모리 구조의 클래스를 제공
- LIFO(후입선출)의 자료구조, 가장 나중에 저장된 데이터가 가장 먼저 인출된다.

<br>

-------

**<참조>**

- [Java - Collection Framework](http://hochulshin.com/java-collection-framework/)

- <http://www.tcpschool.com/java/java_collectionFramework_list>

https://postitforhooney.tistory.com/entry/JavaCollection-Java-Collection-Framework%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4%EB%A5%BC-%ED%86%B5%ED%95%B4-Data-Structure-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0

