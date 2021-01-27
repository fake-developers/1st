# REST API

- ### 들어가기 앞서

  - #### REST란?

    - Representational State Transfer의 약자

    - 자원을 자원의 표현으로 구분하여 해당 자원이 상태(정보)를 주고 받는 모든 것을 의미한다. 즉, 자원의 표현에 의한 상태 전달

      ~~~
      <자원>
      - 해당 소프르웨어가 관리하는 모든 것
      ~~~
    
      ~~~
      <자원의 표현>
      - 자원을 표현하기 위한 이름
      - ex_) DB의 학생 정보가 자원일 때, 'student'를 자원의 표현으로 정한다.
      ~~~
    
      ~~~
      <상태 전달>
      - 데이터가 요청되어지는 시점에서 자원의 상태를 전달
      - JSON 또는 XML을 통해 데이터를 주고 받는다.
      ~~~
    
    - REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 **웹의 장점을 최대한 활용할 수 있는 아키텍쳐**
    
    - HTTP URI를 통해 자원을 명시하고, HTTP Method(Post, Get, Put, Delete)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것이다.
    
      ~~~
      <CRUD Operation>
      Create : 생성 (Post)
      Read : 조회 (Get)
      Update : 수정 (Put)
      Delete : 삭제 (Delete)
      ~~~
      
    - ex_) 게시글 작성
    
      >http://localhost:8080/bbs/insertBoardInfo 라는 URI에 Post방식을 사용하여 JSON형태의 데이터를 전달 한다.
      >
      >CRUD 연산에 대한 요청을 할 때, 요청을 위한 Resource(자원,URI), Method(행위,Post) 그리고 Representation of Resource(자원의 형태, JSON)을 사용한다.
      
      ~~~
      URI VS URL
      
      - URL
        Uniform Resource Loacator로 인터넷 상 자원의 위치를 의미.
        자원의 위치라는 것은 결국 파일의 위치를 의미한다.
      - URI
        Uniform Resource Identifier로 인터넷 상의 자원을 식별하기 위한 문자열의 구성
        URI는 URL을 포함한다.
      그러므로 URI가 더 포괄적인 범위이다.
      ~~~
    
  - #### REST 구성 요소

    - **자원(Resource) : URI**

      > 모든 자원에 고유한 ID가 존재하고, 이 자원은 서버에 존재한다.
      >
      > 자원을 구별하는 ID는 '/groups/:group_id'와 같은 Http URI다.
      >
      > Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 서버에 요청한다.

    - **행위(Method)**

      > Http 프로토콜의 Method를 사용한다.
      >
      > Http 프로토콜은 GET, POST, PUT, DELETE와 같은 메서드를 제공한다.

    - **표현(Representation of Resource)**

      > Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
      >
      > REST에서 하나의 자원은 JSON, XML, TEXT, RSS등 여러 형태의 Representation으로 나타내어 질 수 있다.
      >
      > JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.

  - #### REST 특징

    - **서버-클라이언트 구조(Server-Client)**

      > 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.
      >
      > 	- REST Server : API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
      > 	- Client : 사용자 인증이나 context(세션, 로그인 정보)등을 직접 관리하고 책임진다.
      >
      > 서로간 의존성이 줄어든다.

    - **무상태(Stateless)**

      > HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
      >
      > Client의 conext를 Server에 저장하지 않는다.
      >
      > - 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
      >
      > Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
      >
      > - 각 API 서버는 Client의 요청만을 단순 처각 API 서버는 Client의 요청만을 단순 처리한다.
      >
      > - 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
      >
      >   +) 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
      >
      > - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.

    - **캐시 처리 가능(Cacheable)**

      > 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
      >
      > - HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
      > - HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
      >
      > 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
      >
      > 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.
      >
      > ~~~
      > <캐시>
      > - 자주 사용하는 데이터나 값을 미리 복사해 놓는 임시 저장소
      > <캐싱>
      > - 캐시 영역으로 데이터를 가져와 접근하는 방식
      > ~~~

    - **계층화(Layered System)**

      > Client는 REST API Server만 호출한다.
      >
      > REST Server는 다중 계층으로 구성될 수 있다.
      >
      > - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
      > - 또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.
      >
      > PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.
      >
      > ~~~
      > <로드 밸런싱>
      > - 컴퓨터 네트워크 기술의 일종으로 둘 혹은 셋이상의 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에게 작업을 나누는 것을 의미한다.
      > ~~~

    - **자체 표현(Self-Descriptiveness)**

      > Rest API는 요청 메세지만 보고도 쉡게 이해할 수 있는 자체 표현 구조로 되어있다
      >
      > ~~~
      > HTTP POST , http://localhost:8080/insertBoardInfo
      > {
      > 	"boardVO":{
      > 		"title":"제목",
      > 		"content":"내용"
      > 	}
      > }
      > ~~~
      >
      > - JSON 형태의 REST 메세지는 http://localhost:8080/insertBoardInfo 로 게시글의 제목, 내용을 전달하고 있음을 손쉽게 이해할 수 있다.

    - **인터페이스 일관성(Uniform Interface)**

      > URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
      >
      > HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
      >
      > - 특정 언어나 기술에 종속되지 않는다.
      
     - Code on Demand(optional)
       
       > 클라이언트는 리소스에 대한 표현을 응답으로 받고 처리해야 하는데, 어떻게 처리해야 하는지에 대한 Code를 서버가 제공하는 것을 의미한다.
       >	
       > 서버로부터 스크립트를 받아서 클라이언트에서 실행한다.
       >	
       > 서버에서 제공되는 코드를 실행해야 하기 때문에 보안 문제를 야기할 수 있다.
    
  - #### REST 장단점 & 필요한 이유
  
    - **장점**
      - HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.
      - HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
      - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
      - Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
      - REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
      - 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
      - 서버와 클라이언트의 역할을 명확하게 분리한다.
    - **단점**
      - 표준이 존재하지 않는다.
      - 사용할 수 있는 메소드가 4가지 밖에 없다.
      - 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
        - PUT, DELETE를 사용하지 못하는 점
        - pushState를 지원하지 않는 점
    - **REST가 필요한 이유**
      - 애플리케이션 분리 및 통합
      - 다양한 클라이언트의 등장
      - 최근의 서버 프로그램은 다양한 브라우저와 안드로이폰, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 한다.
      - 이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 되었다.

