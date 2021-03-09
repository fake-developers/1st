# JAVA 어노테이션

- Java에서 어노테이션은 JEE5부터 새롭게 추가된 요소
- Annotation 사용
  - **데이터의 유효성 검사 등을 쉽게 알 수 있고, 관련 코드가 깔끔**해진다.
  - 소스코드에 **메타데이터(Meta-data)**를 삽입하는 것으로 구독성 뿐만 아니라 체계적인 코드를 구성할 수 있다.
    - 코드는 어노테이션의 구현된 정보에 따라 연결되는 방향이 결정된다.
      - 즉, 어노테이션은 메타 데이터의 일종이라고 볼 수 있다.
    - *메타데이터 : 데이터을 위한 데이터, 한 데이터에 대한 설명을 의미하는 데이터*
- Annotation 용도
  - **컴파일러**를 위한 **정보를 제공**하기 위한 용도
    - ex_) @Override를 통해 내가 지금 작성하고 있는 코드가 부모 클래스에 있는지 검사하라는 의미를 전달
  - **런타임**에 **리플렉션**을 이용해 특수 기능을 추가하기 위한 용도
    - ex_) 스프링 프레임워크에서의 @Controller 어노테이션의 역할과 같다.
    - *리플렉션 : 리플렉션이란 객체를 통해 클래스의 정보를 분석해 내는 프로그램 기법*
  - 컴파일 과정에 어노테이션 정보로부터 코드를 생성하기 위한 용도
- Annotation 사용방식
  - **Java에서 제공하는  Buit-in Annotation**과 **Meta Annotation을 이용해 직접 생성하여 사용하는 Custom Annotation** 두가지가 있다.

<br>

## 자바 에노테이션 문법

- **Annotation 선언**

  `@Annotation`

  - @를 통해서 컴파일러에게 어노테이션임을 알린다.
  - @마크 다음에 오는 문자는 해당 어노테이션의 이름
    - 여기서는 Annotation라는 이름을 가진 에노테이션이라고 생각하면 된다.

- **Annotation 타입**

  - 엘리먼트의 이름 뒤엔느 메서드처럼()를 붙여야하는 규칙이 존재

  1. **마커 어노테이션 (Maker Annotation)**

     - @Override 나 @Deprecated와 같은 어노테이션처럼 표시만 해두는 어노테이션

     - 메서드없이 선언하면 마커 어노테이션이 된다.

     - \<create>

       ~~~java
       public @interface MakerAnnotation {}
       ~~~

     - \<use>

       ~~~java
       @MakerAnnotation
       public class UsingMakerAnnotation {
       }
       ~~~

       - 추가 정보 없이 클래스나 메서드위에 추가한다.

  2. **싱글 값 어노테이션 (Single Value Annotation)**

     - 하나의 값만 입력받을 수 있는 어노테이션

     - 멤버로 단일변수만을 갖는다. 단일변수 밖에 없기때문에 값을 병시하여 데이터를 전달

     - \<create>

       ~~~java
       public @interface SingleValueAnnotation {
           int id();
       }
       ~~~

       - 어노테이션 선언에 하나의 값만 존재한다.

     - \<use>

       ~~~java
       @SingleValueAnnotation(id = 1)
       public class UsingSingleValueAnnotation {
       }
       ~~~

  3. **멀티 값 어노테이션 (Multi Value Annotation)**

     - 요소가 둘 이상의 변수를 갖는 어노테이션

     - 데이터를  key-value 형태로 전달한다

       - 데이터가 Array인 경우 "{ }" 이용

     - \<create>

       ~~~java
       public @interface TestAnnotation {
       	String doSomething();
       	int count default 5;
       	String date();
       }
       ~~~

     - \<use>

       ~~~java
       @TestAnnotation(doSomething="What to do", count=1, date="09-09-2019")
       public void setMethode() {
       		...
       }
       ~~~

       - count의 경우 default를 정의하여 값 생략 가능

- **Annotation 위치**

  - 어노테이션은 클래스, 인터페이스, 메소드, 메소드 파리미터, 필드, 지역 변수 위에 위치할 수 있다.

    ~~~java
    @Annotation
    public class AnnotationPlacement {
    
        @Annotation
        String field;
    
        @Annotation
        public void method1(@MakerAnnotation String str) {
            @MakerAnnotation
            String test;
        }
    }
    ~~~

<br>

## Built-in Annotation

- 이미 java에 내장되어 있는 어노테이션

- 주로 컴파일러를 위한 것으로 **컴파일러에게 정보를 제공**한다.

  **@Override**

  - 선언한 메서드가 오버라이드(재정의) 되었다는 것을 나타낸다.

  - 만약 상위(부모) 클래스(또는 인터페이스)에서 해당 메서드를 찾을 수 없다면 컴파일 에러를 발생 시킨다.

  **@Deprecated**

  - 해당 메서드가 더 이상 사용되지 않음을 표시한다.

  - 만약 사용할 경우 컴파일 경고를 발생 시킨다.
  
  **@SuppressWarnings**

  - 선언한 곳의 컴파일 경고를 무시하게 한다.

  **@SafeVarargs**

  - Java7 부터 지원하며, 제너릭 같은 가변인자의 매개변수를 사용할 때의 경고를 무시한다. 

  **@FunctionalInterface**

  - Java8 부터 지원하며, 함수형 인터페이스를 지정하는 어노테이션이다..

  - 만약 메소드가 존재하지 않거나, 1개 이상의 메소드(default 메소드 제외)가 존재할 경우 컴파일 오류를 발생시킨다

