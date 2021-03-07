# Set Collection Class

:bulb:***여기에 나오는 설명의 전반적인 내용을 알기위해서는 Collection인터페이스에 대해 먼저 공부하고 오는 것을 권장 합니다. [여기 ](./Collection.md) 클릭***

- Set 인터페이스를 구현한 클래스
- **데이터의 저장 순서를 유지 하지 않음**
  
- **데이터의 중복 저장을 허용하지 않음**
  - 단, 동일 데이터에 대한 기준은 프로그래머가 정의


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

- JDK 1.2 부터 제공된 HashSet 클래스는*해시 알고리즘(hash algorithm)*을 사용하여 검색 속도가 매우 빠름

- Set 인터페이스를 구현하므로, 요소를 순서에 상관없이 저장하고 중복된 값은 저장하지 않는다.

  - 만약 요소의 순서를 유지해야한다면, JDK 1.4부터 제공하는 *LinkedHashSet* 클래스를 사용한다.
  - LinkedHashSet 
    - 해시 테이블과 연결리스트가 결합된 형태
    - 즉, 중복된 데이터 저장 불가
    - 입력된 순서로 데이터 관리

- ex_) 첫번째 예시

  ~~~java
  public static void main(String[] args){
    HashSet<String> hSet = new HashSet<String>();
    hSet.add("First");
    hSet.add("Second");
    hSet.add("Third");
    hSet.add("First"); //동일한 값 넣어줌
   
    System.out.println("저장된 데이터 수 : " + hSet.size());
   
    Iterator<String> itr = hSet.iterator();
    while(itr.hasNext())
        System.out.println(itr.next());
   
  }
  //실행결과
  //3
  //Third
  //Second
  //First
  ~~~

  - Collection 인터페이스에서는 Iterator 인터페이스를 구현한 iterator() 메소드를 사용하여 각 요소에 접근하도록 한다. 더 자세한 내용이 알고싶다면 [여기](./Collection.md)를 클릭.

- ex_) 두번째 예시

  ~~~java
  import java.util.HashSet;
  
  class Num{
      private int num;
      public Num(int n) { num = n; } // 정수를 받아 num에 저장
  
      @Override
      public String toString(){
          // num 값을 String으로 형 변환
          return String.valueOf(num);
      }
  }
  
  public class HashSetEqualityOne {
      public static void main(String[] args){
          HashSet<Num> set = new HashSet<>();
          set.add(new Num(7799));
          set.add(new Num(9955));
          set.add(new Num(7799));
  
          System.out.println(set);
      }
  }
  //실행결과
  //[9955,7799,7799]
  ~~~

  - 7799 값을 지닌 두 인스턴스가 서로 다른 인스턴스로 간주되어 둘 다 저장이 되었다.
  - HashSet\<E> 이 판단하는 동일 인스턴스의 기준은, Object 클래스에 정의되어 있는 다음 두 메소드의 호출 결과를 근거로 하기 때문이다.
    - public boolean equals(Object obj)
    - public int hashCode()
  - 따라서, 이 두 인스턴스가 같은 인스턴스임을 보여야할 때에는 메소드 오버라이딩을 통해야한다.
    - 위에서 설명했던 *동일 데이터에 대한 기준을 프로그래머가 정한다*는 것의 의미

