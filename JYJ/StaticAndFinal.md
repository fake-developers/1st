# Static 과 Final 차이

:writing_hand: *Assembled by Yunju Jang*

<!--🤝*Contributors :  JiYoung-Kwon, Jeonghea Shin* -->

<hr>

### static

- <b>static 변수</b>

  - <code>static</code>으로 선언된 변수는 <b>메모리 공간에 하나만 존재하고, 어디에서나 접근이 가능한 변수</b>이다.
  - 어디서든 접근하려면 public으로 선언되어야 한다.
  - 클래스 내부에서는 얼마든지 직접 접근이 가능하다.
  - 클래스 외부에서 <b>인스턴스의 이름이나 클래스의 이름</b>을 통해서 접근할 수 있다.
  
  <br/>
  
- <b>static 변수의 초기화 시점</b>

  - static 변수는 인스턴스가 생성되기 이전에 별도의 메모리 공간에 할당되어 초기화까지 완료된다.
  - 초기화되는 시점은 JVM(Java Virtual Machine)에 의해 클래스가 메모리 공간에 올라가는 순간이다.

  <br/>

  <br/>

- <b>static 메소드</b>

  - <b>인스턴스를 생성하지 않아도 static 메소드를 호출</b>할 수 있다.
    - 객체를 생성할 필요 없는 메소드에 붙여 사용한다.
    - 인스턴스 변수에 접근하지 않는 경우에 메소드로 정의해 사용한다.
  - public static void main
    - main 메소드는 인스턴스의 생성과 관계없이 JVM에 의해 호출되므로 반드시 static으로 선언한다.

  <br/>

- <b>static 변수와 메소드를 사용하는 이유</b>

  - 동일한 타입의 객체들이 서로 <b>데이터 공유</b>가 필요한 상황에서 사용한다.

  <br/>

- <b>static 중첩 클래스 (내부 클래스)</b>

  - 최상위 클래스를 static으로 만들 수 없으나, 클래스를 static으로 만들 수는 있따.
  - 일반 클래스의 <b>내부 클래스를 static으로 선언하면 가능하다.</b>
  - 즉, <b>중첩 클래스에서만 static을 사용할 수 있다.</b>

  ``` java
  public class MyNestedClass{
      // static class
      public static class NestedStaticClass {
          public static void printStaticMsg() {
              System.out.println("NestedStaticClass");
          }
          
          public void printMsg(){
              System.out.println("NestedStaticClass");
          }
      }
      
      // inner class
      public class InnerClass {
          public void print(){
              System.out.println("InnerClass");
          }
      }
  }
  
  public static void main(String[] args){
      // static 클래스 (중첩 클래스)의 static 메소드 접근
      MyNestedClass.NestedStaticClass.printStaticMsg();
      
      // static 클래스(중첩 클래스)생성 후 해당 클래스의 일반 메소드 접근
    	MyNestedClass.NestedStaticClass nestedStaticClass = new MyNestedClass.NestedStaticClass();
    	nestedStaticClass.printMsg();
  
    	// 일반 클래스의 내부 클래스 생성 후 메소드 접근
    	MyNestedClass.InnerClass innerClass = new MyNestedClass().new InnerClass();
    	innerClass.print();
  } 
  // static 클래스 및 변수는 static 인 것만 접근이 가능하다.
  ```

  <br/>

<br/>

### final

- <b>final 변수</b>

  - 변수를 상수화 시킨다.
  - 즉, 한번 값이 결정된 변수의 값은 <b>변경이 불가능</b>하다.

  ``` java
  final int a;
  // final int a = 1; 상수 선언과 함께 값을 정의해도 된다.
  Scanner s = new Scanner(System.in);
  a = s.nextInt();
  // a = 10; 오류 (값을 변경할 수 없다.)
  System.out.println(a);
  ```

  

  <br/>

  <br/>

- <b>final 클래스</b>

  - 클래스를 final로 선언하면 이 클래스를 <b>상속하는 것을 허용하지 않는다</b>.
  - 대표적으로 String 클래스가 있다.
  
  ``` java
  final class Test{
      int test;
  }
  // class Main extends Test{} --> final class 는 상속할 수 없다.
  ```

  <br/>

  <br/>

- <b>final 메소드</b>

  - 메소드를 final로 선언하면 이 메소드의 <b>오버라이딩을 허용하지 않겠다</b>는 뜻이다.
  - 클래스는 상속이 가능하되, 해당 메소드는 오버라이딩이 불가능하다.

  ``` java
  class Test {
      public final void test2(){
          // 내용 정의
      }
  }
  
  public class Main extends Test{
      // public test2(){} compile error : 메소드는 오버라이딩 할 수 없음
  }
  ```

<br/>

<br/>

- <b>static final</b>

  - 클래스 내부 또는 외부에서 참조의 용도로만 선언된 변수는 static final로 선언한다.
  - 객체(인스턴스)가 아닌 클래스에 존재하는 단 하나의 상수이다.
    - 따라서, 선언과 동시에 초기화를 해주어야 한다.
  - 원주율, 산소의 질량 등 누구나 알고있는 변하지 않는 상수의 값을 static final로 설정하여 변경되지 않도록 한다.
  - ex) <code>static final double PI = 3.14;</code>

  ``` java
  public class Test {
      static final int a = 1; // 선언과 동시에 초기화
      public static void main(String[] args){
          System.out.println(a);
      }
  }
  ```

  

<br/>

- <b>final</b> vs <b>static final</b>
  - static final을 선언한 변수를 사용하면 메모리에 한 번 올라가면 같은 값을 클래스 내부의 전체 필드와 메서드에서 공유한다.
  - final을 선언한 변수를 사용하면 해당 필드, 메서드 별로 호출할 때마다 새로이 값이 할당(인스턴스화)한다.
  - <b>상수로 사용하려고 할 때, 그 값은 변하지 않을 것인데 호출할 때마다 새롭게 인스턴스화할 필요가 없기 때문에 static final을 관습적으로 사용한다.</b>

<br/>

<br/>

## 예상질문❔

Q1) static 이란 무엇인가?

A1) static으로 선언된 변수는 메모리 공간에 하나만 존재하고, 어디에서나 접근이 가능한 변수이다.

<br/>

Q2) final 이란 무엇인가?

A2) final은 변수를 상수화 시킨다 .즉, 한번 값이 결정된 변수의 값은 변경이 불가능하다.

<br/>

Q3) static final이란 무엇인가?

A3) 원주율, 산소의 질량 등 누구나 알고있는 변하지 않는 상수의 값을 static final로 설정하여 변경되지 않도록 한다.

<br/>

<br/>

### Reference📖

- https://goodncuteman.tistory.com/4
- https://m.blog.naver.com/PostView.nhn?blogId=goddlaek&logNo=220889229659&proxyReferer=https:%2F%2Fwww.google.com%2F
- https://blog.naver.com/goddlaek/220888359923
- https://it-mesung.tistory.com/86?category=830540
- https://hunit.tistory.com/159
- https://zorba91.tistory.com/275