<br>

- ### REST API란?

  - REST 기반으로 서비스 API를 구현한 것

  - 최근 OpenAPI, 마이크로 서비스 등을 제공하는 업체 대부분은 REST API를 제공한다.

    > OpenAPI : 누구나 사용할 수 있도록 공개된 API (구글 맵, 공공 데이터 등)
    >
    > 마이크로 서비스 : 하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처

    ~~~
    API(Application Programming Interface)
    
    데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환가능 하도록 하는 것이다.
    ~~~

<br>

- ### REST API 특징

  - 사내 시스템들도 REST 기반으로 **시스템을 분산**해 **확장성**과 **재사용성**을 높여 **유지보수** 및 운용을 편리하게 할 수 있다.
  - REST는 HTTP표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트와 서버를 구현할 수 있다.
  - 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.

<br>

- ### REST API 디자인 가이드

  - **REST API 중심규칙**
    **1. URI는 정보의 자원을 표현해야 한다.**
       - 리소스 명은 동사보다는 명사를 사용한다.
       - 리소스의 스토어 이름으로는 복수 명사를 사용해야 한다.

    **2. 자원에 대한 행위는 HTTP Method(Get, Post, Put, Delete)으로 표현한다.**
    
    - HTTP Method나 동사표현이 URI에 들어가서는 안된다.
    - ':id'와 같이 변하는 값은 하나의 특정 resource를 나타내는 고유값이어야 한다.
    
    |                         잘못된 사례                          |                         올바른 사례                          |
    | :----------------------------------------------------------: | :----------------------------------------------------------: |
    | GET /chatrooms/get/:id POST /chatrooms/create GET /chatrooms/delete/:id POST /chatrooms/update/:id | GET /chatrooms/:id POST /chatrooms DELETE /chatrooms/:id PUT /chatrooms/:id |

  - **REST API 세부 규칙**

    **1. 슬래시 구분자(/)는 계층 관계를 나타내는데 사용한다.**

    ```
    http://restapi.example.com/houses/apartments
    http://restapi.example.com/animals/mammals/whales
    ```

    **2. URI 마지막 문자로 슬래시를 포함하지 않는다.**

    ```
    http://restapi.example.com/houses/apartments/ (x)
    http://restapi.example.com/houses/apartments (o)
    ```

    **3. 가독성을 위해 하이픈(-)을 사용할 수는 있으나, 언더바(_)는 사용하지 않는다.**

    **4. URI 경로에는 소문자를 쓴다.**

    **5. 파일 확장자는 URI에 포함하지 않고 Accept header을 사용한다.**

<br>

- ### RESTful

  - 일반적으로 REST라는 아키텍쳐를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어

  - REST API를 제공하는 웹 서비스를 'RESTful'하다고 할 수 있다.

  - 목적

    > 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것

  - RESTful 하지 못한 경우

    > CRUD 기능을 모두 Post로만 처리하는 API
    >
    > route에 resource, id 외의 정보가 들어가는 경우(/students/updateName)

<br>

--------------

- ### 예상질문

  > **REST API란** 무엇인가?
  >
  > - REST 아키텍쳐의 제약 조건을 준수하여 서비스 API를 구현한 것이다.

  > **REST 아키텍쳐**에 대해 설명하시오.
  >
  > - 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하여 웹의 장점을 최대한 활용할 수 있는 아키텍쳐

<br>

---------------

<참조>

- [캐시, 캐싱이란](https://letitkang.tistory.com/165)
- [RESTful에 대한 이해](http://amazingguni.github.io/blog/2016/03/REST%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4-1)
- <https://github.com/fake-developers/1st/blob/BJY-03/BJY/REST%20API.md>
- <https://github.com/fake-developers/1st/blob/JYJ-03/JYJ/RestAPI.md>