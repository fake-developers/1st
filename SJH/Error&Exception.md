# Error&Exception

- **runtime시 발생하는 프로그램 오류**

  :bulb: **프로그램 오류**

  - 프로그램 실행 중 오작동하거나 비정상적으로 종료되게 하는 원인
  - 오류의 종류
    - 컴파일 에러 (Compile-Error) : 소스 상의 문법 에러, 컴파일 시에 발생
    - **런타임 에러 (Runtime-Error) : 입력 값이 틀렸거나, 배열의 인덱스 범위를 벗어났거나, 계산식의 오류 등으로 인한 에러, 실행 시에 발생**
    - 논리적 에러 (Logical-Error) : 실행은 되지만 의도와 다르게 동작하는 에러
    - 시스템 에러 (System-Error) : 컴퓨터의 오작동으로 인한 에러, 소스 구문으로 해결 불가

- Error와 Exception은 모두 Throwable의 상속을 받는다.

  - Throwable 클래스는 예외처리를 할 수 있는 최상위 클래스이다.

  <img src="https://user-images.githubusercontent.com/58902042/111029212-cef60300-843e-11eb-9219-cf8515d1ff63.png" height=320>

<br>

## Error(에러)

<img src="https://user-images.githubusercontent.com/58902042/111029256-1e3c3380-843f-11eb-8cee-40070929e136.png" height=360>

- 시스템 레벨에서 발생
- **개발자가 어떻게 조치할 수 없는 수준**을 의미
  - 전부 예측 불가능한 Unchecked Error에 속한다.
  - 컴퓨터 하드웨어의 오동작 또는 고장으로 인해 **응용프로그램에 이상**이 생겼거나 **JVM 실행에 문제**가 생겼을 경우
- ex_) OutOfMemoryError,  StackOverflowError
  - OutOfMemoryError : JVM에 설정된 메모리의 한계를 벗어난 상황일 때 발생
    - heap 사이즈가 부족하거나, 너무 많은 class를 로드할 때, 가용가능한 swap이 없을 때..
    - 해결방안으로는 dump 파일분석, jvm 옵션 수정등이 있다.

<br>

## Exception(예외)

<img src="https://user-images.githubusercontent.com/58902042/111029743-a7ed0080-8441-11eb-8c4a-8103964a7355.png" height=360>

- 개발자가 구현한 로직에서 발생하며, 개발자가 다른 방식으로 처리 가능

- Exception이 발생하는 경우엔 개발자가 예외 발생 상황을 예측해서 미리 **예외처리(Exception Handling) 코드를 작성할 수 있다**.

  - 이를 통해 예외 상황이 발생된 경우의 처리로직을 만들어 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지하게 한다.

- #### Exception의 2가지 종류

  - **Checked Exception** :
    - **예외처리 필수**, 처리하지 않으면 컴파일 되지 않는다.
    - **컴파일 단계에서 확인**하며, 예외 발생 시 roll-back하지 않는다.
    - JVM 외부와 통신(네트워크, 파일시스템 등)할 때 주로 쓴다.
    - RuntimeException 이외에 있는 모든 예외
    - IOException, SQLException 등

  - **Unchecked Exception** 
    - **명시적인 처리를 강제하지 않는다.**
    - **컴파일 때 체크되지 않고**, runtime에서 확인하며 예외 발생 시 roll-back한다.
    - RuntimeException 하위의 모든 예외
    - NullPointerException, IndexOutOfBoundException 등

