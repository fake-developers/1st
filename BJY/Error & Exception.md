## Error(오류)와 Exception(예외)

<br/>

![Throwable](https://user-images.githubusercontent.com/61674527/110339324-64724b00-806b-11eb-8e96-6db604670805.png)

Throwable 클래스는 예외처리를 할 수 있는 최상위 클래스이다. Exception과 Error는 Throwable의 상속을 받는다.

<br/>

### <u>Error(오류)</u>

* 시스템 레벨에서 발생

* **컴퓨터 하드웨어의 오동작 또는 고장**으로 인해 응용프로그램에 이상이 생겼거나 JVM 실행에 문제가 생겼을 경우 발생하는 것
  * 따라서 개발자가 미리 예측하여 처리할 수 없기 때문에, 애플리케이션에서 오류에 대한 처리를 신경쓰지 않아도 된다.

<br/>

### <u>Exception(예외)</u>

* 개발자가 구현한 로직에서 발생
* 사용자의 잘못된 조작 또는 개발자의 잘못된 코딩으로 인해 발생하는 프로그램 오류

예외가 발생하면 프로그램이 종료가 된다는 것은 에러와 동일하지만 예외는 **예외처리(Exception Handling)를 통해 프로그램을 종료되지 않고 정상적으로 작동되게 만들어 줄 수 있다.** 

즉, 예외는 발생할 상황을 미리 예측하여 처리할 수 있다.

#### 종류 

* **Checked Exception**
  * 반드시 예외를 처리 해야한다.
    * 처리하지 않으면 컴파일 되지 않는다.
  * 확인 : 컴파일 단계
  * 예외 발생 시 트랜잭션 처리 : roll-back 하지 않는다
  * 대표 예외 
    * RuntimeException를 제외한 모든 예외
    * IOException
* **Unchecked Exeption**
  * 예외 처리를 반드시 하지 않아도 된다.
  * 확인 : 실행단계 확인
  * 예외 발생시 트랜잭션 처리 : roll-back 진행된다.
  * 대표 예외
    * RuntimeException 하위 예외
    * NullPointException
    * IllegalArgumentException
    * IndexOutOfBoundException
    * SystemException

~~~
roll-back

데이터베이스에서 업데이트에 오류가 발생할 때, 이전 상태로 되돌리는 것을 말한다.
~~~

<br/>

#### 대표적인 Exception Class

| 예외                              | 설명                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| **ArithmeticException**           | 정수를 0으로 나눌경우 발생                                   |
| **ArrayIndexOutOfBoundsExcetion** | 배열의 범위를 벗어난 index를 접근할 시 발생                  |
| **FileNotFoundException**         | 파일을 못 찾을 때 발생                                       |
| **ClassCastExcetion**             | 변환할 수 없는 타입으로 객체를 반환 시 발생                  |
| **NullPointException**            | 존재하지 않는 레퍼런스를 참조할 때 발생 <br />(거의 대부분은 객체가 제대로 생성되지 않은 경우 발생) |
| **IllegalArgumentException**      | 잘못된 인자를 전달할 때 발생                                 |
| **IOException**                   | 입출력 동작 실패 또는 인터럽트 시 발생                       |
| **OutOfMemoryException**          | 메모리가 부족한 경우 발생                                    |
| **NumberFormatException**         | 문자열이 나타내는 숫자와 일치하지 않는 타입의 숫자로 변환시 발생 |
| **ClassNotFoundException**        | 컴파일된 class 파일을 찾을 수 없다.                          |

<br/>

#### 주요 Method

| 메소드                | 설명                                                         |
| --------------------- | ------------------------------------------------------------ |
| **printStackTrace()** | 발생한 Exception의 출처를 메모리상에서 추적하면서 결과를 알려준다.<br />발생한 위치를 정확히 출력해줘서 제일 많이 쓰며 void를 반환한다. |
| **getMessage()**      | 한줄로 요약된 메세지를 String으로 반환해준다.                |
| **getStackTrace()**   | jdk1.4 부터 지원, printStackTrace()를 보완, StackTraceElement[] 이라는 문자열 배열로 변경해서 출력하고 저장한다. |

<br/>

#### Exception Handling

JAVA에서 모든 예외가 발생하면 Exception 객체를 생성한다. 예외를 처리할 수 있는 예외 처리문이 있다.

1. **예외가 발생한 메서드 안에서 처리 (try-catch-finally)**

   * **try** : 예외가 발생할 가능성이 있는 범위를 지정하는 블록이다. try 블록은 최소한 하나의 catch 블록이 있어야 하며, catch 블록은 try 블록 다음에 위치한다.
   * **catch** : 블록의 매개변수는 예외 객체가 발생했을 때 참조하는 변수명으로 반드시 java.lang.Throwable 클래스의 하위 클래스 타입으로 선언되어야 합니다.
   * **finally** : 이 블록은 필수 변록이 아니며, finally 블록은 catch 유무와 상관 없이 무조건 수행된다. 주로 IO 또는 Connection을 close() 하는데 사용된다.

   ~~~java
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
   
   //실행결과
   /*
   9 
   1 
   무조건 실행됩니다. 
   0 
   java.lang.ArithmeticException: / by zero 
   무조건 실행됩니다. 
   	at Test.main(Test.java:9) 
   1 
   9 
   무조건 실행됩니다.
   */
   ~~~

2. **예외가 발생한 메서드를 호출한 곳에서 처리 (throws)**

   * 예외가 발생한 지점이 아닌, 예외가 발생한 코드를 호출한 지점으로 예외를 전달하여 처리하는 방법

   ~~~java
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
   
   //실행결과
   /*
   9 
   1 
   무조건 실행됩니다. 
   0 
   java.lang.ArithmeticException: / by zero 
   무조건 실행됩니다. 
   	at Test.divisionMethod(Test.java:19) 
   	at Test.main(Test.java:7) 
   3 
   3 
   무조건 실행됩니다.
   */
   ~~~

3. **강제로 예외를 발생시켜 처리 (throw)**

   ~~~java
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
   
   //실행결과
   /*
   3 
   3 
   무조건 실행됩니다. 
   0 
   무조건 실행됩니다. 
   java.lang.ArithmeticException: 0으로 나눌 수 없습니다. 
   	at Test.divisionMethod(Test.java:22) 
   	at Test.main(Test.java:7) 
   2 
   4 
   무조건 실행됩니다.
   */
   ~~~

4. **사용자 예외를 생성하여 처리**

   * 정상적으로 동작하지만 비지니스 로직 부분에서는 강제로 예외를 발생시켜야 할 상황이 생기고 자바에서는 특정 상황에서의 예외를 작성하여 발생시킬 수 있다.
   * 생성하는 법 : Exception을 상속받는다.

   ~~~java
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
   
   //실행결과
   /*
   9 
   1 
   무조건 실행됩니다. 
   0 
   무조건 실행됩니다. 
   InsertZeroException: 0을 입력할 수 없습니다. 
   	at Test.divisionMethod(Test.java:28) 
   	at Test.main(Test.java:13)
   */
   ~~~

> **Throws와 Throw를 혼동**
>
> 이 두가지는 Exception을 발생시킨다는 공통점이 있지만 
>
> Throws는 자신을 호출한 상위 메소드로 Exception을 발생시킨다는 것
>
> Throw는 강제로 에러를 발생시키고자 할 때 사용한다.(현재 메소드 또는 상위 메소드)

<br/>

<br/>

<br/>

### REFERENCE

* [Error&Exception (1)](https://java119.tistory.com/44)
* [Error&Exception (2)](https://github.com/GimunLee/tech-refrigerator/blob/master/Language/JAVA/Error%20%26%20Exception.md#error--exception)
* [Exception Handling (1)](https://ktko.tistory.com/entry/JAVA-%EC%9E%90%EB%B0%94%EC%9D%98-%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%ACException-handling)
* [Exception Handling (2)](https://velog.io/@ssseungzz7/Java-Exception-handling)

