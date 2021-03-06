

# Set Collection Class

- Set 인터페이스르 구현한 클래스

  - 데이터의 저장 순서를 유지 하지 않음

  - 데이터의 중복 저장을 허용하지 않음

    - 단, 동일 데이터에 대한 기준은 프로그래머가 정의

    :bulb:

- 인덱스로 저장 순서를 유지하지 않는다.

- 하나의 Null만 존재한다.

- 주요 메서드

  | **기능**      | **메소드**                                                   | **설명**                                                     |
  | ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | **객체 추가** | - boolean add(E e)                                           | 주어진 객체를 저장 객체가 성공적으로 저장되면 true 리턴 중복 객체면 false 리턴 |
  | **객체 검색** | - boolean contains(Object o)<br>- isEmpty()<br>- Iterator\<E> iterator()<br>- int size()<br>- Object toArray() | - 주어진 객체가 저장되어 있는지 여부 반환 - boolean containsAll(Collection<?> c)<br>- 컬렉션이 비어 있는지 조사<br>- 저장된 객체를 한 번씩 가져오는 반복자 리턴<br>- 저장되어 있는 전체 객체 수 리턴<br>- 저장된 객체들을 객체 배열의 형태로 반환 |
  | **객체 삭제** | - void clear()<br>- boolean remove(Object o)                 | - 저장된 모든 객체를 삭제<br>- 주어진 객체를 삭제/boolean removeAll(Collection<?> c) |

- 대표적인 Set 컬렉션 클래스

  1. HashSet\<E>
  2. TreeSet\<E>

<BR>

## HashSet\<E>

- Set 컬렉션 클래스에서 가장 많이 사용되는 클래스 중 하나
- JDK 1.2 부터 제공된 HashSet 클래스는*해쉬 알고리즘(hash algorithm)*을 사용하여 검색 속도가 매우 빠름
- Set 인터페이스를 구현하므로, 요소를 순서에 상관없이 저장하고 중복된 값은 저장하지 않는다.
  - 만약 요소의 순서를 유지해야한다면, JDK 1.4부터 제공하는 LinkedHashSet 클래스를 사용한다.

---------

**<참조>**

- https://minhamina.tistory.com/24
- https://butter-shower.tistory.com/89
- http://www.tcpschool.com/java/java_collectionFramework_set
- https://postitforhooney.tistory.com/entry/JavaCollection-Java-Collection-Framework%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4%EB%A5%BC-%ED%86%B5%ED%95%B4-Data-Structure-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0