- #### 해시 알고리즘과 hashCode() 메서드

  - 해시 알고리즘(hash algorithm)이란 해시 함수(hash function)를 사용하여 데이터를 해시 테이블(hash table)에 저장하고, 다시 그것을 검색하는 알고리즘.

    <img src="https://user-images.githubusercontent.com/58902042/110230324-92646c00-7f53-11eb-97eb-c53c6af242e7.png" height=260> 

  - 자바에서 해시 알고리즘을 이용한 자료구조는 위의 그림과 같이 배열과 연결리스트로 구현된다.

  - ex_)

  - num % 3 을 이용하여 해쉬 알고리즘을 사용할 수 있다.

  - 3, 5, 7, 12, 25, 31 이라는 주어진 값들을 분류해보자. 하나의 집합을 구성한다고 가정할 때,

    - 나머지 연산의 결과에 따라 0인 값, 1인 값, 2인 값, 세 부류로 나뉠 수 있다.

  - 정수 5의 존재 여부를 확인하려면 나머지 연산을 진행한다.

    - 나머지 결과가 2이기 때문에 2인 값에 속한다.

  - 속하는 부류를 찾은 후에 선택된 부류 내에서 탐색을 진행하기 때문에 탐색 속도가 빠르다.

  - 위의 두 단계를 거쳐 동일한 인스턴스의 존재 여부를 확인하는 클래스가 HashSet<E> 이다.
    - 즉 탐색 과정은
      - 1단계 : Object 클래스에 정의된 hashCode 메소드의 반환 값을 기반으로 부류 결정
      - 2단계 : 선택된 부류 내에서 eqauls 메소드를 호출하여 동등 비교

  - Object 클래스에 정의되어 있는 hashCode와 equals 메소드는 다음과 같이 정의되어 있다.
    - 인스턴스가 다르면 Object 클래스의 hashCode 메소드는 다른 값을 반환한다.
    - 인스턴스가 다르면 Object 클래스의 equals 메소드는 false를 반환한다.
  - 참고로, Object 클래스의 hashCode 메소드는 인스턴스가 저장된 **주솟값**을 기반으로 반환 값이 만들어지도록 정의되어 있다.
    - 즉, Object 클래스의 hashCode와 equals는 저장하고 있는 값을 기준으로 동등 여부를 따지지 않는다.
    - 따라서, 위의 HashSet\<E> 두번째 예제에서 7799가 다른 인스턴스로 간주되었다.
    - 값을 기준으로 동등 여부를 따지려면 두 메소드를 오버라이딩 해야 한다.

  - HashSet\<E> 두번째 예시 수정 코드

    ~~~java
    import java.util.HashSet;
    
    class Num{
        private int num;
        public Num(int n) { num = n; } // 정수를 받아 num에 저장
    
        @Override
        public String toString(){
            return String.valueOf(num);
        }
    
        /* 추가된 코드 */
        @Override
        public int hashCode(){ // num 의 값이 같으면 부류도 같다.
            return num % 3;
        }
    
        @Override
        public boolean equals(Object obj){ // num의 값이 같으면 true를반환한다.
            if(num == ((Num)obj).num)
                return true;
            else
                return false;
        }
        
    }
    
    public class HashSetEqualityOne {
        public static void main(String[] args){
            HashSet<Num> set = new HashSet<>();
            set.add(new Num(7799));
            set.add(new Num(9955));
            set.add(new Num(7799));
    
            System.out.println(set);
        }
    }
    //실행결과 
    //[9955,7799]
    ~~~

    - 참고로 String 클래스는 문자열의 내용 비교가 이뤄지도록 hashCode와 equals를 적절히 오버라이딩 하고 있다.
    - 따라서 HashSet\<E> 인스턴스에는 동일한 문자열을 지니는 String 인스턴스가 둘 이상 저장되지 않는다.

<br>

## TreeSet\<E>

- **데이터가 정렬된 상태**로 저장되는 **이진 검색 트리(binary search tree)의 형태로 요소를 저장**

  - 이진 검색 트리는 데이터를 추가하거나 제거하는 등의 기본 동작 시간이 매우 빠르다.

  - 이진 트리를 기반으로하기 때문에 계층적 구조를 가지며 객체를 저장

  - 하나의 노드는 노드값인 value와 왼쪽 오른쪽 자식 노드를 참조하기 위한 두개의 변수로 구성된다.

    <img src="https://user-images.githubusercontent.com/58902042/110232145-6cdd5f80-7f5f-11eb-9c38-ff35387e96f6.png" height=180> 

- JDK 1.2부터 제공되는 TreeSet클래스는 NavigableSet 인터페이스를 기존의 이진 검색 트리의 성능을 향상 시킨 **레드-블랙 트리(Red-Black Tree)**로 구현한다.