- #### 대표적인 클래스들

  | 클래스                              | 설명                                                         |
  | ----------------------------------- | ------------------------------------------------------------ |
  | **NullPointerException**            | Null 레퍼런스를 참조할때 발생<br>(거의 대부분은 객체가 제대로 생성되지 않은 경우 발생) |
  | **IndexOutOfBoundsException**       | 배열과 유사한 자료구조(문자열, 배열, 자료구조)에서 범위를 벗어난 인덱스 번호 사용으로 발생<br>서브 Exception 클래스 :<br>StringIndexOutOfBoundsException, ArrayIndexOutOfBoundsException |
  | **FormatException**                 | 문자열, 숫자, 날짜 변환 시 잘못된 데이터(ex. "123A" -> 123 으로 변환 시)로 발생<br>(보통 사용자의 입력, 외부 데이터 로딩, 결과 데이터의 변환 처리에서 자주 발생) |
  | **ArthmeticException**              | 정수를 0으로 나눌때 발생                                     |
  | **ClassCastException**              | 변환할 수 없는 타입으로 객체를 변환할 때 발생                |
  | **IllegalArgumentException**        | 잘못된 인자 전달 시 발생                                     |
  | **IOException**                     | 입출력 동작 실패 또는 인터럽트 시 발생                       |
  | **IllegalStateException**           | 객체의 상태가 매소드 호출에는 부적절한 경우                  |
  | **ConcurrentModificationException** | 금지된 곳에서 객체를 동시에 수정하는것이 감지될 경우 발생    |
  | **UnsupportedOperationException**   | 객체가 메소드를 지원하지 않는 경우 발생                      |
  | **OutOfMemoryException**            | 메모리가 부족한 경우 발생                                    |
  | **ClassNotFoundException**          | 컴파일된 class 파일을 찾을 수 없을 때                        |

- #### 주요 메서드

  | 메소드                | 설명                                                         |
  | --------------------- | ------------------------------------------------------------ |
  | **printStackTrace()** | 발생한 Exception의 출처를 메모리상에서 추적하면서 결과를 알려준다. 발생한 위치를 정확히 출력해줘서 제일 많이 쓰며 void를 반환한다. |
  | **getMessage()**      | 한줄로 요약된 메세지를 String으로 반환해준다.                |
  | **getStackTrace()**   | jdk1.4 부터 지원, printStackTrace()를 보완, StackTraceElement[] 이라는 문자열 배열로 변경해서 출력하고 저장한다. |

