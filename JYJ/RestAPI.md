# REST API

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYe Bae*

<hr>

### REST


- <b>REST 란?</b>

  - Representational State Transfer

  - 자원을 이름 (자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다. <small>즉, 자원의 표현에 의한 상태 전달</small>

    > 자원
    >
    > - 해당 소프트웨어가 관리하는 모든 것
    > - ex) 문서, 그림, 데이터, 해당 소프트웨어 자체 등
    >
    > <br/>
    >
    > 자원의 표현
    >
    > - 그 자원을 표현하기 위한 이름
    > - ex) DB의 <b>학생 정보</b>가 자원일 때, <b>'students'</b>를 자원의 표현으로 정한다.
    >
    > <br/>
    >
    > 상태 전달
    >
    > - 데이터가 요청되어지는 시점에서 자원의 상태를 전달한다.
    > - JSON 혹은 XML을 통해 데이터를 주고 받는 것이 일반적이다.

  - REST 아키텍처는 월드 와이드 웹 (WWW)와 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처의 한 형식이다.

    - REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 <b>웹의 장점을 최대한 활용할 수 있는 아키텍처</b>이다.
    - REST는 네트워크 상에서 클라이언트와 서버 사이의 통신 방식 중 하나이다.

  <br/>

- REST의 구체적인 개념

  - HTTP URI를 통해 자원을 명시하고, HTTP Method<small>(Post, Get, Put, Delete)</small>를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것이다.

    > CRUD Operation
    >
    > - Create : 생성 (Post)
    > - Read : 조회 (Get)
    > - Update : 수정 (Put)
    > - Delete : 삭제 (Delete)

  - REST는 자원 기반의 구조 (ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 Http Method를 통해 Resource를 처리하도록 설계된 아키텍처이다.

  - 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 Http URL를 부여한다.

  <br/>

- <b>REST의 장단점</b>

  - 장점

    - HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구축할 필요가 없다.
    - HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있다.
    - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용 가능하다.
    - 하이퍼미디어 API의 기본을 충실히 지키면서 범용성을 보장한다.
    - REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
    - 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
    - 서버와 클라이언트의 역할을 명확하게 분리한다.

    <br/>

  - 단점

    - 표준이 존재하지 않는다.
    - 사용할 수 있는 메소드가 4가지 밖에 없다.
    - 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 값이 왠지 더 어렵게 느껴진다.
    - 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
      - Put, Delete를 사용하지 못하는 점 등

  <br/>

  <br/>

- <b>REST의 구성 요소</b>

  - 자원 : URI

    - 모든 자원에 고유한 ID가 존재하고, 이 자원은 서버에 존재한다.
    - 자원을 구별하는 ID는 HTTP URI이다.
    - 클라이언트는 URI를 이용하여 자원을 지정하고 해당 자원의 상태에 대한 조작을 서버에 요청한다.

    <br/>

  - 행위 (Verb) : HTTP Method

    - Http 프로토콜의 메소드 Get, Post, Put, Delete를 사용한다.

    <br/>

  - 표현(Representation of Resource)

    - 클라이언트가 자원의 상태에 대한 조작을 요청하면 서버는 이에 적절한 응답(Representation)을 보낸다.
    - REST에서 하나의 자원은 JSON, XML, TEXT 등 여러 형태의 표현으로 나타내어질 수 있따.
    - JSON 혹은 XML로 데이터를 주고 받는 것이 일반적이다.

    <br/>

- <b>REST의 특징</b>

  - <b>서버-클라이언트 구조</b>

    - REST 서버 : API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
    - 클라이언트 : 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
    - 서로 간의 의존성이 줄어든다.

    <br/>

  - <b>Stateless (무상태)</b>

    - HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.

    - 클라이언트의 context를 서버에 저장하지 않아 세션과 쿠키같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순하다.

    - 서버는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.

      - 각 API 서버는 클라이언트의 요청만을 단순 처리한다.

      - 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.

        <small>+) 단, 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용</small>

      - 서버의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.

    <br/>

  - <b>Cacheable (캐시 처리 가능)</b> 

    <small>* cache : 자주 사용하는 데이터나 값을 미리 복사해 놓는 임시 저장소</small>

    - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
      - 즉, HTTP가 가진 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
      - HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
    - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
    - 캐시 사용을 통해 응답 시간이 빨라지고 REST 서버 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있따.

    <br/>

  - <b>Layered System (계층화)</b>

    - 클라이언트는 REST API 서버만 호출한다.

    - REST 서버는 다중 계층으로 구성될 수 있다.

      - API 서버는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.

      - 또한 로드 밸런싱 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.

        <small>* 로드밸런싱 : 컴퓨터 네트워크 기술의 일종으로 둘 혹은 셋이상의 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에게 작업을 나누는 것을 의미한다. </small>

      - Proxy, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.

    <br/>

  - <b>Code-On-Demand (optional)</b>

    <small>* code on demand :  사용자가 어떤 프로그램을 자기 단말기로 다운로드 받기를 원하면 그때 시스템에 의해 Java 프로그램이 컴파일되어 해당 단말기에서 실행되는 바이너리로 생성되어 다운로드되는 것</small>

    - 서버로부터 스크립트를 받아서 클라이언트에서 실행한다.

    - 반드시 충족할 필요는 없다.

    <br/>

  - <b>인터페이스 일관성</b>

    - URI로 지정한 자원에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
    - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
      - 특정 언어나 기술에 종속되지 않는다.

<br/>

<br/>

### REST API

