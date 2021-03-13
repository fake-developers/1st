# Boxing & Unboxing

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYoung-Kwon*

<hr>


#### <small>+) 참고 - </small> Wrapper 클래스

- <b> Wrapper 클래스란?</b>

  - 자바에서는 8개의 기본형을 객체로 다루지 않는다.
  - 이 기본 자료형의 데이터를 인스턴스(객체)로 만들기 위해 사용(포장)하는 클래스이다.

  <br/>

- <b>Wrapper 클래스 사용 이유</b>

  - 객체 또는 클래스가 제공하는 메서드 또는 생성자에 필요하다.
    - 기본형이 아닌 객체로 저장이 되어야할 때 등
    - ex) Collection
      - Map에는 Key와 Value가 있는데, 선언 시 Key와 Value는 참조형만 가능하다.
      - 따라서 Map<String, Integer> 등으로 선언하고, Map<String, int>는 성립되지 않는다.
  - 클래스가 제공하는 상수를 사용할 때 (MIN_VALUE, MAX_VALUE 등)
  - 숫자, 문자로의 형 변환 또는 진법 변환이 필요할 때
    - ex) Integer.parseInt

  <br/>

- <b>Wrapper 클래스 종류</b>

  - 8개의 기본형을 대표하는 8개의 wrapper 클래스가 있다.

  - java.lang 패키지에 소속되어 있다.

    | 기본형  | 포장 클래스   | 생성 예                                                      |
    | ------- | ------------- | ------------------------------------------------------------ |
    | boolean | **Boolean**   | Boolean bA = new Boolean(true); <br/>Boolean bB = new Boolean(“false”); |
    | char    | **Character** | Character cA = new Character(‘a’);                           |
    | byte    | **Byte**      | Byte byA = new Byte(10); <br/>Byte byB = new Byte(“127”);    |
    | short   | **Short**     | Short sA = new Short(1234); <br/>Short sB = new Short(“1234”); |
    | int     | **Integer**   | Integer iA = new Integer(1234);<br/>Integer iB = new Integer(“1234”); |
    | long    | **Long**      | Long lA = new Long(1234); <br/>Long lB = new Long(“1234”);   |
    | float   | **Float**     | Float fA = new Float(12.34f); <br/>Float fB = new Float(“12.34f”); |
    | double  | **Double**    | Double dA = new Double(12.34); <br/>Double dB = new Double(“12.34”); |

    - 생성자는 매개변수로 문자열이나 각 자료형의 값들을 인자로 ㅂ다는다.
    - 주의할 점
      - 문자열을 인자로 주는 경우, 각 자료형에 알맞는 문자열을 사용해야 한다.
      - new Integer("1.0"); --> NumberFormatException 발생

    <br/>

    <br/>

    <br/>

## Boxing (박싱)


- <b>Boxing 이란?</b>
  
  - 기본형을 참조형으로 변환하는 것이다.
  - 기본 자료형 데이터를 Wrapper 클래스의 객체로 만드는 과정이다.
  
``` java
  public class WrapperEx01{
      public static void main(String[] args){
          int i = 10;
          Integer wi = new Integer(i); // 박싱 (int -> Integer)
          
          String str = "10";
          Integer wi2 = new Integer(str); // (String -> Integer)
          
          double d = 3.14;
          Double wd = new Double(d); // 박싱 (double -> Double)
      }
  }
  ```

<br/>

<br/>

- <b>묵시적인 박싱</b>

  - 오토 박싱 (autoboxing)

    - 자바 컴파일러가 <b>기본형 데이터 타입을 그에 상응하는 wrapper class로</b> 자동 변환 시켜주는 것을 말한다.
    - JDK 1.5 부터 지원

    ``` java
    public static void main(String[] args){
        int i = 10;
        Integer iObj = i; // int를 Integer로 오토 박싱
        
        double d1 = 3.14;
        Double wd = d1; // double을 Double로 오토 박싱
    }
    ```

<br/>

