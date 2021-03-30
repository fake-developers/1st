## Spring MVC

<br/>

### <u>**Spring MVC란**</u>

* Spring 프레임워크에서 제공하는 웹 모듈이다.
* MVC 는 Model-View-Controller 의 약자로, 기본 시스템 모듈을 MVC 로 나누어 구현되어있다.
  - Model 은 '데이터' 디자인을 담당한다.
    - ex. 상품 목록, 주문 내역 등
  - View 는 '실제로 렌더링되어 보이는 페이지' 를 담당한다.
    - ex. `.JSP` 파일들이 여기에 해당된다.
  - Controller 는 사용자의 요청을 받고, 응답을 주는 로직을 담당한다.
    - ex. GET 등의 uri 매핑이 여기에 해당된다.
* Spring MVC 모듈을 사용하여, 백엔드 프로그래밍의 기본 프레임워크를 잡는다.
  - Web 서버에 특화되어 만들어진 모듈이라, 개발자가 해야할 영역을 더 적게 만들어준다.
  - 즉 기존에 Spring 보다 더 깔끔하고 간편하게 개발 가능.

![spring_mvc](https://user-images.githubusercontent.com/61674527/112329107-4149cb80-8cfa-11eb-86ba-d3025f7d390d.png)

<br/>

### <u>특징</u>

*  Spring은 DI나 AOP 같은 기능뿐만 아니라, 서블릿 기반의 웹 개발을 위한 MVC 프레임워크를 제공한다.
* Spring MVC는 모델2 아키텍처와 Front Controller 패턴을 프레임워크 차원에서 제공한다.
* Spring MVC 프레임워크는 Spring을 기반으로 하고 있기 때문에 Spring이 제공하는 트랜젝션 처리나 DI, AOP등을 손쉽게 사용한다.
* 대부분의 MVC 프레임워크들은 Front Controller 패턴을 적용해서 구현한다.
* Spring MVC도 Front Controller 역할을 하는 DispatherServlet 이라는 클래스를 계층의 맨 앞단에 놓고, 서버로 들어오는 모든 요청을 받아서 처리하도록 구성한다.
* 예외가 발생했을 때 일관된 방식으로 처리하는 것도 Front Controller의 역할이다.

<br/>

### <u>기본 동작 흐름</u>

![spring_mvc_flow](https://user-images.githubusercontent.com/61674527/112329155-4c9cf700-8cfa-11eb-819b-6fbec9b45491.png)

~~~
요청 -> 프론트 컨트롤러 -> 핸들러 매핑 -> 핸들러 어댑터 -> 컨트롤러 -> 로직 수행(서비스) -> 컨트롤러 -> 뷰 리졸버 -> 응답(jsp, html)
~~~

<br/>

### <u>구성</u>

- 컨트롤러 중에서도, 맨 앞단에서 유저의 요청을 받는 컨트롤러를 프론트 컨트롤러라고 한다.
  - `DispatcherServlet` 객체가 이 역할을 한다.
  - 본격적으로 로직에 들어오기 전에, 요청에 대한 선처리 작업을 수행한다.
  - ex. 지역 정보 결정, 멀티파트 파일 업로드 처리 등
- 프론트 컨트롤러는 요청을 핸들러 매핑을 통해 해당 요청을 어떤 핸들러가 처리해야하는지를 매핑한다.
  - `HandlerMapping` 객체가 핸들러 매핑에 대한 정보를 담고있다.
- 이렇게 매핑된 핸들러를 실제로 실행하는 역할은 핸들러 어댑터가 담당한다.
  - `HandlerAdapter` 객체가 이 역할을 한다.
- 컨트롤러는 해당 요청을 처리하는 로직을 담고있다.
  - 보통 요청의 종류 혹은 로직의 분류에 따라 내부적으로 Service 단위로 나누어 모듈화 한다.
  - 각 서비스에서는 DB 접근할 수 있는 Repository 객체를 이용하여 데이터에 접근할 수 있다.
- 컨트롤러는 서비스에서의 로직 처리 후, 결과를 뷰 리졸버를 거쳐 뷰 파일을 렌더링하여 내보낸다.
  - `ViewResolver` 객체가 이 역할을 한다.

<br/>

### <u>Spring MVC를 위한 필수 설정</u>

1. **Maven Configuration (pom.xml)**

   * 자신의 프로젝트에 대한 고유의 좌표 설정
     1. groupId
        * 자신의 프로젝트를 고유하게 식별하게 해 주는 것으로, 최소한 내가 컨트롤하는domain name이어야 한다.
        * package 명명 규칙을 따른다.
        * 하위 그룹은 얼마든지 추가할 수 있다.
     2. artifactId
        * 제품의 이름으로, 버전 정보를 생략한 jar 파일의 이름이다.
        * 프로젝트 이름과 동일하게 설정한다.
        * 소문자로만 작성하며 특수문자는 사용하지 않는다.
     3. version
        * SNAPSHOT: 개발용, RELEASE: 배포용
        * 숫자와 점을 사용하여 버전 형태를 표현한다.(1.0, 1.1, 1.0.1, …)
   * Maven 장점
     * pom.xml에 명시한 lib를 자동으로 다운
     * build process 자동화
       * compile -> test -> package(.war) -> install -> deploy
         

2. **Web Deployment Descriptor (web.xml)**

   * 개념
     * web application의 설정을 위한 deployment descriptor
     * SUN에서 정해놓은 규칙에 맞게 작성해야 하며 모든 WAS에 대하여 작성 방법이 동일하다.

   * 역할
     * Deploy할 때 Servlet의 정보를 설정해준다.
     * 브라우저가 Java Servlet에 접근하기 위해서는 WAS(Ex. Tomcat)에 필요한 정보를 알려줘야 해당하는 Servlet을 호출할 수 있다.
       * 정보 1) 배포할 Servlet이 무엇인지
       * 정보 2) 해당 Servlet이 어떤 URL에 매핑되는지
   * 구체적인 설정 내용
     * DispatcherServlet
     * ContextLoaderListener
     * Filter: encodingFilter, springSecurityFilterChain