- Set 인터페이스를 구현하므로, 요소를 순서에 상관없이 저장하고 중복된 값은 저장하지 않는다.

  - 순서에 상관없이 저장하지만, 정렬 시킨다.
  - 기본적으로는 오름차순으로 데이터를 정렬한다.
  - 정렬의 기준은 프로그래머가 직접 정의한다.

- ex_)

  ~~~java
  TreeSet<Integer> ts = new TreeSet<Integer>();
  
   
  // add() 메소드를 이용한 요소의 저장
  ts.add(30);
  ts.add(40);
  ts.add(20);
  ts.add(10);
  
  
  // Enhanced for 문과 get() 메소드를 이용한 요소의 출력
  for (int e : ts) {
      System.out.print(e + " ");
  }
   
  
  // remove() 메소드를 이용한 요소의 제거
  ts.remove(40);
  
   
  // iterator() 메소드를 이용한 요소의 출력
  Iterator<Integer> iter = ts.iterator();
  while (iter.hasNext()) {
      System.out.print(iter.next() + " ");
  }
  
   
  // size() 메소드를 이용한 요소의 총 개수
  System.out.println("이진 검색 트리의 크기 : " + ts.size());
  
  //실행결과
  //10 20 30 40 
  //10 20 30 
  //이진 검색 트리의 크기 : 3
  ~~~

  - 수의 경우에는 크고 작음의 기준이 명확하지만, String name, int age 가 동시에 존재하는 경우에는 이름 오름차순인지, 나이 오름차순인지에 대한 기준을 프로그래머가 결정해야 한다.
  - Comparable\<T>인터페이스를 오버라이딩하여 기준을 정한다.
    - 위에서 설명했던 *정렬에 대한 기준을 프로그래머가 정한다*는 것의 의미

- #### 정렬의 기준을 정하는 Comparable\<T> 인터페이스

  - TreeSet 인스턴스에 저장이 되려면 Comparable 인터페이스를 구현해야 함
  - Comparable 인터페이스의 유일한 메소드는 `int compareTo(T obj);`
  - compareTo 메소드는 다음의 기준으로 구현
    - 인자로 전달된 obj 크기가 작다면 양의 정수 반환
    - 인자로 전달된 obj 크기가 크다면 음의 정수 반환
    - 같다면 0 반환
    - 작다, 크다, 같다의 기준은 프로그래머가 결정

  - ex_)

    ~~~java
    class Person implements Comparable<Person> {
        String name;
        int age;
     
        public int compareTo(Person p) {
            if (age > p.age) return 1;
            else if (age < p.age) return -1;
            else return 0;
        }
    }
     
    public static void main(String[] args){
        TreeSet<Person> sTree = new TreeSet<Person>();
        sTree.add(new Person("Lee", 24);
        sTree.add(new Person("Kim", 29);
        sTree.add(new Person("Park", 21);
     
        Iterator<Person> itr = sTree.iterator();
        while(itr.hasNext())
            System.out.println(itr.Next());
    }
    //실행결과
    //[Park:21, Lee:24, Kim:29]
    ~~~

    

---------

**<참조>**

- [[Java] Collection Framework2 - Set(HashSet / LinkedHashSet / TreeSet)](https://minhamina.tistory.com/24)
- [[Java] 컬렉션 프레임워크 - List, Set, Queue, ArrayList, LinkedList, Iterator, Stack, Tree, Map](https://butter-shower.tistory.com/89)
- http://www.tcpschool.com/java/java_collectionFramework_set
- [[Java/Collection] Java Collection Framework에 대한 이해를 통해 Data Structure 이해하기.](https://postitforhooney.tistory.com/entry/JavaCollection-Java-Collection-Framework%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4%EB%A5%BC-%ED%86%B5%ED%95%B4-Data-Structure-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)

- https://github.com/fake-developers/1st/blob/main/JYJ/HashSetAndTreeSet.md

