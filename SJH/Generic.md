# 제네릭(Generic)

<br>

### 제네릭이란?

- 클래스 내부에서 사용할 데이터 **타입을 클래스 외부에서 지정**하는 기법

  - 데이터 타입을 나중에 확정하는 기법

    - 클래스나 메소드를 선언할 때가 아닌 사용할 때 확정한다.
    - 즉, 인스턴스를 생성할 대나 메소드를 호출할 때 정한다는 의미이다.

    <img src="https://camo.githubusercontent.com/97cad32eea4131f385f2b44e6da3a8de39f614d29c4e5553cd258032ef8444b9/68747470733a2f2f73332e61702d6e6f727468656173742d322e616d617a6f6e6177732e636f6d2f6f70656e7475746f7269616c732d757365722d66696c652f6d6f64756c652f3531362f323133362e706e67">

- 제네릭 **선언**은 **클래스<사용할 타입>**으로 한다.

  ~~~
  public class 클래스명<T> {...}
  public interface 인터페이스명<T> {...}

- #### 제네릭의 장점

  - Object를 사용할 때와 달리 객체의 타입을 컴파일 타임에 체크할 수 있기 때문에 **타입 안정성**을 가진다.
    - 타입 안정성
      - 의도하지 않은 타입의 객체가 저장되는 것을 막는다.
      - 저장된 객체를 꺼내올 때 다른 타입으로 잘못 형변환하여 발생할 수 있는 오류를 줄일다.
  - **코드가 간결**해진다.

- #### 제네릭을 사용해야 하는 이유

  - 잘못된 타입이 사용될 수 있는 문제를 컴파일 과정에서 제거할 수 있기 때문이다.

  - 타입을 국한하기 때문에 요소를 찾아올 때 타입 변환을 할 필요가 없어 프로그램 성능이 향상되는 효과를 얻을 수 있다.

    ```
    //제네릭을 사용하지 않을경우
    ArrayList list = new ArrayList(); 
    list.add("test");
    String temp = (String) list.get(0); //타입변환이 필요함
            
    //제네릭을 사용할 경우        
    ArrayList<String> list2 = new ArrayList(); 
    list2.add("test");
    temp = list2.get(0); //타입변환이 필요없음
    ```

- #### 자주 사용하는 타입 인자

   | 타입인자 | 설명    |
   | -------- | ------- |
   | < T >    | Type    |
   | < E >    | Element |
   | < K >    | Key     |
   | < N >    | Number  |
   | < V >    | Value   |
   | < R >    | Result  |

<br>

-----------

*제네릭은 **클래스와 메소드에서 사용**할 수 있다.*

--------------------------

<br>

### 제네릭 클래스

- 제네릭 타입을 선언한 클래스

- 클래스<사용할 타입>

  ```java
  public class Box<T> {
      
      private T item;
  
      public T getItem() {
          return item;
      }
  
      public void setItem(T item) {
          this.item = item;
      }
  ```

- 멀티 타입 파라미터 : ,(콤마)로 구분해서 여러 개를 선언 가능

  ~~~java
  public class Box<M, I> {
  
      private M material;
      private I item;
  
      public M getMaterial() {
          return material;
      }
  
      public void setMaterial(M material) {
          this.material = material;
      }
  
      public I getItem() {
          return item;
      }
  
      public void setItem(I item) {
          this.item = item;
      }
  }
  ~~~

- 제네릭 클래스 사용 방법

  ```java
  Box<Paper, String> box = new Box<Paper, String>();
  Box<Paper, String> box = new Box<>();   // JDK1.7부터 생략 가능
  Box box = new Box();    // Object로 간주
  ```

  - JDK1.5부터 도입됨
  - JDK1.7부터 생성자의 <>에 타입을 생략할 수 있다.
  - 하위 호환을 위해 타입을 지정하지 않고도 객체를 생성할 수 있다. -> 이경우 타입 : Object

- 주의할 점

  - 참조변수에서 지정한 타입과 생성자에서 지정한 타입은 반드시 일치해야 한다.
  - 두 타입이 서로 상속 관계가 있다고 해도, 타입이 다르면 컴파일 에러가 발생한다.
    - Cardboard 클래스가 Paper의 자식 클래스라고 해도, Box box\<Paper> = new Box\<Cardboard>();는 불가능

<br>

### 제네릭 메소드

- 제네릭 타입을 선언한 메소드

