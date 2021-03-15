# Java Annotation

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JeongHea Shin*

<hr>



## Java Annotation


- <b>Annotation (어노테이션) 이란?</b>
  - 어노테이션이란 본래 주석이란 뜻으로, 인터페이스를 기반으로 한 문법이다.
  - 주석과는 역할이 다르다.
    - 주석처럼 코드에 달아 메타 데이터를 삽입하여, 클래스에 특별한 의미를 부여하거나 기능을 주입할 수 있다.
    - 또한, 해석되는 시점을 정할 수 있다.

    \* 메타데이터 : 데이터를 위한 데이터, 한 데이터에 대한 설명을 의미하는 데이터
  - 어노테이션에는 크게 세 가지 종류가 존재한다.
    - Built-int annotation : JDK에 내장되어 있는 어노테이션
    - Meta annotation : 어노테이션에 대한 정보를 나타내기 위한 어노테이션
    - Custom Annotation : 개발자가 직접 만들어내는 어노테이션

<br/>

<br/>

- <b>Annotation의 특징</b>
  - AOP (Aspect Oriented Programming : 관점 지향 프로그래밍) 을 편리하게 구성할 수 있다.
  - 컴파일러에게 코드 문법 에러를 체크하도록 정보를 제공한다.
  - 소프트웨어 개발 툴이 빌드나 배치 시에 코드를 자동으로 생성할 수 있도록 정보를 제공한다.
  - 어노테이션을 만들 때 용도를 분명하게 해야한다.
    - 소스상에서만 유지해야 할지
    - 컴파일된 클래스에도 유지해야 할지
    - 런타임 시에도 유지해야 할지

<br/>

<br/>

#### Annotation 문법

- <b>Annotation 선언</b>

  <code>@Annotation</code>

  - @를 이용하여 컴파일러에게 어노테이션임을 알린다.
  - @ 마크 다음에 오는 문자는 해당 어노테이션의 이름이다.

  <br/>

  <br/>

- <b>Annotation의 타입</b>

  - 엘리먼트의 이름 뒤에는 메서드처럼()를 붙여야하는 규칙이 존재한다.

  <br/>

  1. 마커 어노테이션 (Maker Annotation)

     - <code>@Override</code>나 <code>@Deprecated</code>와 같은 어노테이션처럼 표시만 해두는 어노테이션이다.
     - 메서드 없이 선언하면 머커 어노테이션이 된다.

     ``` java
     // create
     public @interface MakerAnnotation {}
     
     // use
     @MakerAnnotation
     public class UsingMakerAnnotation{
         
     }
     ```

     - 추가 정보 없이 클래스나 메서드 위에 추가한다.

  <br/>

  <br/>

  2. 싱글 값 어노테이션 (Single Value Annotation)

     - 하나의 값만 입력 받을 수 있는 어노테이션
     - 멤버로 단일 변수만을 갖고, 값을 명시하여 데이터를 전달한다.

     ``` java
     // create
     public @interface SingleValueAnnotation{
         int id(); // 어노테이션 선언에 하나의 값만 존재
     }
     
     // use
     @SingleValueAnnotation(id = 1)
     public calss UsingSingleValueAnnotation{
         
     }
     ```

  <br/>

  <br/>

  3. 멀티 값 어노테이션 (Multi Value Annotation)

     - 둘 이상의 변수를 갖는 어노테이션
     - 데이터를 key-value 형태로 전달한다. 
       - 데이터가 Array인 경우 '{}' 를 이용한다.

     ``` java
     // create
     public @interface TestAnnotation{
         String doSomething();
         int count default 5;
         String date();
     }
     
     // use
     @TestAnnotation(doSomething="What to do", count = 1, date = "09-09-2019")
     public void setMethod() {
         
     }
     ```

     - count의 경우 default를 정의해두었기 때문에 값을 생략할 수 있다.

<br/>

<br/>

<br/>

