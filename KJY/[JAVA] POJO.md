# [JAVA] POJO

:writing_hand: *Assembled by JiYoung-Kwon (2021-05-30)* 

<br/>

## 1. POJO란?

- **Plain Old Java Object** 의 약자

- 평범하고 오래된 방식의 간단한 자바 객체

- getter/setter를 가진 단순한 자바 오브젝트

- **특별한 제한에 종속되지 않고, 클래스 패스(class path)를 필요로 하지 않는 순수한 Java Object**

- 큰 개념이 있는 것이 아니라, Java EE 등으로 점점 무거워지는 객체에 대한 반발로 나타난 개념

  - 한 마디로 자바로 가볍게 개발하자는 뜻

- 2000년 9월 마틴 파울러 등이 사용하기 시작한 용어

- ```
  "우리는 사람들이 자기네 시스템에 보통의 객체를 사용하는 것을 왜 그렇게 반대하는지 궁금하였는데, 간단한 객체는 폼 나는 명칭이 없기 때문에 그랬던 것으로 결론 지었다. 그래서 적당한 이름을 하나 만들어 붙였더니, 아 글쎄, 다들 좋아하더라고" - 마틴 파울러
  ```

<br/>

#### 1-1. Plain Old Java Object

- 특정 '기술'에 종속되어 동작하는 것이 아닌, 순수한 자바 객체를 말함

- ex) ORM과 POJO

  > ORM (Object Relationship Mapping)
  >
  > - 객체-관계 매핑, 즉 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑해주는 것을 말함
  >   - 자바 ORM의 기술 표준 JPA, 대표적인 오픈 소스에는 Hibernate가 해당됨
  > - 만약 자바 객체가 ORM 기술을 사용하기 위해 Hibernate 프레임워크를 직접 의존하는 순간 POJO라고 할 수 없음
  >   - 특정 '기술'에 종속되었기 때문
  >
  > +) Mybatis는 ORM이 아닌, **SQL 매퍼**임
  >
  > - ORM 프레임워크는 데이터베이스 객체를 자바 객체로 매핑함으로써 객체 간의 관계를 바탕으로 **SQL을 자동으로 생성**해주지만,
  > - Mybatis는 **SQL을 명시**해 주어야 함

<br/>

#### 1-2. POJO가 개발된 이유

- 과거 EJB, Strust같은 프레임워크는 비즈니스 로직을 구현하기 위한 클래스를 코딩할 때, 프레임워크의 특정 인터페이스등의 상속을 강요
  - 그 결과 비지니스 로직을 코딩해야할 시간에 상속을 구현하기 위한 불필요한 코딩작업이 늘어남
  - 이렇게 프레임워크가 비지니스 로직에 특정 프레임워크의 기술에 관련된 코딩을 강제하는 것을 **침투적 프레임워크** 라고 함
- 객체지향의 가장 중요한 개념 중 하나의 **느슨한 의존관계** 를 역행하는 이런 침투적인 프레임워크의 문제점을 강조하고 본래 자바의 장점을 살리기 위해 마틴 파울러가 POJO라는 말을 만듦

<br/>

## 2. POJO의 조건

#### 2-1. POJO의 조건

- 특정 규약에 종속되지 않는다.
  - 어떠한 상속도 받지 않는다.
  - 단일 상속 제한 때문에 객체지향적인 설계기법을 적용하기 어려워진다.
  - 다른 환경으로의 이전이 어렵다.
- 특정 환경에 종속되지 않는다.
  - API를 직접 이용하지 않는다.
  - 다른 환경에서 사용하기 어렵다.
  - 비즈니스 로직과 기술적인 내용을 담은 웹정보 코드가 섞여 이해하기 어려워진다.
  - 웹 서버에 올리지 않고 독립적으로 테스트하기 어려워진다.
- 단일 책임 원칙을 지키는 클래스
  - 책임과 역할이 각기 다른 코드를 하나의 클래스에 넣으면 안된다.

