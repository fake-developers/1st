## Collection Framework[HashSet, TreeSet]

<br/>

### <u>Set 컬렉션</u>

* 순서가 존재하지 않는 비선형적인 자료구조를 갖는다.
  * 인덱스로 객체를 검색해서 가져오는 get()이 존재하지 않는다.
  * 대신 전체 객체를 대상으로 한번씩 반복해서 가져오는 반복자 iterator를 제공한다.
* 저장 순서가 유지되지 않는다.
* 중복을 허용하지 않는다.
  * 객체를 중복해서 저장할 수 없어서 중복 데이터 제거 수단으로 사용된다.
* Set이라는 이름처럼 수학에서 말하는 '집합'의 특성을 가지고 있다.
* 하나의 null만 저장할 수 있다.
* Set 인터페이스는 단독으로 객체를 만들 수 없다.
  * 하위 클래스인 HashSet, TreeSet등을 통해 다운캐스팅하여 만들어야 한다.

<br/>

#### 주요메소드

| 메소드                     | 설명                                                         |
| -------------------------- | ------------------------------------------------------------ |
| boolean add(E e)           | 주어진 객체를 저장 후 성공적이면 true를 중복 객체면 false를 리턴합니다. |
| boolean contains(Object o) | 주어진 객체가 저장되어있는지 여부를 리턴합니다.              |
| Iterator<E> iterator()     | 저장된 객체를 한번씩 가져오는 반복자를 리턴합니다.           |
| isEmpty()                  | 컬렉션이 비어있는지 조사합니다.                              |
| int Size()                 | 저장되어 있는 전체 객체수를 리턴합니다.                      |
| void clear()               | 저장된 모든 객체를 삭제합니다.                               |
| boolean remove(Object o)   | 주어진 객체를 삭제합니다.                                    |



### <u>HashSet</u>

Set 인터페이스의 구현 클래스이다. Set의 성질을 그대로 상속받는다.

>  **HashSet<E> 객체명 = new HashSet<E>();**

* 정렬을 해주지 않는다.

<br/>

#### 예제

~~~~java
import java.util.HashSet;
import java.util.Set;

public class SetCollectionFeature {
    public static void main(String[] args){
        Set<String> set = new HashSet<>();
        set.add("Toy"); // 1
        set.add("Box"); // 2
        set.add("Robot"); // 3
        set.add("Box"); // 4

        System.out.println(set);
    }
}

//결과
//[Box, Robot, Toy]
~~~~

<br/>

### <u>TreeSet</u>

이진 트리 구조를 기반으로 한 `Set<E>` 계열의 컬렉션

>  **TreeSet<E> 객체명 = new TreeSet<E>();**

* 자동 정렬을 해준다

<br/>

#### 예제

~~~~java
import java.util.TreeSet;

public class SortedTreeSet {
    public static void main(String[] args){
        TreeSet<Integer> tree = new TreeSet<>();
        tree.add(3); tree.add(1);
        tree.add(2); tree.add(4);

        System.out.println(tree);
    }
}

//결과
//[1, 2, 3, 4]
~~~~

<br/>



### <u>HashSet과 TreeSet의 성능 비교</u>

* **데이터의 추가와 삭제**

  HashSet > TreeSet

* **검색과 정렬**

  HashSet < TreeSet

<br/>

### REFERENCE

* [HashSet, TreeSet(1)](https://github.com/fake-developers/1st/blob/JYJ-06/JYJ/HashSetAndTreeSet.md)
* [HashSet, TreeSet(2)](https://github.com/fake-developers/1st/blob/KJY-06/KJY/%5BJAVA%5D%20%EC%BB%AC%EB%A0%89%EC%85%98%20%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%20-%20Set%20%EC%BB%AC%EB%A0%89%EC%85%98.md)
* [HashSet](https://coding-factory.tistory.com/554)
* [TreeSet](https://coding-factory.tistory.com/555?category=758267)
* [Collection](https://coding-factory.tistory.com/550)

