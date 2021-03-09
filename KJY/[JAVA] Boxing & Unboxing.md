# [JAVA] Boxing & Unboxing

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-09)* 



#### :pushpin: Wrapper 클래스란?

- 자바에서는 8개의 기본형을 객체로 다루지 않음
- 기본 자료형(int, double, boolean 등)의 데이터를 인스턴스 (객체)로 만들기 위해 사용(포장)하는 클래스

* 사용 이유
  1. 객체 또는 클래스가 제공하는 메서드 또는 생성자에 필요 (기본형이 아닌 객체로 저장이 되어야 할 때)
     * 예시 - Collection
       * Map에는 Key와 Value가 있음. 선언을 할 때 Map에는 Key와 Value를 **참조형만** 받을 수 있음 
       * 따라서 Map<String, Integer>으로 선언을 함. Map<String, int>는 성립되지 않음
  2. 클래스가 제공하는 상수 사용(MIN_VALUE, MAX_VALUE 등..)
  3. 숫자, 문자로의 형 변환 또는 진법 변환에 사용
     * 예시 - Integer.parseInt

* 종류

  * 8개의 기본형을 대표하는 8개의 래퍼 클래스가 있음

  * java.lang 패키지에 소속되어 있음

  * char형과 int형을 제외한 나머지는 기본 데이터 타입의 앞 글자를 대문자로 변경해주면 됨

  * | 기본형  | 포장 클래스   | 생성 예                                                      |
    | ------- | ------------- | ------------------------------------------------------------ |
    | boolean | **Boolean**   | Boolean bA = new Boolean(true);<br />Boolean bB = new Boolean(“false”); |
    | char    | **Character** | Character cA = new Character(‘a’);                           |
    | byte    | **Byte**      | Byte byA = new Byte(10);<br />Byte byB = new Byte(“127”);    |
    | short   | **Short**     | Short sA = new Short(1234);<br />Short sB = new Short(“1234”); |
    | int     | **Integer**   | Integer iA = new Integer(1234);<br />Integer iB = new Integer(“1234”); |
    | long    | **Long**      | Long lA = new Long(1234);<br />Long lB = new Long(“1234”);   |
    | float   | **Float**     | Float fA = new Float(12.34f);<br />Float fB = new Float(“12.34f”); |
    | double  | **Double**    | Double dA = new Double(12.34);<br />Double dB = new Double(“12.34”); |

  * 생성자는 매개변수로 문자열이나 각 자료형의 값들을 인자로 받음

  * 주의) 문자열로 주는 경우, 각 자료형에 알맞는 문자열을 사용해야 함

    * new Integer("1.0"); -> NumberFormatException 발생

<br/>

## 1. Boxing(박싱)

- 기본형을 참조형으로 변환하는 것
- 기본 자료형 객체를 래퍼(wrapper) 클래스의 객체로 만드는 과정

```java
public class WrapperEx01 {
	public static void main(String[] args) {
		int i = 10;
		Integer wi = new Integer(i); // 박싱(int → Integer)
		
		String str = "10";
		Integer wi2 = new Integer(str); // String → Integer
		
		double d = 3.14;
		Double wd = new Double(d); // 박싱(double → Double)
	}
}
```

<br/>

#### 1-1. 묵시적인 박싱

- 오토박싱(autoboxing)
  - 자바 컴파일러가 기본형 데이터 타입을 그에 상응하는 wrapper class로 자동 변환 시켜주는 것
  - JDK 1.5부터 지원

```java
public static void main(String[] args) {
    int i = 10;
    Integer iObj = i;
    
    double d1 = 3.14;
	Double wd = d1;
}
```

<br/>

#### 1-2. 명시적인 박싱

- 프로그래머가 명시적으로 형변환 해주는 것

```java
public static void main(String[] args) {
    int i = 10;
    Integer iObj = (Integer)i;
    
    double d1 = 3.14;
	Double wd = (Double)d1;
}
```

* wrapper 클래스에서 갖고 있는 **valueOf()** **메서드를** **이용**하는 방법

```java
public static void main(String[] args) {
	int i = 10;
	Integer wi = Integer.valueOf(i); // 박싱(int → Integer)
		
	String str = "10";
	Integer wi2 = Integer.valueOf(str); // String → Integer
		
	double d = 3.14;
	Double wd = Double.valueOf(d); // 박싱(double → Double)
		
	boolean bl = true;
	Boolean wb = Boolean.valueOf(bl); // 박싱(boolean → Boolean)
}
```

<br/>

## 2. Unboxing(언박싱)

- 참조형을 기본형으로 변환하는 것
- 래퍼(wrapper) 클래스 타입의 값을 기본 자료형 타입으로 바꾸는 것

```java
public static void main(String[] args) {
    int i = 10;
	Integer wi = new Integer(i); // 박싱(int → Integer)
	int i2 = wi.intValue(); // 언박싱(Integer → int)
		
	Double wd = new Double(3.14);
	double d = wd.doubleValue(); // 언박싱(Double → double)
		
	Boolean wb = new Boolean(true);
	boolean bl = wb.booleanValue(); // 언박싱(Boolean → boolean)
}
```

<br/>

#### 2-1. 묵시적인 언박싱

- 오토 언박싱(auto un-boxing)
  - 자바 컴파일러가 자동으로 언박싱 진행
  - JDK 1.5부터 지원

```java
public static void main(String[] args) {
    int i1 = 10;
	Integer wi = i1; // 오토 박싱
	int i2 = wi; // 오토 언박싱
		
	double d1 = 3.14;
	Double wd = d1; // 오토 박싱
	double d2 = wd; // 오토 언박싱
		
	boolean b1 = true;
	Boolean wb = b1; // 오토 박싱
	boolean b2 = wb; // 오토 언박싱
}
```

<br/>

#### 2-2. 명시적인 언박싱

```java
public static void main(String[] args) {
    Integer intg = new Integer(20);
    int i = (int)intg;
}
```

* wrapper 클래스에서 갖고 있는 **기본자료형Value()** **메서드를** **이용**하는 방법

```java
public static void main(String[] args) {
    Integer intg = new Integer(20);
    int i = intg.intValue();
    
    Double wd = new Double(3.14);
    double d = wd.doubleValue();
}
```

<br/>

## :page_with_curl: Reference

[[JAVA/자바] 래퍼(Wrapper) 클래스와 박싱(boxing), 언박싱(un-boxing)](http://blog.naver.com/PostView.nhn?blogId=heartflow89&logNo=220975218499&redirect=Dlog&widgetTypeCall=true)

[[자바 코딩] JAVA AUTOBOXING VS UNBOXING](https://jamesdreaming.tistory.com/154)

[자바 박싱(boxing)과 언박싱(unboxing)](https://ktko.tistory.com/entry/자바-박싱boxing과-언박싱unboxing)

[자바(JAVA)의 wrapper클래스,박싱(boxing),언박싱(unboxing)](https://studymake.tistory.com/420)