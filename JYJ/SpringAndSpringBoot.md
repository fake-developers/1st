# 스프링과 스프링 부트의 차이

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYoung Kwon*

<hr>

- <small><참고></small>라이브러리와 프레임워크의 차이

  - <b>라이브러리</b>

    - 특정 기능을 하는 간단한 코드(도구)의 집합이다.
    - 개발자가 만든 클래스에서 호출하여 원하는 기능을 사용한다.
    - <b>사용자가 전체적인 흐름을 만들고, 그 안에 라이브러리를 가져다 사용한다.</b>

    <br/>

  - <b>프레임워크</b>

    - 라이브러리를 포함하는 개념으로 프로그래밍 방법을 제공한다. 

    - 개발자는 개발 방법에 맞추어 개발한다.

      <b>--> 전체적인 흐름을 프레임워크가 쥐고, 사용자는 그 안에서 필요 코드를 짜 넣는 제어의 역전이 일어난다. (IOC*)</b>

    - 객체 지향 개발의 통합성, 일관성 부족 문제를 해결할 방법 중 하나이다.

    <br/>

    <img src='resources/spring.jpg' align='center' width='450px'>

<br/>

- Spring 이란?

    - 스프링 프레임워크는 자바 플랫폼을 위한 오픈 소스 애플리케이션 프레임워크이다.

      > 애플리케이션 프레임워크
      >
      > ~~~
      > 특정 계층이나, 기술, 업무 분야에 국한되지 않고 애플리케이션의 전 영역을 포괄하는 프레임워크
      > ~~~

    - 동적 웹 사이트를 개발하기 위한 여러가지 서비스를 제공하고 있다.

      <small>+) 대한민국 공공기관 웹 서비스 개발 시 사용을 권장하고 있는 전자정부 표준 프레임워크의 기반 기술이다.</small>

  <br/>

- Spring의 특성

  - 개발자가 코드안에 애플리케이션 동작에 대한 내용을 기술하면 스프링 프레임워크가 이를 해석하여 동작한다.
  - 가장 일반적인 사용 예로 Servlet API가 있다.
    - 개발자가 API 처리 클래스를 정의하고, 이것이 Servlet API를 위한 클래스임을 어노테이션으로 표시한다.
    - 그 이후 프로그램을 실행하면 스프링은 API 요청이 들어올 때 해당 클래스를 이용하여 처리한다.
    - Servlet 관련된 것은 개발하지 않아도 스프링이 데이터 바인딩, 객체 생성 등 알아서 해준다.

<br/>

- Spring의 장단점 

  - 장점

    - 경량 컨테이너이다.

    - 의존성 주입(DI)*과 제어의 역전(IOC)\* 특성을 이용하여 <mark>결합도를 낮추는 방식</mark>으로 개발이 가능하다.

      <small>* DI(Dependency Injection) : 객체 자체가 아니라 프레임워크에 의해 객체의 의존성이 주입되는 패턴, 컨테이너가 bean을 생성하고 주입한다.</small>

      <small>* IOC(Invertion of Control) : 중앙에 객체를 관리하는 기능을 몰아두어 container라는 객체가 생성에서 소멸까지의 control을 관리한다. 다른 객체들은 container로 부터 가져다 쓰고, 반납하고를 반복한다. --> 공유경제</small>

    - 관점 지향 프로그래밍(AOP)* 가 가능하다.

      <small>* AOP(Aspect Oriented Programming) : OOP(object oriented programming) 에서 객체의 면을 바라보는 관점, 핵심 기능과 공통 기능을 분리 시키고 공통 기능을 필요로하는 핵심 기능들에서 사용하는 방법</small>

    - 단위테스트가 용이하여 퀄리티 높은 프로그램 개발이 가능하다.

  <br/>

  - 단점(Spring Boot가 나온 계기)
    - 사용 전 많은 환경 설정이 필요하다.

<br/>

- Spring Boot란?

  - 스프링 프레임워크라는 큰 틀에 속하는 도구로, 스프링 프레임워크의 복잡한 환경설정을 보완하였다.

  - 스프링 프레임워크를 사용하기 위한 설정의 상당수를 자동화한 것이다. 

    <small>--> 환경 설정의 최소화로, 사용자가 해야할 부분을 Spring Boot가 해준다.</small>

  - 실행 환경이나 의존성 관리 등의 인프라 관련 등은 신경 쓸 필요 없이 코딩을 시작할 수 있다. <small>--> 개발자는 비즈니스 로직에만 집중할 수 있다.</small>

  - 스프링을 처음 사용하거나 웹 애플리케이션 서버를 간단히 만들 때 사용하면 빠르고 간편하다.

<br/>

- Spring과 Spring Boot의 차이
  - Spring Boot에는 <mark>Tomcat이 내장</mark>되어 있어 따로 Tomcat을 설치하거나 버전을 관리하는 수고를 덜어준다.
  - Spring Boot는 starter를 통한 dependency 를 자동화한다.
    - 스프링 프레임워크에서는 각각의 dependency 들의 호환 버전을 일일이 맞춰주어야 다른 dependency에 영향을 미치지 않아서 버전 관리에 어려움이 많았다.
    - spring-boot-starter-\*만 추가해주면 관련된 필요 라이브러리들을 알아서 받아온다.
  - Spring Boot는 XML 설정을 하지 않아도 된다.
  - Spring Boot는 jar file을 이용해 자바 옵션만으로 손쉽게 배포가 가능하다.
  - Spring Boot는 Spring Actuator을 이용한 애플리케이션의 모니터링과 관리를 제공한다.

<br/>

## 예상질문❔

Q1) Spring과 Spring Boot의 차이는 무엇인가?

A1) Spring framework의 초기 환경 설정의 복잡성을 해결하기 위해 나온 것이 Spring Boot로, 환경 설정을 자동화하여 starter dependency만 추가하면 관련된 라이브러리를 알아서 받아온다.

<br/>

### Reference📖

- https://sas-study.tistory.com/274
- https://monkey3199.github.io/develop/spring/2019/04/14/Spring-And-SpringBoot.html
- https://ooeunz.tistory.com/56
- https://gmlwjd9405.github.io/2018/11/09/dependency-injection.html (DI, IOC)
- https://hongku.tistory.com/114 (AOP)
- https://velog.io/@max9106/Spring-AOP%EB%9E%80-93k5zjsm95 (AOP)
