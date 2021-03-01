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
  | 기타      | - Iterator\<E> iterator()<br>- boolean equals(Object o)<br>- Object[] toArray() | - 해당 리스트의 반복자(iterator)를 반환<br>- 해당 리스트와 전달된 객체가 같은지 확인<br>- 해당 리스트의 모든 요소를 Object 타입의 배열로 반환 |

- 대표적인 List 컬렉션 클래스

  1. ArrayList\<E>
2. LinkedList\<E>
  3. Vector\<E>
4. Stack\<E>

<br>

## ArrayList

- 저장 용량을 초과한 객체들이 들어오면 자동적으로 저장용량이 늘어나는 구조

- JDK 1.2 부터 제공된내부적으로 배열을 이용하여 객체 저장

  - 인덱스를 이용해 배열 요소에 빠르게 접근가능
  - 하지만 크기를 늘리기 위해서 새로운 배열을 생성하고 기존의 요소들을 옮겨야하는 복잡한 과정

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
  //실행결과 40 20 30 10
  
   
  // remove() 메소드를 이용한 요소의 제거
  arrList.remove(1);
   
  
  // Enhanced for 문과 get() 메소드를 이용한 요소의 출력
  for (int e : arrList) {
      System.out.print(e + " ");
  }
  //실행결과 40 30 10
  
   
  
  // Collections.sort() 메소드를 이용한 요소의 정렬
  Collections.sort(arrList);
  
   
  
  // iterator() 메소드와 get() 메소드를 이용한 요소의 출력
  Iterator<Integer> iter = arrList.iterator();
  
  while (iter.hasNext()) {
      System.out.print(iter.next() + " ");
  }
  //실행결과 10 30 40 
   
  // set() 메소드를 이용한 요소의 변경
  arrList.set(0, 20);
  
  
  for (int e : arrList) {
      System.out.print(e + " ");
  }
  //실행결과 20 30 40
  
  // size() 메소드를 이용한 요소의 총 개수
  System.out.println("리스트의 크기 : " + arrList.size());
  //실행결과 리스트의 크기 : 3
  ~~~
  
  - Collections 클래스는 JDK 1.2부터 제공되는 컬렉션에서 동작하거나 컬렉션을 반환하는 클래스 메소드 만으로 구성된 클래스이다.
  - Collections는 클래스, Collection은 인터페이스임을 주의해야한다.

## LinkedList

- ArrayList가 배열을 이용하여 발생하는 단점을 극복하지 위해 고안

  - ArrayList와 비슷하지만, 선입 선출인 **Queue**와 양쪽 끝에서의 처리를 하는 **Deque**의 속성과 메소드를 가지고 있다.

- 동기화를 보장하지 않으며, 동기화가 필요할 때는 `Collections.synchronizeList()`메서드를 통해 동기화가 보장되는 List를 반환받아 사용한다.

- JDK 1.2 부터 제공된 LinkedList는 *연결리스트*를 이용하여 요소 저장

  - 인접 참조를 링크해서 체인처럼 관리 특정 인덱스의 객체를 제거하면 앞뒤 링크만 변경된다.

  - 즉, 삽입/삭제가 빈번할 때 사용하는 적이 효율적

    \* *연결리스트*

    <img src="https://user-images.githubusercontent.com/58902042/109516034-18fbf200-7aeb-11eb-9ba9-1e25553c341f.png" height=160> 

    - 단일 연결 리스트는 요소의 저장과 삭제 작업이 다음 요소를 가리키는 참조만 변경하면 되므로 아주 빠른 처리 가능
    - but, 현재 요소에서 이전 요소로 접근하기 매우 어렵다.

    <img src="https://user-images.githubusercontent.com/58902042/109516397-77c16b80-7aeb-11eb-993d-539db8682e71.png" height=160> 

    - 이전 요소를 가리키는 참조도 가진다.
    - LinkedList 클래스도 위와 같은 이중 연결리스트를 내부적으로 구현한 것이다.