3. **Spring MVC Configuration Files**

   * dispatcher-servlet.xml
     * 주요 설정 내용 : Controller 관련, ViewResolver, mvc:annotation-driven 설정 등
   * applicationContext.xml
     * 주요 설정 내용 : DataSource 관련, properties 등룍, SessionFactory, TransactionManager 등
   * service-context.xml
     * 주요 설정 내용 : Service 관련
   * dao-context.xml
     * 주요 설정 내용 : DAO 관련
   * security-context.xml
     * 주요 설정 내용 : Security 관련, BCryptPasswordEncoder 등

<br/>

### <u>구현</u>

1. **DispatcherServlet을 프론트 컨트롤러로 세팅**

   ~~~xml
   <!-- web.xml -->
   
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app>
     <display-name>Spring JavaConfig Sample</display-name>
   
     <servlet>
       <!-- 2. 해당 서블릿의 구현체는 DispatcherServlet 로 정의-->
       <servlet-name>mvc</servlet-name>
       <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
       <!-- 3. contextClass는 AnnotationConfigWebApplicationContext 를 사용-->
       <init-param>
         <param-name>contextClass</param-name>
         <param-value>org.springframework.web.context.support.AnnotationConfigWebApplicationContext</param-value>
       </init-param>
       <!-- 4. context 에 대해 따로 설정해둔 클래스의 위치를 파라미터로 줌.
       여기서는 사용자가 정의한 WebMvcContextConfiguration 을 사용-->
       <init-param>
         <param-name>contextConfigLocation</param-name>
         <param-value>kr.or.connect.mvcexam.config.WebMvcContextConfiguration</param-value>
       </init-param>
       <load-on-startup>1</load-on-startup>
     </servlet>
   
     <servlet-mapping>
       <!-- 1. / 로 들어오는 요청은 mvc 라는 이름의 servlet 이 처리-->
       <servlet-name>mvc</servlet-name>
       <url-pattern>/</url-pattern>
     </servlet-mapping>
   </web-app>
   ~~~

   ~~~java
   // WebMvcContextConfiguration.java
   
   package org.example.guestbook.config;
   
   ...
   
   // 설정 파일임을 Spring이 알게함.
   @Configuration 
   // Web에 필요한 빈들을 대부분 자동으로 설정. 주로 아래처럼 커스텀으로 설정해야할 때, WebMvcConfigurerAdapter 를 상속받아 클래스로 구현
   @EnableWebMvc
   // 해당 패키지에 정의된 클래스중 컴포넌트들을 빈으로 등록해놓음.
   // @Controller, @Service, @Repository, @Component 가 달린 객체를 찾음. 
   @ComponentScan(basePackages = { "kr.or.connect.mvcexam.controller" })
   public class WebMvcContextConfiguration extends WebMvcConfigurerAdapter {
   
       // 자바 파일이 아닌, Resource 파일들에 대한 url 요청이 왔을 경우, 해당 경로에서 찾을 수 있게 설정
       @Override
       public void addResourceHandlers(ResourceHandlerRegistry registry) {
   
           registry.addResourceHandler("/assets/**").addResourceLocations("classpath:/META-INF/resources/webjars/").setCachePeriod(31556926);
           registry.addResourceHandler("/css/**").addResourceLocations("/css/").setCachePeriod(31556926);
           registry.addResourceHandler("/img/**").addResourceLocations("/img/").setCachePeriod(31556926);
           registry.addResourceHandler("/js/**").addResourceLocations("/js/").setCachePeriod(31556926);
         }
   
       // default servlet handler를 사용하게 함
       @Override
       public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
           configurer.enable();
       }
   
       // / 로 접근시 main 템플릿(jsp) 로 가게함.
       @Override
       public void addViewControllers(final ViewControllerRegistry registry) {
           System.out.println("addViewControllers가 호출됩니다. ");
           registry.addViewController("/").setViewName("main");
       }
   
       // 렌더링되는 view 파일들의 경로와 확장자명 설정
       @Bean
       public InternalResourceViewResolver getInternalResourceViewResolver() {
           InternalResourceViewResolver resolver = new InternalResourceViewResolver();
           resolver.setPrefix("/WEB-INF/views/");
           resolver.setSuffix(".jsp");
           return resolver;
       }
   }
   ~~~

