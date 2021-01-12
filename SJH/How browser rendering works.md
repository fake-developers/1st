# 브라우저 동작 과정

- #### 들어가기 앞서

  - 웹 애플리케이션이란?

    - 웹 브라우저에서 이용할 수 있는 응용 소프트웨어

        ~~~
        <웹 애플리케이션 구동 과정>
        1.URL Entered: 사용자가 웹 브라우저에서 사이트 주소를 입력
        2.DNS Lookup: DNS를 이용하여 사이트 주소에 해당되는 Server IP 접근
        3.Socket Connection: Client(브라우저)와 Server 간 접속을 위한 TCP 소켓 연결
        4.HTTP Request: Client 에서 HTTP Header 와 데이터가 서버로 전송
        5.Content Download: 해당 요청이 Server 에 도달하면 사용자가 원하는 문서를 다시 웹 브라우저에 전송
        6.Browser Rendering: 웹 브라우저의 렌더링엔진에서 해당 문서를 다음과 같은 순서로 파싱
        ~~~
        
        ![WebApplicationlogic](https://user-images.githubusercontent.com/58902042/104191258-a19dd080-5460-11eb-8db3-c3da78012130.PNG)

<br>

- #### 브라우저란?

  - 인터넷상에서 웹에 연결시켜 주는 윈도 기반의 소프트웨어
  - ex. 인터넷 익스플로러, 크롬, 사파리, 오페라, 파이어 폭스 등..

<br>

- #### 브라우저의 기능

  - 사용자가 선택한 **자원**을 서버에 요청하고 화면(브라우저)에 받아오는 것

    > 자원은 보통 HTML문서지만 PDF나 이미지 또는 다른 형태일 수 도 있다.
    >
    > 자원의 주소는 URI에 의해 정해진다.

<br>

- #### 브라우저의 구조

  ​	<img src="https://user-images.githubusercontent.com/58902042/104192414-22a99780-5462-11eb-86ec-8d08d7010c1d.PNG" width="500" height="300">

  - **사용자 인터페이스(UI)**
    
    - 주소창, 즐겨찾기 등 사용자가 조작 가능한 영역
    
  - **브라우저 엔진**
  
    - 사용자 인터페이스와 렌더링 엔진 사이의 동작 제어
  
  - **렌더링 엔진**
  
    - 요청한 콘텐츠 표시
  
    - W3C명세에 따하 해석
  
    - html요청이 들어오면 html, css를 파싱하여 화면에 표시
  
      ~~~
      - 파싱이란?
       :프로그램을 컴파일하는 과정에서 특정 프로그래밍 언어가 제시하는 문법을 잘 지켜 작성하였는지를 컴파일러가 검사하는 것
      ~~~
  
      
  
  - **네트워킹(통신)**
  
    - http 요청과 같은 네트워크 호출에 사용
  
  - **UI백엔드**
  
    - 플랫폼에서 명시하지 않은 일반적인 인터페이스
    - OS 사용자 인터페이스 체계를 사용
  
  - **자바스크립트 인터프리터**
  
    - 자바스크립트 코드를 해석하고 실행
  
  - **데이터 저장소**
  
    - 쿠키 등 모든 종류의 자원을 하드 디스크에 저장하는 계층

<br>

- #### 브라우저의 동작과정

  - 즉, 사용자가 선택한 자원을 해석하여 브라우저 화면에 띄우기까지의 과정 == 브라우저의 동작과정

  1. 브라우저가 서버로 부터 HTML, CSS, JS, 이미지 파일등을 응답받는다.
  2. HTML, CSS파일이 **<u>렌더링 엔진</u>**의 HTML파서와 CSS 파서에 의해 파싱된다.
  3. 파싱된 파일들이 DOM, CSSOM트리로 변환되고 렌더 트리로 결합된다.
  4. 이렇게 생성된 렌터 트리를 기반으로 브라우저가 웹페이지를 표시한다.

<br>

-----------------

- #### <u>렌더링 엔진</u>

  - 요청받은 내용을 브라우저 화면에 표시하는 역할

  - **렌더링 동작 과정**

    ![Rendering](https://user-images.githubusercontent.com/58902042/104292313-05c3a180-5500-11eb-8f28-acb90d1cb27a.png)

    1. DOM Tree 생성
    2. CSSOM 생성
    3. Render Trre(DOM + CSSOM) 생성
    4. Render Tree 배치
    5. Render Tree 그리기

- #### <u>Parsing</u>

  - 브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 것
  - 파싱 결과는 보통 문서 구조를 나타내는 Node Tree
  - 어휘 분석과 구문 분석 과정을 통해 파싱 트리를 구축

  <img src="https://user-images.githubusercontent.com/58902042/104293078-ef6a1580-5500-11eb-8119-c6ebe39c7136.png" height=300>

- #### <u>DOM Tree</u>

  - HTML의 내용과 속성을 Node로 갖고 각 Node의 관계를 나타내는 트리

  - 문서 마크업의 속성과 관계를 포함한다.

  - DOM은 마크업과 1:1관계를 맺는다.

    <img src="https://user-images.githubusercontent.com/58902042/104293974-fe04fc80-5501-11eb-854a-2cf63eef5952.png" weight =200 height=150>

    ![image](https://user-images.githubusercontent.com/58902042/104294105-24c33300-5502-11eb-95f3-750d4d17a668.png)

- #### <u>CCSSOM Tree</u>

  - DOM 생성과 마찬가지로 태그들을 토큰환, 토큰을 Node로 변환하여 CSSOM으로 변환
  - 브라우저가 모든 CSS를 파싱하고 처리할때까지 페이지가 화면에 그려지지 않는다.

- #### <u>Render Tree</u>

  - DOM+CSSOM, DOM의 Node에 일치하는 CSSOM규칙을 찾아 연결
  - 페이지를 렌더링하는 필요한 시각적인 Node만 포함한다.
    - 렌더러가 DOM요소에 부합하지만 1:1로 대응하는 것은 아니다.
    - 예를 들어<head>요소와 같은 비시각적인 DOM은 렌더 트리에 추가되지 않는다.
    - 또한 `display: none`스타일이 지정된 노드도 제외된다.

<br>

-------------------------------

<참조>

- <https://poiemaweb.com/js-browser>
- [브라우저 동작 과정에 대해 알아보자](https://kim6394.tistory.com/217)
- [[github.io] 브라우저 동작원리](https://yilpe93.github.io/Web/browser/)
- [브라우저는 어떻게 동작하는가?](https://d2.naver.com/helloworld/59361)

