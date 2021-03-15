# [JAVA] Annotation

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-14)* 

<br/>

## 1. Java Annotation

- 어노테이션 : 본래 주석이란 뜻으로, **인터페이스를 기반으로 한 문법** (하지만 주석과는 역할이 다름)
- 주석처럼 코드에 달아 메타 데이터(Meta-data)를 삽입하여, 클래스에 특별한 의미를 부여하거나 기능을 주입할 수 있음
  - 메타데이터 : 데이터를 위한 데이터, 한 데이터에 대한 설명을 의미하는 데이터
- 해석되는 시점을 정할 수 있음
  - 코드는 어노테이션의 구현된 정보에 따라 연결되는 방향이 결정됨
    - 즉, 어노테이션은 메타 데이터의 일종이라고 볼 수 있음
- Java에서 어노테이션은 JEE5부터 새롭게 추가된 요소

* **데이터의 유효성 검사 등을 쉽게 알 수 있고, 관련 코드가 깔끔**해짐

- 어노테이션에는 크게 세 가지 종류가 존재
  - **Built-in annotation** : JDK에 내장되어 있는 어노테이션
  - **Meta annotation** : 어노테이션에 대한 정보를 나타내기 위한 어노테이션
  - **Custom Annotation** : 개발자가 직접 만들어내는 어노테이션

<br/>

#### 1-1. Annotation의 특징

- AOP (Aspect Oriented Programming : 관점 지향 프로그래밍) 을 편리하게 구성할 수 있음
- 컴파일러에게 코드 문법 에러를 체크하도록 정보를 제공함
- 소프트웨어 개발 툴이 빌드나 배치 시에 코드를 자동으로 생성할 수 있도록 정보를 제공함
- 어노테이션을 만들 때 용도를 분명하게 해야 함
  - **소스상에서만 유지해야 할지**
  - **컴파일된 클래스에도 유지해야 할지**
  - **런타임 시에도 유지해야 할지**

<br/>

#### 1-2. Annotation 용도

- **컴파일러를 위한 정보를 제공하기** 위한 용도
  - ex) @Override를 통해 내가 지금 작성하고 있는 코드가 부모 클래스에 있는지 검사하라는 의미를 전달
- **런타임에 리플렉션을 이용해 특수 기능을 추가하기** 위한 용도
  - ex) 스프링 프레임워크에서의 @Controller 어노테이션의 역할과 같음
  - *리플렉션 : 객체를 통해 클래스의 정보를 분석해 내는 프로그램 기법*
- **컴파일 과정에 어노테이션 정보로부터 코드를 생성하기** 위한 용도

<br/>

## 2. Annotation 문법

#### 2-1. Annotation 선언

* `@Annotation`

- @를 이용하여 컴파일러에게 어노테이션임을 알림
- @마크 다음에 오는 문자는 해당 어노테이션의 이름

<br/>

#### 2-2. Annotation의 타입

- 엘리먼트의 이름 뒤에는 메서드처럼 ()를 붙여야하는 규칙이 존재함

1. **마커 어노테이션 (Maker Annotation)**

   - `@Override`나 `@Deprecated`와 같은 어노테이션처럼 **표시만 해두는 어노테이션**

   ```java
   // create - 메서드 없이 선언하면 머커 어노테이션이 됨
   public @interface MakerAnnotation {}
   
   // use - 추가 정보 없이 클래스나 메서드 위에 추가함
   @MakerAnnotation
   public class UsingMakerAnnotation{
   }
   ```

2. **싱글 값 어노테이션 (Single Value Annotation)**
   
   * 하나의 값만 입력 받을 수 있는 어노테이션
* 멤버로 단일 변수만을 갖고, 값을 명시하여 데이터를 전달함
   
   ```java
   // create
   public @interface SingleValueAnnotation{
       int id(); // 어노테이션 선언에 하나의 값만 존재
   }
   
   // use
   @SingleValueAnnotation(id = 1)
   public calss UsingSingleValueAnnotation{
       
   }
   ```