2. **이 외 전반적인 모듈 구성**

   <img width="300" alt="spring_mvc_구성" src="https://user-images.githubusercontent.com/61674527/112329209-59214f80-8cfa-11eb-964e-73d56ee3c8a0.png">

   * **config/***

     - 각종 설정 클래스 파일들을 담고 있다.
     - 클래스 앞에 `@Configuration` 이 붙는다.
     - WebMvc 설정 관련 Config 를 제외하고 나머지는 모듈화한 뒤 Application 에서 모두 import
     - `@Controller` 관련 빈들은 `WebMvcContextConfiguration` 에서 `@ComponentScan` 으로 찾아줘야하고,
       `@Service`, `@Service`, `@Component` 관련 빈들은 `ApplicationConfig` 에서 찾아줘야 한다.
     - 예를 들어 `ApplicationConfig` 는 다음과 같다.

     ~~~java
     @Configuration
     @ComponentScan(basePackages = {"org.example.guestbook.dao", "org.example.guestbook.service"})
     @Import({DBConfig.class})
     public class ApplicationConfig {
     }
     ~~~

   * **controller/***

     * 각종 컨트롤러 클래스 파일들을 담고 있다.
     * 클래스 앞에 `@Controller` 가 붙는다.
     * 각 컨트롤러 코드는 URI 매핑을 담당한다.
     * Serivce 인스턴스를 가져와 로직을 실행하고, View 단에 나가기 전후 작업을 담당한다.
     * 예를 들어 `GuestbookController` 는 다음과 같다.

     ~~~java
     @Controller
     public class GuestbookController {
         // @Autowired 를 통해 스프링이 관리하는 빈을 가져올 수 있음.
         @Autowired
         GuestbookService guestbookService;
     
         @GetMapping(path="/list")
         public String list(@RequestParam(name="start", required = false, defaultValue = "0") int start, ModelMap model) {
     
             // start로 시작하는 방명록 목록 구하기
             List<Guestbook> list = guestbookService.getGuestbooks(start);
     
             ...
     
             model.addAttribute("list", list);
     
             // list.jsp 로 렌더링
            return "list";
         }
     
         @PostMapping(path="/write")
         public String write(@ModelAttribute Guestbook guestbook,
                             HttpServletRequest request) {
             String clientIp = request.getRemoteAddr();
             guestbookService.addGuestbook(guestbook, clientIp);
             return "redirect:list";
         }
     }
     ~~~

   * **dao/***

     * B 에 대해 접근할 때 사용하는 클래스 파일들을 담고 있다.
     * 클래스 앞에 `@Repository` 가 붙는다.
     * 실제 dao 클래스와, 사용할 SQL 만을 담고있는 클래스가 따로 모듈화해서 사용한다.
     * 예를 들어 `GuestbookDao` 와 `GuestbookDaoSqls` 는 다음과 같다.

     ~~~java
     // GuestbookDao.java
     
     import static org.example.guestbook.dao.GuestbookDaoSqls.*;
     
     @Repository
     public class GuestbookDao {
         private NamedParameterJdbcTemplate jdbc;
         private SimpleJdbcInsert insertAction;
         private RowMapper<Guestbook> rowMapper = BeanPropertyRowMapper.newInstance(Guestbook.class);
     
         public GuestbookDao(DataSource dataSource) {
             this.jdbc = new NamedParameterJdbcTemplate(dataSource);
             this.insertAction = new SimpleJdbcInsert(dataSource)
                     .withTableName("guestbook")
                     .usingGeneratedKeyColumns("id");
         }
     
         public List<Guestbook> selectAll(Integer start, Integer limit) {
             ...
         }
     
         public Long insert(Guestbook guestbook) {
             ...
         }
     
         public int deleteById(Long id) {
             ...
         }
     
         ...
     }
     ~~~

     ~~~java
     // GuestbookDaoSqls.java
     
     public class GuestbookDaoSqls {
         public static final String SELECT_PAGING = "SELECT id, name, content, regdate FROM guestbook ORDER BY id DESC limit :start, :limit";
         public static final String DELETE_BY_ID = "DELETE FROM guestbook WHERE id = :id";
         public static final String SELECT_COUNT = "SELECT count(*) FROM guestbook";
     }
     ~~~

   * **dto/***

     * 데이터를 모델링한 클래스 파일들을 담고있다.
     * 필드(프로퍼티)와 Getter, Setter 를 가진다.
     * 예를 들어 `Guestbook` 는 다음과 같이 같다.

     ~~~java
     public class Guestbook {
         private Long id;
         private String name;
         private String content;
         private Date regdate;
     
         public Long getId() {
             return id;
         }
     
         public void setId(Long id) {
             this.id = id;
         }
     
         public String getName() {
             return name;
         }
         ...
     }
     ~~~

   * **service/***

     * 서비스 로직을 담는 클래스 파일들을 담고있다.
     * 클래스 앞에 `@Service` 가 붙는다.
     * Interface로 핵심 로직 먼저 정의한 후, 클래스로 구현한다.
     * 필요한 경우, `Dao` 를 직접 사용하는 클래스이다.
     * 예를 들어 `GuestbookServiceImpl` 는 다음과 같다.

     ~~~java
     @Service
     public class GuestbookServiceImpl implements GuestbookService {
         @Autowired
         GuestbookDao guestbookDao;
     
         @Autowired
         LogDao logDao;
     
         @Override
         @Transactional // 기본 값 read only transaction 적용
         public List<Guestbook> getGuestbooks(Integer start) {
             return guestbookDao.selectAll(start, GuestbookService.LIMIT);
         }
     
         @Override
         @Transactional(readOnly = false)
         public int deleteGuestbook(Long id, String ip) {
             int deleteCount = guestbookDao.deleteById(id);
             Log log = new Log();
             log.setIp(ip);
             log.setMethod("delete");
             log.setRegdate(new Date());
             logDao.insert(log);
             return deleteCount;
         }
     
         ...
     }
     ~~~

   * **webapp/WEB-INF/views/***

     * 렌더링 되는 뷰 관련 파일(`.jsp`)들을 담고있다.
     * 이 파일들은 뷰 리졸버를 거쳐, 최종적으로 렌더링 되기 직전의 파일이다.

<br/>

<br/>

<br/>

### REFERENCE

* [Spring MVC(1)](https://javacan.tistory.com/entry/130)
* [Spring MVC(설정)](https://gmlwjd9405.github.io/2018/12/20/spring-mvc-framework.html)
* [Spring MVC(3)](https://dailyheumsi.tistory.com/159)
* [Spring MVC(4)](https://shlee0882.tistory.com/207)