- <b>REST API (RESTful API) 란?</b>

   - REST 아키텍처의 제약 조건을 준수하여 서비스 API를 구현한 것이다.

     > API
     >
     > ```
     > 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램 간 상호작용을 촉진하며,
     > 서로 정보를 교환 가능하도록 하는 것이다.
     > ```
     >
     > - 때때로 API는 정보 제공자와 정보 사용자 간의 계약으로 지칭되며,
     > - 소비자에게 필요한 콘텐츠 (호출) 와 생산자에게 필요한 콘텐츠 (응답) 를 구성한다.
     >   - ex) 날씨 서비스용 API에서 사용자는 우편번호를 제공, 생산자는 최고 기온, 최저 기온으로 구성된 응답을 답하도록 지정할 수 있음
     > - 즉, 시스템과 상호 작용하여 정보를 검색하거나 기능을 수행하고자 할 때 API는 사용자가 원하는 것을 시스템에 전달할 수 있게 지원하여 시스템이 요청을 이해하고 이행할 수 있도록 할 수 있다.

     <br/>

   -  최근 Open API , 마이크로 서비스 등을 제공하는 업체 대부분은 REST API를 제공한다.

      <small> * Open API : 누구나 사용할 수 있도록 공개된 API, ex) 구글 맵</small>

      <small>* 마이크로 서비스 : 하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처</small>

   <br/>

   <br/>

- <b>REST API의 특징</b>

  - 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
  - REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트와 서버를 구현할 수 있다.
  - 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.

  <br/>

- <b>REST API 디자인 가이드

  - URI 는 정보의 자원을 표현해야 한다.
  - 자원에 대한 행위는 HTTP Method(Get, Post, Put, Delete)로 표현한다.

  > <b>REST API 중심 규칙</b>
  >
  > 1. URI는 정보의 자원을 표현해야 한다. <small>(리소스 명은 동사보다는 <b>명사</b>를 사용한다.)</small>
  >
  >    ```xml
  >    GET /members/delete/1 <!-- REST를 제대로 적용하지 않은 URI -->
  >
  >    <!-- URI는 자원을 표현하는데 중점을 두어야 한다.
  >    	즉, delete와 같은 행위에 대한 표현이 들어가서는 안된다.-->
  >    ```
  >
  >    <br/>
  >
  > 2. 자원에 대한 행위는 HTTP Method로 표현한다.
  >
  >    <small>위의 잘못된 URI를 HTTP Method를 통해 수정</small>
  >
  >    ```
  >    DELETE /members/1	
  >    ```
  >
  >    - HTTP Method나 동사 표현이 URI에 들어가면 안된다.
  >    - :id와 같이 변하는 값은 하나의 특정 자원을 나타내는 고유 값이어야 한다.
  >
  >    | 잘못된 사례                                                  | 올바른 사례                                                  |
  >    | ------------------------------------------------------------ | ------------------------------------------------------------ |
  >    | GET /chatrooms/get/:id <br />POST /chatrooms/create<br />GET /chatrooms/delete/:id <br />POST /chatrooms/update/:id | GET /chatrooms/:id <br />POST /chatrooms <br />DELETE /chatrooms/:id <br />PUT /chatrooms/:id |
  >
  >    <br/>
  >
  >    <br/>
  >
  > <b>URI 설계 시 주의할 점</b>
  >
  > 1. 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용한다.
  >
  >    ```
  >        http://restapi.example.com/houses/apartments
  >        http://restapi.example.com/animals/mammals/whales
  >    ```
  >
  >    <br/>
  >
  > 2. URI 마지막 문자로 슬래시를 포함하지 않는다.
  >
  >    ```
  >        http://restapi.example.com/houses/apartments/ (x)
  >        http://restapi.example.com/houses/apartments (o)
  >    ```
  >
  >    <br/>
  >
  > 3. 하이픈은 URI 가독성을 높이는데 사용한다.
  >
  >    - 불가피하게 긴 URI를 사용하게 된다면 사용
  >
  >    <br/>
  >
  > 4. 밑줄은 URI에 사용하지 않는다.
  >
  >    <br/>
  >
  > 5. URI 경로는 소문자로 작성한다.
  >
  > 6. 파일 확장자는 URI에 포함시키지 않는다.
  >
  >    ```
  >       http://restapi.example.com/members/soccer/345/photo.jpg (X)
  >    ```

  

<br/>

- <b>RESTful의 목적</b>

  - 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
  - RESTful한 API를 구현하는 근본적인 목적이 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이다.
    - 성능이 중요한 상황에서는 굳이 구현할 필요가 없다.

  <br/>

- <b>RESTful 하지 못한 경우</b>

  - CRUD 기능을 모두 Post로만 처리하는 API
  - route에 resource, id 외의 정보가 들어가는 경우 (/students/updateName)

<br/>

<br/>

## 예상질문❔

Q1) REST API란 무엇인가?

A1) REST 아키텍처의 제약 조건을 준수하여 서비스 API를 구현한 것이다. HTTP method 네가지를 이용하여 자원과 행위를 표현하고 정보를 공유한다.

<br/>

Q2) REST 아키텍처에 대해 설명하라.

A2) 자원을 이름 (자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다. HTTP URI를 통해 자원을 명시하고, HTTP Method를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것이다.

<br/>

Q3) API란 무엇인가?

A3) 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램 간 상호작용을 촉진하며, 서로 정보를 교환 가능하도록 하는 것이다. 정보를 주고 받을 때 정해진 형식을 이용한다.

### Reference📖

- https://www.redhat.com/ko/topics/api/what-is-a-rest-api
- https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
- https://meetup.toast.com/posts/92
- https://mangkyu.tistory.com/69