##### 즉, POJO란 객체지향적인 원리에 충실하면서, 특정 환경과 규약에 종속되지 않아 필요에 따라 재사용될 수 잇는 방식으로 설계된 오브젝트라 할 수 있다.

<br/>

#### 2-2. POJO가 아닌 객체

1. 클래스 확장(extends)

   ```java
   public class Foo extends javax.servlet.http.HttpServlet { ...}
   ```

2. 인터페이스 구현(implements)

   ```java
   public class Bar implements javax.ejb.EntityBean { ...}
   ```

3. annotation 포함

   ```java
   @javax.persistence.Entity public class Baz { ...}
   ```

<br/>

#### 2-3. 예시

* POJO를 사용하지 않은 경우

  ```java
  // 특정 환경에 결합도가 높은 코드
  // JMS로 부터 메시지를 받는 경우 --> JMS를 사용하기 위해 MessageListener 인터페이스를 상속받아야 한다.
  
  public class ExampleListener implements MessageListener {
      public void onMessage(Message message){
          if(message instanceof TextMessage){
              try{
                  System.out.println((TextMessage) message).getText());
              } catch(JMSException ex){
                  throw new RuntimeException(ex);
              }
          } else {
              throw new OllegalArgumentException("Message must be o type Text Message");
          }
      }
  }
  ```
* POJO를 사용한 경우

  ```java
  @Component
  public class ExampleListener{
      @JmsListener(destination = "myDestination")
      public void processOrder(String message){
          System.out.println(message);
      }
  }
  ```

  - 위의 코드는 어떠한 인터페이스에 종속되지 않는다.
  - @JmsListener라는 어노테이션을 이용하여 JMS 서비스와 연동한다.
    - 어노테이션의 사용은 어노테이션을 뺐을 때 POJO로 간주되는 경우, POJO로 인정한다.
  - 다른 솔루션을 사용하고 싶은 경우 어노테이션만 바꿔주면 된다.
  - 스프링 프레임워크는 위의 예제처럼 우리의 코드와 라이브러리와의 결합성을 줄이도록 도와준다.

<br/>

## 3. POJO의 장점

* 특정 규약에 종속되지 않아 객체지향 설계를 할 수 있다.
* 특정 환경에 종속되지 않아 테스트하기 좋다.
* 특정 규약에 종속되지 않아 로우 레벨 코드와 비즈니스 코드가 분리되어 깔끔한 코드 작성이 가능하다.

<br/>

## 4. POJO 프레임워크

- Spring은 POJO를 이용한 엔터프라이즈 애플리케이션 개발을 목적으로 하는 프레임워크이다.
- 엔터프라이즈 애플리케이션 개발 중 하나의 예를 들면, DB 이용 기술이 있다.
- DB 이용 기술에 관련된 코드를 객체지향적인 POJO를 기반으로 깔끔하게 구현할 수 있다.

#### 4-1. Spring에서의 POJO