- <b>Annotation의 위치</b>

  - 어노테이션은 클래스, 인터페이스, 메소드, 메소드 파라미터, 필드, 지역 변수 위에 위치할 수 있다.

  ``` java
  @Annotation // 클래스
  public class AnnotationPlacement {
      
      @Annotation // 필드
      String field;
      
      @Annotation // 메소드
      public void method1(@MakerAnnotation String str){ // 메소드 파라미터
          @MakerAnnotation // 지역변수
          String test;
      }
  }
  ```

  

<br/>

#### Java Annotation 종류

- <b>Built-in Annotations</b>

  1. <code>@Override</code>
     - 메소드 선언하며 지정한 메소드가 부모 클래스로부터 오버라이드된 메소드임을 명시한다.
     - 메소드가 오버라이드 되었는지 검증한다.
       - 만약 부모 클래스 또는 구현해야할 인터페이스에서 해당 메소드를 찾을 수 없다면 컴파일 오류가 발생한다.

  <br/>

  2. <code>@Deprecated</code>
     - 클래스, 메소드, 필드 등에 선언한다.
     - 지정한 요소가 더이상 사용되지 않음을 의미한다.
     - 만약 사용한다면 컴파일 경고를 일으킨다.

  <br/>

  3. <code>@SuppressWarnings</code>
     - 클래스, 메소드, 필드 등에 선언한다.
     - 선언한 영역에서 발생한 컴파일러의 경고를 제거하여 무시하도록 한다.

  <br/>

  4. <code>@SafeVarags</code>
     - 제네릭 같은 가변인자 매개변수를 사용할 때 경고를 무시한다. (자바 7 이상)

  <br/>

  5. <code>@FunctionalInterface</code>

     - 람다 함수 등을 위한 인터페이스를 지정한다.

     - 메소드가 없거나 두개 이상이 되면 컴파일 오류가 난다. (자바 8 이상)

       > 람다 함수
       >
       > - 익명 함수 (Anonymous functions)를 지칭하는 용어
       > - 메소드 이름 없이 몸체만 구현하여 코드를 간결하게 한다.

  <br/>

<br/>

- <b>Meta Annotations</b>

  <small>\* Meta Annotation을 활용하여 Custom Annotation을 만들 수 있다.</small>

  1. <code>@Retention</code>

     - 어노테이션의 정보가 언제까지 유지될지를 지정한다.

     - value 값으로는 RetentionPolicy 에 enum 상수인 다음의 값들을 사용한다. 

       ``` java
       @Retention(RetentionPolicy.RUNTIME) // 소스, 클래스, 실행 시에 사용됨
       @Retention(RetentionPolicy.CLASS) // 소스와 클래스에서 사용됨
       @Retention(RetentionPolicy.SOURCE) // 소스에서만 사용됨
       ```

       <br/>

  2. <code>@Documented</code>

     - 문서에도 어노테이션의 정보가 표현된다.

     <br/>

  3. <code>@Target</code>

     - 적용할 위치와 대상을 지정한다.
     - value 값으로는 ElemntType에 enum 상수인 다음의 값들을 사용할 수 있다.

     ``` java
     @Target({
         ElementType.PACKAGE, // 패키지 선언 시
         ElementType.TYPE, // 타입 선언 시
        	ElementType.CONSTRUCTOR, // 생성자 선언 시
     	ElementType.FIELD, // 멤버 변수 선언 시
     	ElementType.METHOD, // 메소드 선언 시
     	ElementType.ANNOTATION_TYPE, // 어노테이션 타입 선언 시
     	ElementType.LOCAL_VARIABLE, // 지역 변수 선언 시
     	ElementType.PARAMETER, // 매개 변수 선언 시
     	ElementType.TYPE_PARAMETER, // 매개 변수 타입 선언 시
     	ElementType.TYPE_USE // 타입 사용 시
     })
     ```

     

     <br/>

  4. <code>@Inherited</code>

     - 자식 클래스가 어노테이션을 상속 받을 수 있다.

     <br/>

  5. <code>@Repeatable</code>

     - 반복적으로 어노테이션을 선언할 수 있게 한다.

