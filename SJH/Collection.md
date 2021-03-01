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

---------

**<참조>**

- [[Java] Collection Framework1 - List(ArrayList / Vector / LinkedList)](https://minhamina.tistory.com/14)

- [자바 컬렉션 프레임워크(Java Collection Framework) 정리](https://gbsb.tistory.com/247)

- [[JAVA] Java 컬렉션(Collection) 정리](https://gangnam-americano.tistory.com/41)