<br/>

- <b>명시적인 박싱</b>

  - 프로그래머가 명시적으로 형변환을 해주는 것을 말한다.
    ``` java
    public static void main(String[] args){
        int i = 10;
        Integer iObj = (Integer)i; // 명시적으로 형변환
        
        double d1 = 3.14;
        Double wd = (Double)d1; // 명시적으로 형변환
    }
    ```

  <br/>

  - Wrapper 클래스가 갖고있는 valueOf() 메서드를 이용하는 방법도 있다.

    ``` java
    public static void main(String[] args){
        int i = 10;
        Integer wi = Integer.valueOf(i);
        
        String str = "10";
        Integer wi2 = Integer.valueOf(str);
        
        double d = 3.14;
        Double wd = Double.valueOf(d);
        
        boolean b1 = true;
        Boolean wb = Boolean.valueOf(b1);
    }
    ```

    

<br/>

<br/>

<br/>

## Unboxing (언박싱)

- <b>Unboxing 이란?</b>
  
  - 참조형을 기본형으로 변환하는 것을 말한다.
  - Wrapper 클래스 타입의 값을 기본 자료형 타입으로 바꾸는 것이다.
  
  ``` java
  public static void main(String[] args){
      int i = 10;
      Integer wi = new Integer(i); // 박싱 (int -> Integer)
      int i2 = wi.intValue(); // 언박싱 (Integer -> int)
      
      Double wd = new Double(3.14);
      double d = wd.doubleValue(); // 언박싱 (Double -> double)
      
      Boolean wb = new Boolean(true);
      boolean bl = wb.booleanValue(); // 언박싱 (Boolean -> boolean)
  }
  ```

<br/>

<br/>

- <b>묵시적인 언박싱</b>

  - 오토 언박싱 (auto un-boxing)

    - 자바 컴파일러가 자동으로 언박싱을 진행한다.
    - JDK 1.5부터 지원한다.

    ``` java
    public static void main(String[] args){
        int i1 = 10;
        Integer wi = i1; // 오토 박싱
        int i2 = wi; // 오토 언박싱
        
        double d1 = 3.14;
        Double wd = d1; // 오토 박싱
        double d2 = d1; // 오토 언박싱
        
        boolean b1 = true;
        Boolean wb = b1; // 오토 박싱
        boolean b2 = wb; // 오토 언박싱
    }
    ```

  <br/>

  <br/>

- <b>명시적인 언박싱</b>

  - 프로그래머가 명시적으로 형변환

    ``` java
    public static void main(String[] args){
        Integer intg = new Integer(20);
        int i = (int)intg; // 명시적 형변환
    }
    ```

  <br/>

  - Wrapper 클래스에서 갖고 있는 기본 자료형 Value() 메서드를 이용하는 방법

    ``` java
    public static void main(String[] args){
        Integer intg = new Integer(20);
        int i = intg.intValue();
        
        Double wd = new Double(3.14);
        double d = wd.doubleValue();
    }
    ```

<br/>

<br/>

<br/>

## 예상질문❔

Q1) Wrapper 클래스란 무엇인가?

A1) 기본자료형의 데이터를 인스턴스로 만들기 위해 포장하는 클래스이다. 

<br/>

Q2) 박싱, 언박싱이란 무엇인가?

A2) 박싱이란 Wrapper 클래스를 이용하여 기본 자료형을 참조형으로 변환하는 것이고, 언박싱이란 참조형인 Wrapper 클래스 타입의 값을 기본 자료형으로 타입을 바꾸는 것이다.

<br/>

<br/>

### Reference📖

- https://k39335.tistory.com/40
- https://khj93.tistory.com/entry/JAVA-%EB%9E%8C%EB%8B%A4%EC%8B%9DRambda%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%82%AC%EC%9A%A9%EB%B2%95
- https://nesoy.github.io/articles/2018-04/Java-Annotation
- https://qssdev.tistory.com/27
- https://blueyikim.tistory.com/147