3. **멀티 값 어노테이션 (Multi Value Annotation)**

   - 둘 이상의 변수를 갖는 어노테이션
   - 데이터를 key-value 형태로 전달함
     - 데이터가 Array인 경우 '{}' 를 이용

   ```java
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

   - count의 경우 default를 정의함 -> 사용 시 값을 생략할 수 있음

<br/>

#### 2-3. Annotation의 위치

- 어노테이션은 클래스, 인터페이스, 메소드, 메소드 파라미터, 필드, 지역 변수 위에 위치할 수 있음

```java
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

## 3. Built-in Annotation

* 이미 java에 내장되어 있는 어노테이션

* 주로 컴파일러를 위한 것으로 **컴파일러에게 정보를 제공함**

  **@Override**

  - 선언한 메서드가 오버라이드(재정의) 되었다는 것을 나타냄
  - 만약 상위(부모) 클래스(또는 인터페이스)에서 해당 메서드를 찾을 수 없다면, 컴파일 에러를 발생시킴

  **@Deprecated**

  - 해당 메서드가 더 이상 사용되지 않음을 표시함
  - 만약 사용할 경우, 컴파일 경고를 발생시킴

  **@SuppressWarnings**

  - 선언한 곳의 컴파일 경고를 무시하게 함

  **@SafeVarargs**

  - Java7 부터 지원하며, 제너릭 같은 가변인자의 매개변수를 사용할 때의 경고를 무시함

  **@FunctionalInterface**

  - Java8 부터 지원하며, 함수형 인터페이스를 지정하는 어노테이션
  - 만약 메소드가 존재하지 않거나, 1개 이상의 메소드(default 메소드 제외)가 존재할 경우, 컴파일 오류를 발생시킴

<br/>

## 4. Meta Annotation

- 어노테이션에 사용되는 어노테이션

- 해당 어노테이션의 동작 대상을 결정함

- 주로 새로운 어노테이션을 정의할 때 사용함

  **@Retention**

  - 자바 컴파일러가 어노테이션을 다루는 방법을 기술하며, 어노테이션이 유지되는 기간을 지정하는데 사용

  - value 값으로는 RetentionPolicy 에 enum 상수인 다음의 값들을 사용

  - 세 가지 **유지 정책(retention policy)**

    - 어노테이션 유지 정책 : 어노테이션 유지범위를 설정하는 방법

      1. **RetentionPolicy.SOURCE** : 컴파일 전까지만 유효 (컴파일 이후에는 사라짐)

      2. **RetentionPolicy.CLASS** : 컴파일러가 클래스를 참조할 때까지 유효

      3. **RetentionPolicy.RUNTIME** : 런타임시까지 계속 유효 (컴파일 이후에도 JVM에 의해 계속 참조가 가능) (리플렉션 사용)

    ```java
    @Retention(RetentionPolicy.RUNTIME)
    public @interface AnnotationName { ... } 
    ```

    - @Retention을 이용해 리플렉션 기능으로 런타임시 어노테이션 정보를 얻게 함

  **@Target**

  - 적용할 위치와 대상을 지정

  - 여러 개의 값을 지정할 때는 배열에서 처럼 괄호 { } 를 사용

  - value 값으로는 ElementType에 enum 상수인 다음의 값들을 사용할 수 있음

    **ElementType.PACKAGE** : 패키지 선언

    **ElementType.TYPE** : class, interface, enum에 적용 (타입 선언)

    **ElementType.ANNOTATION_TYPE** : 어노테이션 타입 선언

    **ElementType.CONSTRUCTOR** : 생성자 선언

    **ElementType.FIELD** : 멤버 변수 선언

    **ElementType.LOCAL_VARIABLE** : 지역 변수 선언

    **ElementType.METHOD** : 메서드 선언

    **ElementType.PARAMETER** : 전달인자 선언

    **ElementType.TYPE_PARAMETER** : 자바 8부터 추가, 제네릭 타입 변수 

    **ElementType.TYPE_USE** : 어떤 타입에도 적용

    ```java
    @Target({ElementType.METHOD, ElementType.Field})
    public @interface AnnotationName { ... } 
    ```

    - Method, 멤버 변수에서만 사용 가능한 어노테이션 정의

  **@Documented**

  - 해당 어노테이션을 javadoc에 포함시킴 (문서에 어노테이션 정보 표현)

  **@Inherited**

  - 자식 클래스가 어노테이션을 상속 받을 수 있게 함

  **@Repeatable**

  - Java 8 부터 지원하며, 반복적으로 어노테이션을 선언할 수 있게 함

