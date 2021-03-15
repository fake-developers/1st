# 박싱(Boxing)과 언박싱(UnBoxing)

- JDK 1.5 버전 부터 추가된 개념

  - JDK 1.5버전 밑 버전은 컴파일러가 기본형과 참조형의 관계를 알지 못했다.

- **기본 자료형(Primitive Type)과 래퍼 클래스(Wrapper Class) 간의 변환**을 나타내는 단어이다.

  :bulb:**래퍼 클래스(Wrapper Class)**

  - 기본자료형(int, double, boolean 등)의 데이터를 인스턴스(객체)로 만들기 위해 사용하는 클래스

  - **사용이유**

    - 제네릭, 자료구조, 매개변수 등 기본 자료형이 아닌 레퍼런스 타입을 필요로 하는 경우가 많고 메서드를 갖고 있어 다양하게 활용이 가능하기 때문이다.

      ex_) Map<String, Integer>으로 선언을 함. Map<String, int>는 성립되지 않음

    - 인스턴스를 생성(heap 메모리에 저장)하여 상속 및 재사용이 가능하기 때문이다.

    - 문자열과 기본 자료형 간 형 변환에 사용이 가능하기 때문이다.

      ex_) Integer.parseInt()

  - **래퍼 클래스 종류**

    - 우리가 사용하는 기본 자료형의 모든 wrapper 클래스는 자바에서 기본적으로 제공

    - java.lang 패키지에 소속

    - 대부분 기본 데이터 타입의 앞 글자를 대문자로 바꿔주면 된다.

      | 기본 자료형 | Wrapper 클래스 |
      | ----------- | -------------- |
      | byte        | Byte           |
      | char        | Character      |
      | short       | Short          |
      | int         | Integer        |
      | long        | Long           |
      | float       | Float          |
      | double      | Double         |
      | boolean     | Boolean        |

  - **래퍼클래스에 대입된 값은 ==, !=과 같은 연산자를 이용하여 값의 비교가 불가능**
    - 인스턴스를 생성하면서 heap 메모리에 값이 저장되고 객체 변수는 참조 값을 가지기 때문이다.
    - 따라서, equals()메서드를 이용하거나 데이터를 언박싱해서 값을 비교해야 한다.

<br>

## 박싱(Boxing)

- 기본 자료형의 데이터를 래퍼 클래스의 객체로 만드는 과정

- 박싱하는 방식 

  - **명시적 박싱** :  new 연산자를 이용, valueOf() 메서드 이용, 프로그래머가 명시적으로 형변환

  - **묵시적 박싱** : 오토 박싱

  - **new 연산자를 이용**

    ~~~java
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
    ~~~

  - wrapper 클래스가 가지고 있는 **valueOf()메서드를 이용**

    ~~~java
    public class WrapperEx02 {
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
    }
    ~~~

  - **프로그래머가 명시적으로 형 변환**

    ~~~java
    public static void main(String[] args) {
        int i = 10;
        Integer iObj = (Integer)i;
        
        double d1 = 3.14;
    	Double wd = (Double)d1;
    }
    ~~~

  - **오토박싱(atuoboxing)**

    - 자바 컴파일러가 기본형 데이터 타입을 그에 상응하는 wrapper class로 자동 변환 시켜주는 것
    - 해당 래퍼(wrapper) 클래스에 기본 자료형의 데이터를 대입
    - JDK 1.5부터 지원

    ~~~java
    public class WrapperEx04 {
    	public static void main(String[] args) {
    		int i1 = 10;
    		Integer wi = i1; // 오토 박싱
    	}
    }
    ~~~

    

<BR>

## 언박싱(UnBoxing)

- 래퍼 클래스의 데이터를 기본 자료형 변경하는 과정

- 언박싱하는 방식

  - **명시적 박싱** : (기본자료형)value()메서드 이용, 프로그래머가 명시적으로 형변환

  - **묵시적 박싱** : 오토언박싱

  - wrapper 클래스가 가지고 있는**(기본자료형)value()메서드 이용**

    ~~~java
    public class WrapperEx03 {
    	public static void main(String[] args) {
    		int i = 10;
    		Integer wi = new Integer(i); // 박싱(int → Integer)
    		int i2 = wi.intValue(); // 언박싱(Integer → int)
    		
    		Double wd = new Double(3.14);
    		double d = wd.doubleValue(); // 언박싱(Double → double)
    		
    		Boolean wb = new Boolean(true);
    		boolean bl = wb.booleanValue(); // 언박싱(Boolean → boolean)
    	}
    }
    ~~~

  - **프로그래머가 명시적으로 형변환**

    ~~~java
    public static void main(String[] args) {
        Integer intg = new Integer(20);
        int i = (int)intg;
    }
    ~~~

  - **오토언박싱(autounboxing)**

    - 기본 자료형에 래퍼 객체를 대입

    ~~~java
    public class WrapperEx04 {
    	public static void main(String[] args) {
    		int i1 = 10;
    		Integer wi = i1; // 오토 박싱
    		int i2 = wi; // 오토 언박싱
    	}
    }
    ~~~

<br>

--------

**<참조>**

- https://soft.plusblog.co.kr/56
- [[JAVA/자바] 래퍼(Wrapper) 클래스와 박싱(boxing), 언박싱(un-boxing)](https://m.blog.naver.com/PostView.nhn?blogId=heartflow89&logNo=220975218499&proxyReferer=https:%2F%2Fwww.google.com%2F)

- [[Java 강의68]자바 박싱과 언박싱(Boxing, Unboxing)](https://m.blog.naver.com/PostView.nhn?blogId=highkrs&logNo=220530396617&proxyReferer=https:%2F%2Fwww.google.com%2F)