<br>

## Mata Annotation

- 어노테이션에 사용되는 어노테이션으로 해당 어노테이션의 동작 대상을 결정한다.

- 주로 새로운 어노테이션을 정의할 때 사용한다.

  **@Retention**

  -  자바 컴파일러가 어노테이션을 다루는 방법을 기술하며, 어노테이션이 유지되는 기간을 지정하는데  사용한다.

  - 세 가지 **유지 정책(retention policy)** 사용 가능

    - 어노테이션 유지 정책 : 어노테이션 유지범위를 설정하는 방법

        **RetentionPolicy.SOURCE** : 컴파일 전까지만 유효. (컴파일 이후에는 사라짐)

        **RetentionPolicy.CLASS** : 컴파일러가 클래스를 참조할 때까지 유효.

        **RetentionPolicy.RUNTIME** : 런타임시까지 계속 유효. 컴파일 이후에도 JVM에 의해 계속 참조가 가능. (리플렉션 사용) 

    ~~~java
    @Retention(RetentionPolicy.RUNTIME)
    public @interface AnnotationName { ... } 
    ~~~

    - @Retention을 이용해 리플렉션 기능으로 런타임시 어노테이션 정보를 얻게 함

  **@Target**   

  - 어노테이션이 적용할 위치를 지정합니다.

  - 여러 개의 값을 지정할 때는 배열에서 처럼 괄호 { } 를 사용한다.

    **ElementType.PACKAGE** : 패키지 선언
    
    **ElementType.TYPE** : class, interface, enum에 적용
    
    **ElementType.ANNOTATION_TYPE** : 어노테이션 타입 선언
    
    **ElementType.CONSTRUCTOR** : 생성자
    
    **ElementType.FIELD** : 멤버 변수
    
    **ElementType.LOCAL_VARIABLE** : 지역 변수 선언
    
    **ElementType.METHOD** : 메서드
    
    **ElementType.PARAMETER** : 전달인자 선언
    
    **ElementType.TYPE_PARAMETER** : 자바 8부터 추가, 제네릭 타입 변수
    
    **ElementType.TYPE_USE** : 어떤 타입에도 적용
    
    ~~~java
    @Target({ElementType.METHOD})
    public @interface AnnotationName { ... } 
    ~~~
    
    - Method에서만 사용가능한 어노테이션 정의
  
  **@Documented**
  
  - 해당 어노테이션을 javadoc에 포함시킨다.
  
  **@Inherited**  
  
  - 어노테이션의 상속을 가능하게 한다.
  
  **@Repeatable**
  
  - Java 8 부터 지원하며, 연속적으로 어노테이션을 사용할 수 있게 한다.

<br>

## Custom Annotation

- 개발자가 직접 작성한 어노테이션으로, **메타 어노테이션**을 이용한다.

- 어노테이션 필드에서는 enum,String 이나 기본 자료형, 기본 자료형 배열을 사용가능하다.

- ex_)

  ~~~java
  public @interface AnnotationName { ... } 
  ~~~

  - 어노테이션은 기본적으로 인터페이스 형태를 취하고 있으며, 단지 interface 앞에 @표시를 한다.
  - 어노테이션을 선언했지만 런타임시 컴파일러가 해당 코드를 읽지 못함
  - 위의 Meta annotation들을 이용하여 응용한다.

- ex_) 클래스 선언 예제

  ~~~java
  @Retention(RetentionPolicy.RUNTIME)
  @Target(ElementType.TYPE)
  public @interface MyAnnotation {
      String name();
      String value();
  }
  
  @MyAnnotation(name = "someName", value = "Hello World")
  public class TheClass {
  }
  ~~~

- ex_) 클래스 필드 선언 예제

  ~~~java
  @Retention(RetentionPolicy.RUNTIME)
  @Target(ElementType.FIELD)
  public @interface MyAnnotation {
      String name();
      String value();
  }
  
  public class TheClass {
      @MyAnnotation(name = "someName", value = "Hello World")
      public String myField = null;
  }
  ~~~

----------

**<참조>**

- [Java에서 어노테이션(Annotation)이란?](https://elfinlas.github.io/2017/12/14/java-annotation/)
- [1. 자바 어노테이션 기본 문법](https://hamait.tistory.com/314)
- [[JAVA]어노테이션(Annotation) - 1](https://sassun.tistory.com/57)

- [JAVA @어노테이션이란?](https://simostory.tistory.com/32)
- [자바 커스텀 어노테이션 만들기](https://advenoh.tistory.com/21)