- ex_)

  ~~~java
  LinkedList<String> lnkList = new LinkedList<String>();
  
  
  // add() 메소드를 이용한 요소의 저장
  lnkList.add("넷");
  lnkList.add("둘");
  lnkList.add("셋");
  lnkList.add("하나");
  
   
  // for 문과 get() 메소드를 이용한 요소의 출력
  for (int i = 0; i < lnkList.size(); i++) {
     System.out.print(lnkList.get(i) + " ");
  }
  //실행결과 넷 둘 셋 하나
  
   
  // remove() 메소드를 이용한 요소의 제거
  lnkList.remove(1);
   
  
  // Enhanced for 문과 get() 메소드를 이용한 요소의 출력
  for (String e : lnkList) {
      System.out.print(e + " ");
  }
  //실행결과 넷 셋 하나
  
  
  // set() 메소드를 이용한 요소의 변경
  lnkList.set(2, "둘");
   
  for (String e : lnkList) {
      System.out.print(e + " ");
  }
  //실행결과 넷 셋 둘
  
  
  // size() 메소드를 이용한 요소의 총 개수
  System.out.println("리스트의 크기 : " + lnkList.size());
  //실행결과 리스트의 크기 : 3
  ~~~

  - 위의 예제를 살펴보면 ArrayList와 LinkedList의 메서드가 거의 같은 것을 볼 수 있따.
  - 이처럼 **ArrayList와 LinkedList의 차이**는 사용 방법이 아닌, **내부적으로 요소를 저장하는 방법에 있다.**

## Vector

- JDK 1.0부터 상요해온 ArrayList 클래스와 같은 동작을 수행하는 클래스
  - ArrayList와 같은 구조를 가지고 있으나 동기화된 메서드로 구성되어 있어 멀티 쓰레딩 구조에 안정적이다.
- 과거에 대용량 처리를 위해 사용했으나, 비교적 성능이 좋지 않고 무거워 잘 쓰지 않는다.
  - 현재에는 기존 코드와의 호환성을 위해서만 남아있다.

## Stack

- List 컬렉션 클래스의 Vector 클래스를 상속받아, 전형적인 스택 메모리 구조의 클래스를 제공

- LIFO(후입선출)의 자료구조

  -  가장 나중에 저장된 데이터가 가장 먼저 인출된다.

  <img src="https://user-images.githubusercontent.com/58902042/109519767-e48a3500-7aee-11eb-997d-1035e91316a7.png" height=370> 

- Stack 클래스는 스택 메모리 구조를 표현하기 위해, Vector 클래스의 메소드 5개를 상속받아 사용한다.

  |        메소드        |                             설명                             |
  | :------------------: | :----------------------------------------------------------: |
  |   boolean empty()    | 해당 스택이 비어 있으면 true를, 비어 있지 않으면 false를 반환 |
  |       E peek()       | 해당 스택의 제일 상단에 있는(제일 마지막으로 저장된) 요소 반환 |
  |       E pop()        | 해당 스택의 제일 상단에 있는(제일 마지막으로 저장된) 요소 반환<br> 해당 요소를 스택에서 제거함. |
  |    E push(E item)    |          해당 스택의 제일 상단에 전달된 요소를 삽입          |
  | int search(Object o) | 해당 스택에서 전달된 객체가 존재하는 위치의 인덱스를 반환<br>이때 인덱스는 제일 상단에 있는(제일 마지막으로 저장된) 요소의 위치부터 0이 아닌 1부터 시작 |

- 더 복잡하고 빠른 스택을 구현하고 싶다면 Deque 인터페이스를 구현한 ArrayDeque 클래스를 사용한다.

  - 단, ArrayDeque 클래스는 Stack 클래스와 달리 search() 메서드를 지원하지 않는다.

  ~~~java
  Deque<Integer> st = new ArrayDeque<Integer>();
  ~~~

- ex_)

  ~~~java
  Stack<Integer> st = new Stack<Integer>(); // 스택의 생성
  //Deque<Integer> st = new ArrayDeque<Integer>();
  
   
  
  // push() 메소드를 이용한 요소의 저장
  st.push(4);
  st.push(2);
  st.push(3);
  st.push(1);
  
   
  // peek() 메소드를 이용한 요소의 반환
  System.out.println(st.peek());
  //실행결과 1
  
  System.out.println(st);
  //실행결과 [4,2,3,1]
  
   
  
  // pop() 메소드를 이용한 요소의 반환 및 제거
  System.out.println(st.pop());
  //실행결과 1
  
  System.out.println(st);
  //실행결과 [4,2,3]
  
   
  
  // search() 메소드를 이용한 요소의 위치 검색
  System.out.println(st.search(4));
  //실행결과 3
  System.out.println(st.search(3));
  //실행결과 1
  ~~~

  

<br>

-------

**<참조>**

- [Java - Collection Framework](http://hochulshin.com/java-collection-framework/)

- <http://www.tcpschool.com/java/java_collectionFramework_list>

- [[Java/Collection] Java Collection Framework에 대한 이해를 통해 Data Structure 이해하기.](https://postitforhooney.tistory.com/entry/JavaCollection-Java-Collection-Framework%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4%EB%A5%BC-%ED%86%B5%ED%95%B4-Data-Structure-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)

