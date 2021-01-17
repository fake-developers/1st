## REST API (RESTFUL)

<br/>

### <u>REST란</u>

Representational State Transfer의 약자.

어떤 자원에 대해 CRUD(Create, Read, Update, Delete) 연산을 수행하기 위해 URI(Resource)로 요청을 보내는 것.

* Get, Post 등의 방식을 사용하여 요청을 보내며, 요청을 위한 자원은 특정한 형태로 표현된다.

> ex) 게시글 작성  
>
> http://localhost:8080/bbs/insertBoardInfo 라는 URI에 Post방식을 사용하여 JSON형태의 데이터를 전달 한다.
>
> CRUD 연산에 대한 요청을 할 때, 요청을 위한 Resource(자원,URI), Method(행위,Post) 그리고 Representation of Resource(자원의 형태, JSON)을 사용한다. 
>
> 이것이 REST이다.

~~~
URI VS URL

URL은 Uniform Resource Loacator로 인터넷 상 자원의 위치를 의미.
자원의 위치라는 것은 결국 파일의 위치를 의미한다.
URI는 Uniform Resource Identifier로 인터넷 상의 자원을 식별하기 위한 문자열의 구성으로, URI는 URL을 포함하게 된다.
그러므로 URI가 더 포괄적인 범위이다.
~~~

<br/>

### <u>REST 구성 요소</u>

#### - 자원(Resource) : URI

* 모든 자원에 고유한 ID가 존재하고, 이 자원은 서버에 존재한다.
* 자원을 구별하는 ID는 '/groups/:group_id'와 같은 Http URI다.
* Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 서버에 요청한다.

#### - 행위(Method) 

* Http 프로토콜의 Method를 사용한다.
* Http 프로토콜은 GET, POST, PUT, DELETE와 같은 메서드를 제공한다.

#### - 표현(Representation of Resource)

* Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
* REST에서 하나의 자원은 JSON, XML, TEXT, RSS등 여러 형태의 Representation으로 나타내어 질 수 있다.
* JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.

<br/>

### <u>REST 특징</u>

#### 1. 서버- 클라이언트 구조(Server-Client)

* 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.
  * REST Server : API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
  * Client : 사용자 인증이나 context(세션, 로그인 정보)등을 직접 관리하고 책임진다.
* 서로간 의존성이 줄어든다.

#### 2. 무상태(Stateless)

* HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
* Client의 conext를 Server에 저장하지 않는다.
  * 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
* Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
  * 각 API 서버는 Client의 요청만을 단순 처각 API 서버는 Client의 요청만을 단순 처리한다.
  * 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
  * 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
  * Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.

#### 3. 캐시 처리 가능(Cacheable)

* 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.

  *  HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
  * HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.

* 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.

* 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.

  ~~~
  캐싱(Caching)
  
  이미 가져온 데이터나 계산된 결과 값의 복사본을 저장함으로써 처리 속도를 향상시키며, 이를 통해 향후 요청을 더 빠르게 처리할 수 있다.
  ~~~

#### 4. 계층화(Layered System)

* Client는 REST API Server만 호출한다.
* REST Server는 다중 계층으로 구성될 수 있다.
  * API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
  * 또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.
* PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.

#### 5. 자체 표현(Self-Descriptiveness)

* Rest API는 요청 메세지만 보고도 쉡게 이해할 수 있는 자체 표현 구조로 되어있다.

  ~~~json
  HTTP POST , http://localhost:8080/insertBoardInfo
  {
  	"boardVO":{
  		"title":"제목",
  		"content":"내용"
  	}
  }
  ~~~

  > JSON 형태의 REST 메세지는 http://localhost:8080/insertBoardInfo 로 게시글의 제목, 내용을 전달하고 있음을 손쉽게 이해할 수 있다.

#### 6. 인터페이스 일관성(Uniform Interface)

* URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
* HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
  * 특정 언어나 기술에 종속되지 않는다.

<br/>

### <u>REST 장단점 & 필요한 이유</u>

#### 장점

* HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.
* HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
* HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
* Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
* REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
* 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
* 서버와 클라이언트의 역할을 명확하게 분리한다.

#### 단점

* 표준이 존재하지 않는다.
* 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
  * PUT, DELETE를 사용하지 못하는 점
  * pushState를 지원하지 않는 점

#### REST가 필요한 이유

* ‘애플리케이션 분리 및 통합’
* ‘다양한 클라이언트의 등장’
* 최근의 서버 프로그램은 다양한 브라우저와 안드로이폰, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 한다.
* 이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 되었다.

<br/>

### <u>REST API</u>

REST 기반으로 서비스 API를 구현한 것

* 최근 OpenAPI, 마이크로 서비스 등을 제공하는 업체 대부분은 REST API를 제공한다.

  > OpenAPI : 누구나 사용할 수 있도록 공개된 API (구글 맵, 공공 데이터 등)
  >
  > 마이크로 서비스 : 하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처

~~~
API(Application Programming Interface)

데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환가능 하도록 하는 것.
~~~

#### 특징

* 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
* REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
* 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.

#### 기본 규칙

1. **URI는 정보의 자원을 표현해야한다.**

   * resource는 동사보다는 명사를, 대문자보다는 소문자를 사용한다.
   * resource의 스토어 이름으로는 복수 명사를 사용해야 한다.

2. **자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)으로 표현한다.**

   * HTTP Method나 동사표현이 URI에 들어가면 안된다.
   * `:id`와 같이 변하는 값은 하나의 특정 resource를 나타내는 고유값이어야 한다.

   |                         잘못된 사례                          |                         올바른 사례                          |
   | :----------------------------------------------------------: | :----------------------------------------------------------: |
   | GET /chatrooms/get/:id <br />POST /chatrooms/create <br />GET /chatrooms/delete/:id <br />POST /chatrooms/update/:id | GET /chatrooms/:id <br />POST /chatrooms <br />DELETE /chatrooms/:id <br />PUT /chatrooms/:id |

3. **HTTP Method**

   ~~~
   주로 쓰는 Method
   
   GET: 조회 (받겠다)
   POST: 리소스 생성 (보내겠다)
   PUT: 리소스 전체 갱신(놓겠다/넣겠다)
   PATCH: 리소스 부분 갱신(붙이겠다)
   DELETE: 리소스 삭제 (지정한 서버의 파일을 삭제하겠다)
   ~~~

   ~~~
   나머지 Method
   
   HEAD: GET과 유사하나 HTTP 메시지 헤더만 반송하고 데이터 내용을 돌려보내지 않음(헤더만 보겠다)
   OPTION: 통신 옵션을 통지/조사
   TRACE: 리퀘스트 라인과 헤더를 그대로 클라이언트에 반송(리퀘스트 치환상태를 조사할 때 사용)
   CONNECT: 암호화된 메시지를 프록시로 전송
   ~~~

#### 세부 규칙

1. 슬래시(/)는 계층 관계를 나타낸다.
2. URI의 마지막엔 슬래시(/)를 포함하지 않는다.
3. 가독성을 높이기 위해 하이픈(-)을 사용할 수 있으나 언더바(_)를 사용하진 않는다.
4. URI 경로에는 소문자를 쓴다.
5. 파일 확장자는 URI에 포함하지 않고 Accept header을 사용한다.
6. 리소스간 연관관계가 있는 경우
   * /리소스명/리소스ID/관계있는 다른 리소스명(일반적으로 소유has의 관계)

<br/>

### <u>RESTful</u>

`일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어`

* REST API를 제공하는 웹 서비스를 'RESTful'하다고 할 수 있다.

* RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다. 

  즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.

<br/>

<br/>

<br/>

### REFERENCE

* [REST API](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)
* [REST API](https://mangkyu.tistory.com/46)
* [캐싱](https://hahahoho5915.tistory.com/33)
* [RESTful API 설계규칙](https://one-it.tistory.com/entry/RESTful-API-%EC%84%A4%EA%B3%84-%EA%B7%9C%EC%B9%99)

