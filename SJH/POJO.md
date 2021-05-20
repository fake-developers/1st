# POJO<SMALL>(feat.spring)</SMALL>

- Plain Old Java Object 약자, 평범하고 오랜된 방식의 간단하 자바 객체
- getter/setter를 가진 단순한 자바 오브텍트
- **특별한 제한에 종속되지 않고, 클래스 패스(class path)를 필요로 하지 않는 순수한 Java Object**
- 큰 개념이 있는 것이 아니라 Java EE 등으로 점점 무거워지는 객체에 대한 반발로 나타난 개념

<br>

## POJO가 개발된 이유

- 과거 EJB, Strust같은 프레임워크는 비지니스 로직을 구현하기 위한 클래스를 코딩할 때 프레임워크의 특정 인터페이스등의 상속을 강요
  - 그 결과 비지니스 로직을 코딩해야할 시간에 상속을 구현하기 위한 불필요한 코딩작업이 늘어났다.
  - 이렇게 프레임워크가 비지니스 로직에 특정 프레임워크의 기술에 관련된 코딩을 강제하는 것을 **침투적 프레임워크** 라고 한다.
- 객체지향의 가장 중요한 개념 중 하나의 **느슨한 의존관계** 를 역행하는 이런 침투적인 프레임워크의 문제점을 강조하고 본래 자바의 장점을 살리기 위해 마틴 파울러가 POJO라는 말을 만들었다.

<BR>

## POJO가 아닌 객체

- 위에서 설명했듯이, POJO는 Java 언어 규약에 의해 강제된 것 이외의 제한에 구속되지 않는 Java Object

1. 클래스 확장(extends)

   ~~~java
   public class Foo extends javax.servlet.http.HttpServlet { ...}
   ~~~

2. 인터페이스 구현(implements)

   ~~~java
   public class Bar implements javax.ejb.EntityBean { ...}
   ~~~

3. annotation 포함

   ~~~java
   @javax.persistence.Entity public class Baz { ...}
   ~~~

<br>

## 스프링에서의 POJO

 <img src="https://t1.daumcdn.net/cfile/tistory/99B156465B9E5DC417" height=150>  

- 스프링 애플리케이션 = POJO를 이용해서 만든 애플리케이션 로직 + POJO가 어떻게 관계를 맺고 동작하는지 정의해 놓은 설계정보
  - IoC/[DI](https://github.com/shinjeonghea/Inflearn-Spring/blob/main/DI.md), [AOP](https://github.com/shinjeonghea/Inflearn-Spring/blob/main/AOP.md), [PSA](https://siyoon210.tistory.com/120)는 애플리케이션을 POJO로 개발할 수 있게 해주는 기술들
- 스프링 프레임워크는 IoC 컨테이너 안에서 POJO를 구성 및 관리하는 것이 가장 핵심
  - 스프링은 POJO를 이용한 엔터프라이즈 애플리케이션 개발을 목적으로 한다.
    - 엔터프라이즈 애플리케이션 : 사회적 필요를 충족하기 위해 만들어지는 애플리케이션
  - Java EE를 사용할 때에 비해서 특정 인터페이스를 구현하거나 상속 할 필요가 없고 라이브러리를 지원하기에 용이하며 객체 또한 가벼운 것이 특징이다.

<BR>

## POJO 프로그래밍의 진정한 가치

- **자바의 객체지향적인 특징을 살려 비즈니스 로직에 충실한 개발이 가능하도록 하는 것**
- 그러면서 복잡한 요구조건을 가진 엔터프라이즈 개발의 필요조건을 충족시킬 수 있도록 POJO 기반의 프레임워크를 적절히 사용하는 것이 요구된다.
  - 단순히 POJO 프레임워크로 알려진 제품을 사용한다고 POJO 개발이 자동으로 되는 것이 아니라는 것
- **POJO 기반의 코드인지 확인하는 두 가지 중요한 기준**
  1. 객체지향적인 설계원칙에 충실하도록 개발되었는가?
     - 객체지향언어로서의 자바 오브젝트의 특징을 가지고 있는지가 중요
  2. 테스트 코드 개발의 용이성이나 테스트 코드를 잘 작성했는가?
     - 잘 만들어진 POJO 애플리케이션은 자동화된 테스트 코드 작성이 편리하다.
     - 리팩토링할 여유가 생겨 더 나은 설계구조로 변경할 가능성이 높아진다.
- **풍성한 도메인 모델**
  - POJO의 특징은 하나의 오브젝트안에 **인스턴스 변수** 와 **로직을 가진 메서드** 를 모두 가지고 있는 것
  - 객체지향 원리에 충실하게 도메인 모델을 만드는 것을 풍성한 도메일 모델이라고 한다.

<BR>

##  :pushpin:JavaBeans와 POJO

- JavaBeans는 데이터를 표현하기 위한 Java 클래스를 만들 때의 규약
- JavaBeans 규칙
  - 모든 클래스의 프로퍼티는 private이며 getter, setter 메소드로 제어한다.
  - 인자가 없는 public 생성자가 있어야 한다.
  - Serializable 인터페이스를 구현해야 한다.
- Java beans는 POJO이다.
- POJO는 Java beans가 아니다.
- POJO가 Java beans보다 번주가 더 넓은 개념이다.
- Java beans는 더 세부적인 규약이 정해져 있고 이를 지켜야한다.

<br>

---------------------

**<참조>**

[POJO - (Plain Old Java Object)란 뭘까?](https://siyoon210.tistory.com/120)

[POJO 정리](https://velog.io/@dion/what-is-POJO)

[POJO(Plain old java object)란 무엇인가?](https://happyer16.tistory.com/entry/POJOplain-old-java-object%EB%9E%80)

[포조(Plain Old Java Object, POJO) 이해하기](https://needjarvis.tistory.com/585)

[java - POJO vs Java Bean](https://www.hanumoka.net/2019/01/06/java-20190106-java-pojo-vs-bean/)

[[Spring] POJO 란 무엇인가?](https://withseungryu.tistory.com/62)

[엔터프라이즈 애플리케이션(Enterprise Application)](https://server-engineer.tistory.com/214?category=905015)