- ![img](https://camo.githubusercontent.com/366a956835c4fc605bfe278454a3893b02cf31df55a9a10c3925ee24ae4a07b0/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393942313536343635423945354443343137)

- Spring 애플리케이션

  - POJO를 이용해서 만든 애플리케이션 로직 + POJO가 어떻게 관계를 맺고 동작하는지 정의해 놓은 설계정보

    - IoC/[DI](https://github.com/shinjeonghea/Inflearn-Spring/blob/main/DI.md), [AOP](https://github.com/shinjeonghea/Inflearn-Spring/blob/main/AOP.md), [PSA](https://siyoon210.tistory.com/120)는 애플리케이션을 POJO로 개발할 수 있게 해주는 기술들

  - Spring 프레임워크는 IoC 컨테이너 안에서 POJO를 구성 및 관리하는 것이 가장 핵심
    - Spring은 POJO를 이용한 엔터프라이즈 애플리케이션 개발을 목적으로 함
      - 엔터프라이즈 애플리케이션 : 사회적 필요를 충족하기 위해 만들어지는 애플리케이션
    - Java EE를 사용할 때에 비해서 특정 인터페이스를 구현하거나 상속 할 필요가 없고, 라이브러리를 지원하기에 용이하며 객체 또한 가벼운 것이 특징

<br/>

## 5. POJO 프로그래밍의 진정한 가치

- **자바의 객체지향적인 특징을 살려 비즈니스 로직에 충실한 개발이 가능하도록 하는 것**
- 그러면서 복잡한 요구조건을 가진 엔터프라이즈 개발의 필요조건을 충족시킬 수 있도록 POJO 기반의 프레임워크를 적절히 사용하는 것이 요구됨
  - 단순히 POJO 프레임워크로 알려진 제품을 사용한다고 POJO 개발이 자동으로 되는 것이 아니라는 것
- POJO 기반의 코드인지 확인하는 **두 가지 중요한 기준**
  1. **객체지향적인 설계원칙에 충실하도록 개발되었는가?**
     - 객체지향언어로서의 자바 오브젝트의 특징을 가지고 있는지가 중요
  2. **테스트 코드 개발의 용이성이나 테스트 코드를 잘 작성했는가?**
     - 잘 만들어진 POJO 애플리케이션은 자동화된 테스트 코드 작성이 편리함
     - 리팩토링할 여유가 생겨 더 나은 설계구조로 변경할 가능성이 높아짐
- **풍성한 도메인 모델**
  - POJO의 특징은 하나의 오브젝트안에 **인스턴스 변수** 와 **로직을 가진 메서드** 를 모두 가지고 있는 것
  - 객체지향 원리에 충실하게 도메인 모델을 만드는 것을 풍성한 도메인 모델이라고 함

<br/>

## 6. JavaBeans와 POJO

- JavaBeans : 데이터를 표현하기 위한 Java 클래스를 만들 때의 규약
- JavaBeans 규칙
  - 모든 클래스의 프로퍼티는 private이며 getter, setter 메소드로 제어한다.
  - 인자가 없는 public 생성자가 있어야 한다.
  - Serializable 인터페이스를 구현해야 한다.
- **Java beans는 POJO이다.**
- **POJO는 Java beans가 아니다.**
- POJO가 Java beans보다 범주가 더 넓은 개념이다.
- Java beans는 더 세부적인 규약이 정해져 있고 이를 지켜야한다.

<br/>

## :page_with_curl: Reference

- https://siyoon210.tistory.com/120
- [https://dreaming-soohyun.tistory.com/entry/JPA%EC%99%80-MyBatis%EC%9D%98-%EC%B0%A8%EC%9D%B4-ORM%EA%B3%BC-SQL-Mapper](https://dreaming-soohyun.tistory.com/entry/JPA와-MyBatis의-차이-ORM과-SQL-Mapper)
- https://gmlwjd9405.github.io/2019/02/01/orm.html
- https://mangkyu.tistory.com/20
- https://okky.kr/article/336882
- [https://happyer16.tistory.com/entry/POJOplain-old-java-object%EB%9E%80](https://happyer16.tistory.com/entry/POJOplain-old-java-object란)
- [POJO - (Plain Old Java Object)란 뭘까?](https://siyoon210.tistory.com/120)
- [POJO 정리](https://velog.io/@dion/what-is-POJO)
- [POJO(Plain old java object)란 무엇인가?](https://happyer16.tistory.com/entry/POJOplain-old-java-object란)
- [포조(Plain Old Java Object, POJO) 이해하기](https://needjarvis.tistory.com/585)
- [java - POJO vs Java Bean](https://www.hanumoka.net/2019/01/06/java-20190106-java-pojo-vs-bean/)
- [[Spring] POJO 란 무엇인가?](https://withseungryu.tistory.com/62)
- [엔터프라이즈 애플리케이션(Enterprise Application)](https://server-engineer.tistory.com/214?category=905015)