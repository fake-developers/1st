# Spring MVC 패턴

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdJDooL%2FbtqBpP4NxVG%2Fi9C3OlKdgILgixFKny52EK%2Fimg.png" height=250>

- [MVC 패턴](./MVC%20Pattern.md) 의 model2를 기반으로 하는 Spring framework에서 제공하는 웹모듈
- **프론트 컨트롤러 디자인 패턴** 을 사용

  - 뷰에서 들어오는 모든 요청을 담당하는 대표 컨트롤러를 두고 각 요청의 처리는 개별 컨트롤러에 위임하여 나중에 한번에 처리한다.   


<br>

## 동작 흐름

<img src="https://t1.daumcdn.net/cfile/tistory/996CA6455B90B6CC4E">

- 전체적인 실행 흐름

  - 요청 : **Request -> DispatcherServlet -> HandlerMapping -> Controller -> Service -> DAO -> DB** 

    결과 : **-> DAO -> Service -> Controller -> DispatcherServlet -> ViewResolver -> View -> Response**

1. Client로부터 Request요청이 들어오면 **DistcherServlet가 요청을 가로챈다.**
   - 모든 요청을 가로채는 것은 아니고 `web.xml` 에 `<url-pattern>` 에 등록된 내용만 가로챈다.
2. DistcherServlet은 받은 요청을 **HandlerMapping에게 전달. 요청받은 URL을 분석하여 HandlerMapping이 적합한 Controller를 선택하여 반환한다.**
   - HandlerMapping은 `servlet-context.xml` 에서 `@Controller` 로 등록한 것들을 스캔하여 찾아놨기 때문에 어느 Controller가 적합한지 알고있다.
3. 요청에 매핑된 컨트롤러가 **@RequestMapping** 를 통하여 요청할 메서드에 도달한다.
4. 컨트롤러는 해당 요청을 처리한 **Service를 주입([DI](https://github.com/shinjeonghea/Inflearn-Spring/blob/main/DI.md))받아 비지니스 로직을 Service에게 위임** 한다.
5. Service에서는 요청에 필요한 작업 대부분을 담당하며 **데이터베이스에 접근이 필요하면 DAO를 주입받아 DB처리를 DAO에게 위임** 한다.
6. DAO는 mybatis(or hibernate etc..) 설정을 이용해 SQL 쿼리를 날려 DB에 저장되어있는 정보를 받아 서비스에게 다시 돌려준다.
7. 모든 비지니스 로직을 끝낸 Service가 결과물을 Controller에게 보낸다.
8. 결과물을 받은 Controller는 필요에 따라 Model 객체에 결과물을 넣고, 어떤 view(jsp)파일을 보여줄 것인지 등의 정보를 담아 DispatherServlet에게 보낸다.
9. DispatcherServlet은 **Controller에서 받은 view에 대한 정보를 ViewResolver로 넘긴다.**
10. ViewResolver은 적절한 view(jsp)를 찾아서 DispatcherServlet에게 알려준다.
11. DispatcherServlet은 View 객체에 Render를 지시하고 View는 응답 로직을 처리한다.
    - View는 Model 객체에서 화면 표시에 필요한 객체를 가져와 화면 표시를 처리
12. 처리 결과가 포함된 view를 DispatcherSerlvet에 전달한다.
13. 결과적으로 DispatcherSerlvet이 Client에게 렌더링된 view를 출력한다.

<br>

## 주요 구성 요소

- Spring Framework가 제공하는 Class

  - **DispatherServlet**
    - 프론트 컨르롤러를 담당
    - 클라이언트의 요청을 받아 Controller에게 전달 및 리턴한 결과값을 View에게 전달하여 알맞은 응답을 생성
  - **HandlerMapping**
    - URL과 요청정보를 기준으로 어떤 Controller를 실행할지 결정
    - 요청 URL에 해당하는 Controller정보를 저장하는 table을 가진다.
    - 즉, 클래스에 @RequestMapping(“/url”) annotaion을 명시하면 해당 URL에 대한 요청이 들어왔을 때 table에 저장된 정보에 따라 해당 클래스 또는 메서드에 Mapping한다.
  - **ViewResolver**
    - Controller 처리 결과를 생성할 뷰 결정
    - Controller가 반환한 View Name에 prefix, suffix를 적용하여 View Object를 반환한다.
      - View Name 은 논리적인 이름, View Object는 논리적 이름에 prefix, suffix를 붙인 물리적인 view 파일명이다.
      - 예를 들어, 다음과 같은 구성이면,
        - View Name : home
        - prefix : /WEB-INF/views/
        - suffix : .jsp
      - "/WEB-INF/views/home.jsp" 라는 위치의 View(JSP)에 Controller에게서 받은 Model을 전달한다.

- Controller, model, view 구조

  - **Controller**

    - @Contorller 애노테이션 설정
      - bean으로 등록
    - 메서드 별로 @RequestMapping 애노테이션을 사용하여 URL 매핑을 설정
      - @RequestParam은 HTTP 요청 파라미터를 메소드의 파라미터로 전달받을 때 사용
      - 메서드 반환 값은 view 이름으로 반환

    ~~~java
    @Controller // 컨트롤 클래스 설정
    public class MemberController {
    	@Inject 
    	private MemberService memberService;
    	// URL과 메서드 매핑
    	@RequestMapping(value = "/Member", method = RequestMethod.GET)
    	public String memeInfo(@RequestParam("bno") int bno, Model model) {
    		List<MemberVO> members = getAllMember( bno ); 
    		model.addAttribute("members"); //model
    		return ”memberList"; // 반환 값은 View 이름(memberList.jsp)
    	}
    }
    ~~~

  - **Model**

    - 데이터를 저장하기 위한 객체
    - Controller에서 View로 객체를 전달하기 위해 사용된다.
    - 명명된 객체(key-value 형식의 하나의 쌍)들의 집합이며,
      - 이러한 명명된 객체는 model attribute라고 부른다.

  - **View**

    - 결과화면 생성
    - view를 생성하는 방식에는 JSP 이외에도 Thymeleaf, Groovy, Freemarker 등 여러 [Tempate Engine](https://github.com/shinjeonghea/Inflearn-Spring/blob/main/Thymeleaf%20Template%20Engine.md)이 있다.

<br>

:pushpin: *내용이 매우 많고 복잡하기 때문에 조금 큰 틀로 정리를 했으며 더 세부적인 내용은 [여기](https://gmlwjd9405.github.io/2018/12/20/spring-mvc-framework.html) 를 클릭하여 확인하는 것을 추천드립니다.*

-------

**<참조>**

- [[SpringMVC] Spring MVC Framework란](https://gmlwjd9405.github.io/2018/12/20/spring-mvc-framework.html)
- [[부스트코스 웹 프로그래밍] 스프링 MVC](https://dailyheumsi.tistory.com/159)
- [Spring MVC의 동작 구조](https://junu0516.tistory.com/92)

- [ Spring Framework (스프링프레임워크) 기본 동작 순서 및 구조](https://intro0517.tistory.com/151)