- 클래스의 제네릭 타입이 전역 변수처럼 사용된다면, 메소드의 제네릭 타입은 해당 메소드 안에서만 사용할 수 있는 **지역성**을 가짐

- 제네릭 클래스가 아닌 일반 클래스 내부에도 제네릭 메서드를 정의 할 수 있다.

  - 클래스에 지정된 타입 파라미터와 제네릭 메서드에 정의된 타입 파라미터는 상관이 없다는 것
  - 즉, 제네릭 클래스에 \<T>를 사용하고, 같은 클래스의 제네릭 메서드에도 \<T>로 같은 이름을 가진 타입 파라미터를 사용하더라도 둘은 전혀 상관 없다.

- 메서드에서 제네릭 타입 선언

  ```java
  public class CoffeeMachine {
  
      public <T> Coffee makeCoffee(T capsule) {
  
          return new Coffee(capsule);
      }
  }
  ```

  - 접근 제한자와 반환 타입 사이에 선언

- 제네릭 메소드 사용방법

  ```java
  CoffeeMachine coffeeMachine = new CoffeeMachine();
  Colombian capsule = new Colombian();
  coffeeMachine.<Colombian>makeCoffee(capsule); //메서드 앞에 지정
  coffeeMachine.makeCoffee(capsule);  // 타입 추정 가능하므로 생략 가능
  ```

  - 제네릭 메소드를 호출할 대는 메소드 명 앞에 \< >로 타입을 지정해줘야 하지만, 컴파일러가 타입을 추정할 수 있는 경우엔 생략 가능
  - 대부분의 경우 컴파일러가 타입을 추정할 수 있다.

<br>

### 제한된 타입 파라미터

- 제네릭의 상위 타입, 하위 타입을 구체적으로 제한하고 싶을 경우

- 메서드, 인터페이스, 클래스에서 동일하게 사용 가능

- < T extends 상위타입 >, <T super 하위타입> 으로 제한할 수 있음

  ```java
  public class BeforeTest  {
      public < T extends Number, D extends Map > void show( D map, T key ) {
          System.out.println(map.containsKey(key));
      }
  }
  ```

  - 내부에서 사용할 T 객체가 꼭 Number 클래스의 하위 타입이어야 할 때 or 상위 인터페이스의 구현체이어야 할 때 사용 가능
  - 그래야 메소드 안에서 필요한 인터페스의 메소드 혹은 클래스의 메소드를 사용할 수 있음

<br>

### 와일드 카드

- 코드에서 **?**를 일반적으로 와일드카드라고 부른다.

- 사용하는 경우

  <img src="https://camo.githubusercontent.com/ecfa4e0cc36f77c39d51a3cae9daa54ae7ea8121a563604dbe0e64d424393024/68747470733a2f2f686f6e6261627a6f6e652e636f6d2f6173736574732f696d616765732f706f73742f6a6176612f67656e657269632e706e67" height=280> 

  - < ? >
    - 모든 클래스나 인터페이스가 올 수 있음. 즉 제한없음
    - A ~ E 모두 올 수 있음
  - < ? extends 상위타입 >
    - 상위타입 이하로만 올 수 있음
    - < ? extends D > => D, E 가능
  - < ? super 하위타입 >
    - 하위타입 이상으로만 올 수 있음
    - < ? super D > => D, A 가능

```java
public class Calcu {
    public void printList(List<?> list) {
       for (Object obj : list) {
    	   System.out.println(obj + " ");  
       }
    }

    public int sum(List<? extends Number> list) {
      int sum = 0;
      for (Number i : list) {
    	  sum += i.doubleValue();  
      }
      return sum;
    }

   public List<? super Integer> addList(List<? super Integer> list) {
      for (int i = 1; i < 5; i++) {
    	 list.add(i); 
      }
      return list;
    }
}
```

<br>

----------

<br>

--------

**<참조>**

- [[Java\] 제네릭(Generic) 사용법 & 예제 총정리](https://coding-factory.tistory.com/573)
- [java 제네릭(Generic) 이란??](https://2dubbing.tistory.com/17)
- [JAVA 제네릭이란(Generic)?](https://honbabzone.com/java/java-generic/)
- [JAVA 제네릭(Generics) 클래스와 메소드](https://atoz-develop.tistory.com/entry/JAVA-제네릭Generics-클래스와-메소드)
- [제네릭](https://opentutorials.org/module/516/6237)
