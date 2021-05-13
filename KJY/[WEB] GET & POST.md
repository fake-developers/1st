# [WEB] GET & POST

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-28)* 



#### :pushpin: HTTP *(Hypertext Transfer Protocol)*

* 하이퍼텍스트 전송 규약으로 Web-Client와 Web-Server간 데이터를 전송하는 프로토콜
* GET & POST 메소드는 HTTP 프로토콜에서 데이터 전송을 위해 지원하는 7가지 메소드 중 일부

- **HTTP 패킷**
  - 클라이언트가 서버로 요청을 했을 때 보내는 데이터
  - **구조**
    - Header
      - 키-값 방식으로 정보가 들어감
      - 7가지의 HTTP 메서드 방식
      - Accept, Cookie, Content-Type등과 같은 클라이언트 정보를 담음
    - Body
      - 보통 비어있지만, 특정 데이터를 담아서 서버에 요청을 보낼 수 있음

***

<br/>

## 1. GET 방식

#### 1.1 특징

- 주로 어떤 정보를 가져와서 조회하기 위해 사용되는 방식
- URL에 Parameter를 붙여서 데이터를 전송함
  - `www.example.com?param1=value1&param2=value2`
  - 데이터가 URL뒤에 붙기 때문에 **최소한의 보안도 유지되지 않음**.
  - 데이터 변경 등의 기능을 개발하게 되었을때 크롤링 봇 등 예기치 못한 접근으로 인해 문제가 발생 할 여지가 있음
  - 한 번 요청 시, 전송할 수 있는 데이터는 URL 포함 255바이트
    - HTTP/1.1 IE에서는 2048까지 가능함
    - 초과 데이터는 절단됨
- **전송 속도가 POST방식보다 빠름**
  - GET방식의 요청은 **캐싱** 할 수 있기 때문
    - 캐싱 : 한번 접근 후, 또 요청할 시 빠르게 접근하기 위해 데이터를 저장시켜 놓음
- 데이터베이스에 대한 질의어 데이터와 같은 **요청 자체를 위한 정보를 전송할 때** 사용됨
- 데이터를 header에 포함하여 전송함
  - 따라서, body 영역을 데이터 전송을 위해서는 사용할 필요가 없음

<br/>

#### 1-2. 사용 방법

* 클라이언트로부터의 데이터를 이름과 값이 결합된 스트링 형태로 전달

  ```java
  www.example.com?id=dongsik&pass=1234
  ```

* 위와 같이 클라이언트의 데이터를 URL 뒤에 붙여서 보냄

  - URL 뒤에 `?` 마크를 통해 URL의 끝, 데이터 표현의 시작점을 알려줌
  - URL 뒤에 붙이므로, Header에 포함되어 서버에 요청함
  - Header에 포함해야 하기 때문에 키-값 쌍으로 넣음
  - 2개 이상의 키-값 쌍을 보낼때에는 `&`로 구분해서 요청함

* GET 방식에서 Body에 특별한 내용을 넣을 것이 없으므로 **Body가 빈 상태로 보내짐**

  - 따라서 Header의 내용 중 Body 데이터를 설명하는 `Content-Type`이라는 Header는 들어가지 않음

<br/>

## 2. POST 방식

#### 2-1. 특징

* 데이터를 서버로 제출하여, 추가 또는 수정하기 위해 사용하는 방식
* 클라이언트와 서버간에 인코딩하여 서버로 전송함
* 데이터 전송을 기반으로 한 요청 메서드
* Get 방식과 달리 URL에 붙여 보내지 않고, Body 영역에 데이터를 실어 보냄
  - 데이터 전송에 길이 제한이 없으며, 대용량 데이터를 보내는데 적합함
  - 최대 요청을 받는 시간인 Time Out이 존재
    - 클라이언트에서 페이지를 요청하고 기다리는 시간이 존재함
  - Header의 `Content-Type`이라는 필드에 어떤 데이터 타입인지 명시해야 함
* 쿼리스트링 (문자열) 데이터, 라이도 버튼, 텍스트 박스와 같은 객체들의 값을 전송 가능
* Get 방식과 달리, 보내는 데이터가 URL을 통해 노출되지 않아 **기본 보안은 되어있음**
  * 그러나 다른 툴을 사용하여 Post 영역의 데이터를 확인할 수도 있다고 함
  * Get, Post 방식 모두 보안을 생각한다면 암호화가 필요함
  * 데이터베이스에 대한 갱신 작업과 같은 **서버측에서의 정보 갱신 작업을 원할 때** 사용

<br/>

#### 2-2. 사용 방법

* Body에 데이터를 넣어 전송하기 때문에, 헤더 필드 중 body의 데이터를 설명하는 Content-Type에 타입을 명시함

  - header 영역 : `<Content-type:application/json; charset=UTF-8>`

    - ```
      - application/x-www-form-urlencoded
      - text/html
      - multipart/form-data
      등등 7가지 타입이 존재
      ```

  - body 영역 : `{ "param1" : "value1", "param2" : "value2" }`

<br/>

## 3. GET VS POST

* **설계**

  - GET : Idempotent 하게
    - 서버에게 동일한 요청을 여러 번 전송하더라도 동일한 응답이 돌아와야 한다는 것
    - 주로 조회를 할 때 사용
  - POST : Non-idempotent 하게
    - 서버에게 동일한 요청을 여러 번 전송해도 응답은 항상 다를 수 있음
    - 서버의 상태나 데이터를 변경시킬 때 사용

  ```
  Idempotent(멱등)
  
  수학이나 전산학에서 연산의 한 성질을 나타내는 것으로, 연산을 여러번 적용하더라도 결과가 달라지지 않는 성질
  ```

- **비교표**

  | 처리 방식              | Get 방식                                                     | Post 방식                      |
  | ---------------------- | ------------------------------------------------------------ | ------------------------------ |
  | URL에 데이터 노출 여부 | O                                                            | X                              |
  | URL 예시               | http://localhost:8080/boardList?name=title&contents=contents | http://localhost:8080/addBoard |
  | 데이터의 위치          | Header (헤더)                                                | Body (바디)                    |
  | 캐싱 가능 여부         | O                                                            | X                              |

* ![img](https://github.com/fake-developers/1st/raw/JYJ-09/JYJ/resources/GetvsPost.png)

<br/>

## :page_with_curl: Reference

- [https://khj93.tistory.com/entry/GET-%EB%B0%A9%EC%8B%9D%EA%B3%BC-POST-%EB%B0%A9%EC%8B%9D-%EC%9D%B4%EB%9E%80-%EC%B0%A8%EC%9D%B4%EC%A0%90](https://khj93.tistory.com/entry/GET-방식과-POST-방식-이란-차이점)
- https://mangkyu.tistory.com/17
- https://all-record.tistory.com/100
- [GET & POST(1)](https://mangkyu.tistory.com/17)
- [GET & POST(2)](https://dongsik93.github.io/til/2019/12/01/til-tech-getNpost/)
- [GET & POST(3)](https://khj93.tistory.com/entry/GET-방식과-POST-방식-이란-차이점)