- #### 예외처리

  - Java에서 모든 예외가 발생하면 Exception 객체를 생성한다.
  - 예외 상황이 발생된 경우의 처리로직을 만들어 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지하게 한다.
  - JVM의 예외처리기가 받아 원인을 화면에 출력한다.

  1. **예외가 발생한 메서드 안에서 처리 (try-catch-finally)**

     - **try 블록** : 예외가 발생할 가능성이 있는 코드,  try 블록은 최소한 하나의 catch 블록이 있어야 하며, catch 블록은 try 블록 다음에 위치한다.
     - **catch 블록** : 예외에 대한 후 처리 코드, 블록의 매개변수는 예외 객체가 발생했을 때 참조하는 변수명으로 반드시 java.lang.Throwable 클래스의 하위 클래스 타입으로 선언
     - **finally 블록** : Try 블록에서의 Exception과 발생 유무와 상관 없이 무조건 수행되는 코드 (옵션이라 생략이 가능)

     ```java
     public class Test {
         public static void main(String[] args) {
             while(true) {
                 try {
                     Scanner scan = new Scanner(System.in);
                     int value = scan.nextInt();
                     System.out.println(9/value);
                 } catch(ArithmeticException e) {
                     e.printStackTrace();
                 } finally {
                     System.out.println("무조건 실행됩니다.");
                 }
             }
         }
     }
     ```

     ~~~
     <실행결과>
     //exception이 발생하지 않는 경우
     9 
     1 
     무조건 실행됩니다. 
     
     //exception이 발생한 경우
     0 
     java.lang.ArithmeticException: / by zero 
     무조건 실행됩니다. 
     	at Test.main(Test.java:9) 
     ~~~

     

  2. **예외가 발생한 메서드를 호출한 곳에서 처리 (throws)**

     - 예외가 발생한 지점이 아닌, 예외가 발생한 코드를 호출한 지점으로 예외를 전달하여 처리하는 방법

     ```java
     public class Test {
         public static void main(String[] args) {
             while(true) {
                 try {
                     divisionMethod();
                 } catch(ArithmeticException e) {
                     e.printStackTrace();
                 } finally {
                     System.out.println("무조건 실행됩니다.");
                 }
             }
         }
         
         public static void divisionMethod() throws ArithmeticException {
             Scanner scan = new Scanner(System.in);
             int value = scan.nextInt();
             System.out.println(9/value);
         }
     }
     
     ```

     ~~~
     <실행결과>
     //exception이 발생하지 않는 경우
     9 
     1
     무조건 실행됩니다.
     
     //exception이 발생한 경우
     0 
     java.lang.ArithmeticException: / by zero 
     무조건 실행됩니다. 
     	at Test.divisionMethod(Test.java:19) 
     //	at Test.main(Test.java:7) 
     ~~~

     

  3. **강제로 예외를 발생시켜 처리 (throw)**

     ```java
     public class Test {
         public static void main(String[] args) {
             while(true) {
                 try {
                     divisionMethod();
                 } catch(ArithmeticException e) {
                     e.printStackTrace();
                     e.getMessage();
                 } finally {
                     System.out.println("무조건 실행됩니다.");
                 }
             }
         }
         
         public static void divisionMethod() throws ArithmeticException {
             Scanner scan = new Scanner(System.in);
             int value = scan.nextInt();
             if(value == 0) 
             {
                 throw new ArithmeticException("0으로 나눌 수 없습니다.");
             }
             System.out.println(9/value);
         }
     }
     ```

     ~~~
     <실행결과>
     //exception이 발생하지 않는 경우
     3 
     3 
     무조건 실행됩니다. 
     
     //exception이 발생한 경우
     0 
     무조건 실행됩니다. 
     java.lang.ArithmeticException: 0으로 나눌 수 없습니다. 
     	at Test.divisionMethod(Test.java:22) 
     	at Test.main(Test.java:7) 
     ~~~

     

  4. **사용자 예외를 생성하여 처리**

     - 정상적으로 동작하지만 비지니스 로직 부분에서는 강제로 예외를 발생시켜야 할 상황이 생기고 자바에서는 특정 상황에서의 예외를 작성하여 발생시킬 수 있다.
     - 생성하는 법 : Exception을 상속받는다.

     ```java
     class InsertZeroException extends Exception {
         public InsertZeroException() {
             super("0을 입력할 수 없습니다.");
         }
     }
     
     public class Test {
         public static void main(String[] args) {
             while(true) {
                 try {
                     divisionMethod();
                 } catch(InsertZeroException e) {
                     e.printStackTrace();
                     e.getMessage();
                 } finally {
                     System.out.println("무조건 실행됩니다.");
                 }
             }
         }
         
          public static void divisionMethod() throws InsertZeroException {
                 Scanner scan = new Scanner(System.in);
                 int value = scan.nextInt();
                 if(value == 0) 
                 {
                     throw new InsertZeroException();
                 }
                 System.out.println(9/value);
         }
     }
     ```

     ~~~
     <실행결과>
     //exception이 발생하지 않는 경우
     9 
     1 
     무조건 실행됩니다. 
     
     //exception이 발생한 경우
     0 
     무조건 실행됩니다. 
     InsertZeroException: 0을 입력할 수 없습니다. 
     	at Test.divisionMethod(Test.java:28) 
     	at Test.main(Test.java:13)
     ~~~

  - **Throws와 Throw의 혼동**
    - 공통점 :  Exception을 발생시킨다는 공통점
    - but , 
    - Throws : 자신을 호출한 상위 메소드로 Exception을 발생시킨다.
    - Throw : 강제로 에러를 발생시키고자 할 때 사용한다.(현재 메소드 또는 상위 메소드)

-------

**<참조>**

- https://rebeccacho.gitbooks.io/java-study-group/content/chapter8.html
- [Java 예외처리에 대한 작은 생각](https://www.nextree.co.kr/p3239/)

- [자바 이론# 예외 처리](https://velog.io/@codepark_kr/%EC%9E%90%EB%B0%94-%EC%9D%B4%EB%A1%A0-%EC%98%88%EC%99%B8-%EC%B2%98%EB%A6%AC)

- [예외처리 (throwable, exception, error, throws)](https://sjh836.tistory.com/122)

- [[JAVA] 자바 Exception 개념 및 예외 처리란?](https://limkydev.tistory.com/198)

- [자바 예외처리(Exception handling)](https://ktko.tistory.com/entry/JAVA-자바의-예외처리Exception-handling)

  