<br/>

<br/>

- <b>Custom Annotation</b>

  - Annotation의 선언은 일반 인터페이스 선언과 유사하다.
    - @가 interface 키워드 앞에 온다.
  - 메소드 선언에 throws 절이 없어야 한다.
  - 반환 유형은 Primitives, String, Class, enums, annotation, array 등으로 제한된다.

  ``` java
  // Maker.java
  // Maker라는 Cunstom Annotation을 정의하는 소스파일
  // interface 앞에 @ 문자를 지정해줌
  import java.lang.annotation.*;
  
  @Retention(RetentionPolicy.RUNTIME)
  public @interface Maker{
      int num() default 1;
      String name();
      String date() default "2021-03-10";
  }
  ```

  

  ``` java
  // AnnTest.java
  // @Maker Annotation을 테스트하는 소스파일
  
  import java.lang.annotation.Annotation;
  
  @Maker(num = 9, name = "james") // num과 name만 설정됨 (date는 설정되지 않아 default 값이 표시됨)
  public class AnnTest {
      public static void main(String[] args){
          Class<AnnTest> obj = AnnTest.class;
          
          Maker maker = (Maker) obj.getAnnotation(Maker.class);
          
          System.out.println("num : " + maker.num());
          System.out.println("name : " + maker.name());
          System.out.println("date : " + maker.date());
      }
  }
  
  // 결과 
  // num : 9
  // name : james
  // date : 2021-03-10
  ```

  <br/>

  <br/>

  <br/>

#### Annotation과 Retention

- 어노테이션 자체는 언제 어디서 사용될 수 있는지 나타내기 위해서 주석을 달 수 있다.

- 사용자 정의 클래스 및 메소드에 동작을 편리하게 적용하는 방법으로 프레임워크에서 자주 사용된다.

- Java 소스 코드가 컴파일되면 Annotation processor라는 컴파일러 플러그인이 annotation을 처리할 수 있다.

  - 이 processor는 정보 메시지를 생성하거느 java 소스 파일이나 리소스를 추가로 생성할 수 있고, 컴파일 및 처리와 어노테이션이 달린 코드 수정도 가능하다.

  - 자바 컴파일러는 어노테이션이 클래스 또는 RUNTIME의 RetentionPolicy를 갖는 경우, 조건부로 메타 데이터를 .class 파일에 저장한다. 
    - 이로써 나중에 JVM 또는 다른 프로그램이 메타 데이터를 찾아 프로그램 요소와 상호작용하거나 동작을 변경하는 방법을 결정할 수 있다.
    - 그래서 어노테이션을 정의할 때 @Retention(RetentionPolicy.RUNTIME)을 써주어야 한다. 

<br/>

<br/>

<br/>

## 예상질문❔

Q1) 자바에서 Annotation이란 무엇인가?

A1) 주석처럼 코드에 달아 메타 데이터를 삽입하여, 클래스에 특별한 의미를 부여하거나 기능을 주입할 수 있다.

<br/>

Q2) Annotation의 사용 이점은 무엇인가?

A2) 컴파일러에게 컴파일을 위한 정보를 제공하고, 데이터의 유효성 검사 등을 쉽게 알수 있다. 또한 코드가 간결해진다는 장점이 있다.

<br/>

<br/>

### Reference📖

- https://k39335.tistory.com/40
- https://khj93.tistory.com/entry/JAVA-%EB%9E%8C%EB%8B%A4%EC%8B%9DRambda%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%82%AC%EC%9A%A9%EB%B2%95
- https://nesoy.github.io/articles/2018-04/Java-Annotation
- https://qssdev.tistory.com/27
- https://blueyikim.tistory.com/147

