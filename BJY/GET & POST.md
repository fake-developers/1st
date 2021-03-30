## GET & POST

<br/>

### <u>**HTTP**</u>

* HTTP(Hypertext Transfer Protocol)란 하이퍼텍스트 전송 규약으로 Web-Client와 Web-Server간 데이터를 전송하는 프로토콜
* GET & POST 메소드는 HTTP 프로토콜에서 데이터 전송을 위해 지원하는 7가지 메소드 중 일부

<br/>

#### HTTP 패킷

* 클라이언트가 서버로 요청을 했을 때 보내는 데이터

**구조**

- Header
  - 키-값 방식으로 정보가 들어간다.
  - 7가지의 HTTP 메서드 방식
  - Accept, Cookie, Content-Type등과 같은 클라이언트 정보를 담는다.
- Body
  - 보통 비어있지만 특정 데이터를 담아서 서버에 요청을 보낼 수 있다.

<br/>

### <u>GET</u>

* 클라이언트로부터의 데이터를 이름과 값이 결합된 스트링 형태로 전달

  ~~~
  www.example.com?id=dongsik&pass=1234
  ~~~

* 위와 같이 클라이언트의 데이터를 URL 뒤에 붙여서 보낸다.

  - URL 뒤에 `?` 마크를 통해 URL의 끝, 데이터 표현의 시작점을 알려준다.
  - URL 뒤에 붙이므로, Header에 포함되어 서버에 요청한다.
  - Header에 포함해야 하기 때문에 키-값 쌍으로 넣으며 2개 이상의 키-값 쌍을 보낼때에는 `&`로 구분해서 요청한다.

* GET 방식에서 Body에 특별한 내용을 넣을 것이 없으므로 `BODY가 빈 상태로 보내진다`.

  - 따라서 Header의 내용중 Body 데이터를 설명하는 `Content-Type`이라는 Header는 들어가지 않는다.

<br/>

#### 특징 

- 전송할 수 있는 데이터는 255바이트이다.
  - HTTP/1.1 IE에서 2048까지 가능하다고 한다.
- 전송속도가 POST방식보다 빠르다.
  - GET방식의 요청은 `캐싱`(한번 접근 후, 또 요청할 시 빠르게 접근하기 위해 데이터를 저장시켜 놓는다) 때문이다.
- 데이터베이스에 대한 질의어 데이터와 같은 **요청 자체를 위한 정보를 전송할 때** 사용된다.
- 데이터가 URL뒤에 붙기 때문에 **최소한의 보안도 유지되지 않는다**.
- URL 기반의 parameter을 기반으로 하기 때문에 데이터 변경등의 기능을 개발하게 되었을때 크롤링 봇등 예기치 못한 접근으로 인해 문제가 발생 할 여지가 있다.

<br/>

### <u>POST</u>

- 클라이언트와 서버간에 인코딩하여 서버로 전송한다

- 데이터 전송을 기반으로 한 요청 메서드이다

- URL에 붙여 보내지 않고 Body에 데이터를 넣어서 보낸다

  - 그렇기 때문에 Header의 `Content-Type`이라는 필드에 어떤 데이터 타입인지 명시해야 한다

  ~~~
  Content-Type의 예시
  - application/x-www-form-urlencoded
  - text/html
  - multipart/form-data
  등등 7가지 타입이 존재한다.
  ~~~

<br/>

#### 특징

- 입력한 데이터가 URL에 보이지 않으므로 GET방식보다 보안에 우수하다.
  - 단지 보이지 않아서 우수할 뿐이지 두 방식 모두 보안을 생각한다면 암호화가 필요하다.
- 전송할 데이터의 길이에 제한이 없다.
- 복잡한 형태의 데이터를 전송할 때 유용하다.
- 데이터베이스에 대한 갱신 작업과 같은 **서버측에서의 정보 갱신 작업을 원할 때** 사용한다.

<br/>

### <u>GET VS POST</u>

* **설계**

  * GET : Idempotent 하게
    * 서버에게 동일한 요청을 여러 번 전송하더라도 동일한 응답이 돌아와야 한다는 것
    * 주로 조회를 할 때 사용하는 이유
  * POST : Non-idempotent 하게
    *  서버에게 동일한 요청을 여러 번 전송해도 응답은 항상 다를 수 있다
    * 서버의 상태나 데이터를 변경시킬 때 사용되는 이유

  ~~~
  Idempotent(멱등)
  
  수학이나 전산학에서 연산의 한 성질을 나타내는 것으로, 연산을 여러번 적용하더라도 결과가 달라지지 않는 성질
  ~~~

* **URL**

  * GET 
    * URL에 데이터 노출 여부 : O
    * 예시 : `http://localhost:8080/boardList?name=제목&contents=내용` 
  * POST
    * URL에 데이터 노출 여부 : X
    * 예시 : `http://localhost:8080/addBoard`

* **데이터 위치**

  * GET : Header
  * POST : Body

* **캐싱 가능 여부**

  * GET : O
  * POST : X

<br/>

<br/>

<br/>

### REFERENCE

* [GET & POST(1)](https://mangkyu.tistory.com/17)
* [GET & POST(2)](https://dongsik93.github.io/til/2019/12/01/til-tech-getNpost/)
* [GET & POST(3)](https://khj93.tistory.com/entry/GET-%EB%B0%A9%EC%8B%9D%EA%B3%BC-POST-%EB%B0%A9%EC%8B%9D-%EC%9D%B4%EB%9E%80-%EC%B0%A8%EC%9D%B4%EC%A0%90)