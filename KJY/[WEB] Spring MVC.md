# [WEB] Spring MVC

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-28)* 



#### :pushpin: MVC 패턴이란?

* Spring Framework로 웹 개발을 할 때, 기본적으로 MVC 패턴을 따름

- MVC 패턴

  - Model, View, Controller 이 3가지로 나뉘어 역할을 분할하여 처리하도록 만들어진 디자인 패턴

  ![img](https://github.com/fake-developers/1st/raw/main/JYJ/resources/mvcpattern.png)

- MVC 패턴 처리 순서
  1. 사용자의 Request를 Controller가 받음
  2. Controller는 Business Logic 처리를 Service와 같이 처리한 후 결과를 Model에 담음
  3. Model에 저장된 결과를 바탕으로 시각처리를 담당하는 View를 제어하여 사용자에게 전달

<br/>

- **역할**
  - **Controller 역할**
    - 사용자가 접근한 URL에 따라 요청을 파악함
    - URL에 맞는 Method를 호출하여 Service와 함께 Business Logic을 처리함
    - 최종적으로 나온 결과는 Model에 저장하고, View에 던져줌
  - **Model 역할**
    - Controller에서 받은 데이터를 저장하는 역할을 함
  - **View 역할**
    - Controller로 부터 받은 Model 데이터를 바탕으로 사용자에게 표현해 줌
    - 일반적으로 HTML, JSP 에 해당함

<br/>

- **MVC 패턴의 종류** (크게 2가지)

  - Model1 방식

    ![img](https://github.com/fake-developers/1st/raw/main/JYJ/resources/model1.png)

    - Java 파일과 <Tag\>를 HTML에 모두 작성하여 개발함
    - 즉, JSP가 모든 요청을 다 처리함
    - 개발이 빠르다는 장점이 있으나, 코드가 복잡해져 유지보수가 힘들어짐

  - Model2 방식

    ![img](https://github.com/fake-developers/1st/raw/main/JYJ/resources/model2.png)

    - 처리해야 할 역할을 Controller, View, Model이 모두 나눠 처리함
    - Controller는 RequestMapping을 통해 URL 확인 후, 바로 View에 던져줄 지, Service로 들어가 추가적인 Business Logic을 수행할지 결정함
    - 이렇게 역할을 나눔으로써 HTML과 Java를 분리할 수 있음
      - 확장성이 좋고, 유연하며, 유지보수도 쉬워짐
    - 현재 대부분의 Spring 프로젝트들은 Model2 구조를 따름

  * 자세한 MVC 내용은 [[SW] MVC 패턴](https://github.com/fake-developers/1st/blob/main/KJY/%5BSW%5D%20MVC%20%ED%8C%A8%ED%84%B4.md) 참고

    <br/>

## 1. Spring MVC

#### 1-1. Spring MVC Architecture란?

![img](https://github.com/fake-developers/1st/raw/main/JYJ/resources/springmvc.png)

- Spring 프레임워크에서 제공하는 웹 모듈

- Spring MVC 모듈을 사용하여, 백엔드 프로그래밍의 기본 프레임워크를 잡음

  - Web 서버에 특화되어 만들어진 모듈이라, 개발자가 해야할 영역을 더 적게 만들어줌
  - 즉, 기존에 Spring 보다 더 깔끔하고 간편하게 개발 가능

- Model, View, Controller를 분리한 디자인 패턴으로, 개발자가 직접 구현함

  - Model
    - 애플리케이션의 상태(data)를 나타냄
    - 일반적으로 Pojo로 구성됨
    - JavaBeans

  - View
    - 디스플레이 또는 데이터 프레젠테이션
    - Model data의 렌더링을 담당하며, HTML output을 생성함
    - JSP와 JSP 이외 Thymeleaf, Groovy, Freemarker 등 여러 Template Engine이 있음

  - Controller
    - View와 Model 사이의 인터페이스 역할
    - Model/View에 대한 사용자 입력 및 요청을 수신하여 그에 따라 적절한 결과를 Model에 담아 View에 전달함
      - 즉, Model Object와 이 Model을 화면에 출력할 View Name을 반환함
    - Controller --> Service --> Dao --> DB
    - Servlet

- **특징**

  - Spring은 DI나 AOP 같은 기능뿐만 아니라, 서블릿 기반의 웹 개발을 위한 MVC 프레임워크를 제공함
  - Spring MVC는 모델2 아키텍처와 Front Controller 패턴을 프레임워크 차원에서 제공함
  - Spring MVC 프레임워크는 Spring을 기반으로 하고 있기 때문에 Spring이 제공하는 트랜젝션 처리나 DI, AOP등을 손쉽게 사용함
  - 대부분의 MVC 프레임워크들은 Front Controller 패턴을 적용해서 구현
  - Spring MVC도 Front Controller 역할을 하는 DispatherServlet 이라는 클래스를 계층의 맨 앞단에 놓고, 서버로 들어오는 모든 요청을 받아서 처리하도록 구성함
  - 예외가 발생했을 때, 일관된 방식으로 처리하는 것도 Front Controller의 역할

<br/>

#### 1.2 Spring Framework가 제공하는 Class

- DispatcherServlet
  - Spring에서 제공하는 Servlet 클래스
  - 사용자의 요청을 받음
  - Dispatcher가 받은 요청은 HandlerMapping으로 넘어감
- HandlerMapping
  - 사용자의 요청을 처리할 Controller를 찾음 (Controller URL Mapping)
  - 요청 URL에 해당하는 Controller 정보를 저장하는 table을 가짐
  - 즉, 클래스에 @RequestMapping("/url") annotation을 명시하면, 해당 URL에 대한 요청이 들어왔을 때 table에 저장된 정보에 따라 해당 클래스 또는 메서드에 Mapping함
- ViewResolver
  - Controller가 반환한 View Name에 prefix, suffix를 적용하여 View Object를 반환함
    - View Name
      - 논리적인 이름
    - View Object
      - 논리적 이름에 prefix, suffix를 붙인 물리적인 view 파일명
    - ex)
      - View Name : home
      - prefix : /WEB-INF/views/
      - suffix : .jsp
      - "/WEB-INF/views/home.jsp" 라는 위치의 View(JSP)에 Controller에게서 받은 Model을 전달함
  - 이후, 해당 View에서 이 Model data를 이용하여 적절한 페이지를 만들어 사용자에게 보여줌

<br/>

#### 1-3. Spring MVC 처리 순서

![img](https://github.com/fake-developers/1st/raw/main/JYJ/resources/springmvcprocess.png)

 

![img](https://github.com/fake-developers/1st/raw/main/JYJ/resources/springmvcprocess2.png)

```
요청 -> 프론트 컨트롤러 -> 핸들러 매핑 -> 핸들러 어댑터 -> 컨트롤러 -> 로직 수행(서비스) -> 컨트롤러 -> 뷰 리졸버 -> 응답(jsp, html)
```

<br/>

1. 클라이언트가 서버에 어떤 요청을 하면, **DispatcherServlet**이 요청을 가로챔
   - web.xml을 살펴보면, 모든 url에 서블릿 매핑을 하여, 모든 요청을 가로챌 수 있게 해둠(변경이 가능함)
2. 요청을 가로챈 DispatcherServlet은 **HandlerMapping**에게 어떤 컨트롤러에게 요청을 위임할지 물어봄
   - HandlerMapping은 servlet-context.xml에서 @Controller로 등록한 것들을 스캔해서 찾아놨기 떄문에, 어느 컨트롤러에게 요청을 위임할지 알고 있음 (앞에서 말한 table)
3. 요청에 매핑된 컨트롤러가 있다면, **@RequestMapping**을 통하여 요청을 처리할 메서드에 도달함
4. 컨트롤러에서는 해당 요청을 처리할 **Service**를 주입 받아, 비즈니스 로직을 Service에게 위임함
5. Service에서는 요청에 필요한 작업 대부분 (코딩)을 담당하며, 데이터베이스 접근이 필요하면 DAO를 주입 받아 DB 처리를 DAO에게 위임함
6. DAO는 MyBaits(또는 hibernate 등) 설정을 이용해 SQL 쿼리를 날려 DB에 저장되어 있는 정보를 받아 서비스에게 다시 돌려줌
   * 이 때, 보통 Request와 함께 날아온 DTO 객체 (@RequestParam, @RequestBody, ...)로 부터 DB 조회에 필요한 데이터를 받아와 쿼리를 만들어 보냄
   * 결과로 받은 Entity 객체를 가지고 Response에 필요한 DTO객체로 변환함

7. 모든 비즈니스 로직을 끝낸 서비스가 결과물을 컨트롤러에게 넘김

8. 결과물을 받은 컨트롤러는 필요에 따라 Model 객체에 결과물을 넣거나, 어떤 view 파일(jsp)을 보여줄 것인지 등의 정보를 담아 DispatcherServlet에게 보냄

9. DispatcherServlet은 **ViewResolver에게** 위에서 받은 뷰에 대한 정보를 넘김

10. ViewResolver는 해당 JSP를(응답할 View를) 찾아 DispatcherServlet에게 알려줌
    * servlet-context.xml에서 suffix, prefix를 통해 만들어준 것을 넘김 (위에서 말했던 것)

11. DispatcherServlet은 응답할 View에게 Render를 지시하고, View는 응답 로직을 처리함

12. 결과적으로, DispatcherServlet이 클라이언트에게 렌더링된 View를 응답함

<br/>

***

+) 더 자세한 부분은 [이 곳](https://gmlwjd9405.github.io/2018/12/20/spring-mvc-framework.html)을 참고

<br/>

## :page_with_curl: Reference

- https://aridom.tistory.com/61
- https://gmlwjd9405.github.io/2018/12/20/spring-mvc-framework.html
- https://jeong-pro.tistory.com/96

- [Spring MVC(1)](https://javacan.tistory.com/entry/130)
- [Spring MVC(설정)](https://gmlwjd9405.github.io/2018/12/20/spring-mvc-framework.html)
- [Spring MVC(3)](https://dailyheumsi.tistory.com/159)
- [Spring MVC(4)](https://shlee0882.tistory.com/207)