<br/>

## 5. Custom Annotation

- 개발자가 직접 작성한 어노테이션

- **메타 어노테이션**을 이용함

- 어노테이션 필드에서는 enum, String 이나 기본 자료형, 기본 자료형 배열을 사용 가능함

- 메소드 선언에 throws 절이 없어야 함

- 반환 유형은 Primitives, String, Class, enums, annotation, array 등으로 제한됨

- ex)

  ```java
  public @interface AnnotationName { ... } 
  ```

  - 어노테이션은 기본적으로 인터페이스 형태를 취하고 있으며, interface 앞에 @표시를 함
  - 어노테이션을 선언했지만 런타임시 컴파일러가 해당 코드를 읽지 못함
  - 위의 Meta annotation들을 이용하여 응용함

- ex) 클래스 선언 예제

  ```java
  @Retention(RetentionPolicy.RUNTIME)
  @Target(ElementType.TYPE)
  public @interface MyAnnotation {
      String name();
      String value();
  }
  
  @MyAnnotation(name = "someName", value = "Hello World")
  public class TheClass {
  }
  ```

- ex) 클래스 필드 선언 예제

  ```java
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
  ```

<br/>

## 6. Annotation과 Retention

- 어노테이션 자체는 언제 어디서 사용될 수 있는지 나타내기 위해서 주석을 달 수 있음
- 사용자 정의 클래스 및 메소드에 동작을 편리하게 적용하는 방법으로 프레임워크에서 자주 사용됨
- Java 소스 코드가 컴파일되면 Annotation processor라는 컴파일러 플러그인이 annotation을 처리할 수 있음
  - 이 processor는 정보 메시지를 생성하거나 java 소스 파일이나 리소스를 추가로 생성할 수 있고, 컴파일 및 처리와 어노테이션이 달린 코드 수정도 가능함
  - 자바 컴파일러는 어노테이션이 클래스 또는 RUNTIME의 RetentionPolicy를 갖는 경우, 조건부로 메타 데이터를 .class 파일에 저장함
    - 이로써 나중에 JVM 또는 다른 프로그램이 메타 데이터를 찾아 프로그램 요소와 상호작용하거나 동작을 변경하는 방법을 결정할 수 있음
    - 그래서 어노테이션을 정의할 때 @Retention(RetentionPolicy.RUNTIME)을 써주어야 함
<br/>

## :page_with_curl: Reference

https://k39335.tistory.com/40

[https://khj93.tistory.com/entry/JAVA-%EB%9E%8C%EB%8B%A4%EC%8B%9DRambda%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%82%AC%EC%9A%A9%EB%B2%95](https://khj93.tistory.com/entry/JAVA-람다식Rambda란-무엇이고-사용법)

https://nesoy.github.io/articles/2018-04/Java-Annotation

https://qssdev.tistory.com/27

https://blueyikim.tistory.com/147

[Java에서 어노테이션(Annotation)이란?](https://elfinlas.github.io/2017/12/14/java-annotation/)

[1. 자바 어노테이션 기본 문법](https://hamait.tistory.com/314)

[[JAVA]어노테이션(Annotation) - 1](https://sassun.tistory.com/57)

[JAVA @어노테이션이란?](https://simostory.tistory.com/32)

[자바 커스텀 어노테이션 만들기](https://advenoh.tistory.com/21)
