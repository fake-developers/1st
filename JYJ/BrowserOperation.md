# 브라우저 동작 과정

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYe Bae, Jeonghea Shin*

<hr>


- <small><참고></small> <b>웹 애플리케이션이란?</b>

  - 웹 브라우저에서 이용할 수 있는 응용 소프트웨어이다.

  > 웹 애플리케이션 동작 과정
  >
  > 1. URL Entered : 사용자가 웹 브라우저에서 사이트 주소를 입력
  > 2. DNS Lookup : DNS를 이용하여 사이트 주소에 해당되는 Server IP 접근
  > 3. Socket Connection : 클라이언트 - 서버 간 접속을 위한 TCP 소켓 연결
  > 4. HTTP request : 클라이언트에서 HTTP Header와 데이터가 서버로 전송
  > 5. Content Download : 해당 요청이 Server에 도달하면 사용자가 원하는 문서를 다시 웹 브라우저에 전송
  > 6. Browser Rendering : 웹 브라우저의 렌더링 엔진에서 해당 문서를 파싱
  >
  > <img src='resources/browserParse.png' align='center' width='500px'>

<br/>

- <b>브라우저란?</b>

  - 인터넷 상에서 웹에 연결시켜 주는 윈도우 기반의 소프트웨어

    <small>ex) 인터넷 익스플로러, 사파리, 크롬, 오페라, 파이어 폭스 ... </small>

  <br/>

- <b>브라우저의 기능</b>

  - 사용자가 선택한 자원을 서버에 요청하고 화면에 받아오는 역할이다.
    - 자원은 보통 HTML 문서이나, PDF 또는 이미지 등 다른 형태일 수 있다.
    - 자원의 주소는 URI에 의해 정해진다.

<br/>

- <b>브라우저의 구조</b>

  <img src='resources/browserStruct.png' width='400px' align='center'>

  - 사용자 인터페이스 (UI)

    - 주소창, 즐겨찾기 등 사용자가 조작 가능한 영역이다.

    <br/>

  - 브라우저 엔진

    - 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어한다.

    <br/>

  - 렌더링 엔진

    - 요청한 콘텐츠를 표시하는 역할을 한다.
    - W3C 명세에 따라 해석한다.
    - HTML 요청이 들어오면 HTML, CSS를 파싱하여 화면에 표시한다.

    <br/>

  - 네트워킹

    - http 요청과 같은 네트워크 호출에 사용한다.

    <br/>

  - UI 백엔드

    - 플랫폼에서 명시하지 않은 일반적인 인터페이스이다.
    - OS 사용자 인터페이스 체계를 사용한다.

    <br/>

  - 자바스크립트 인터프리터

    - 자바 스크리트 코드를 해석하고 실행한다.

    <br/>

  - 데이터 저장소

    - 쿠키 등 모든 종류의 데이터 자원을 하드 디스크에 저장하는 계층이다.

  <br/>

  <br/>

- <b>브라우저의 동작 과정</b>

  <small>사용자가 선택한 자원을 해석하여 브라우저에 띄우기까지의 과정</small>

  1. 브라우저가 서버로부터 HTML, CSS, JS, 이미지 파일 등을 응답 받는다.
  2. HTML, CSS 파일이 렌더링 엔진* 의 HTML 파서와 CSS 파서에 의해 파싱된다.

  3. 파싱된 파일들이 DOM, CSSOM 트리로 변환되고, 렌더 트리로 결합된다.

  4. 이렇게 생성된 렌더 트리를 기반으로 브라우저가 웹 페이지를 표시한다.

  <br/>

  <hr>

  > 렌더링 엔진
  >
  > - 요청받은 내용을 브라우저 화면에 표시하는 역할을 한다.
  >
  > - 렌더링 동작 과정 
  >
  >   <img src='resources/rendering.png' width='500px' align='center'>
  >
  >   1. DOM tree 생성
  >   2. CSSOM 생성
  >   3. 렌더 트리 생성 (DOM + CSSOM)
  >   4. 렌더 트리 배치
  >   5. 렌더 트리 그리기

  <br/>

  > 파싱
  >
  > - 브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 것이다.
  > - 파싱 결과는 보통 문서 구조를 나타내는 Node Tree이다.
  > - 어휘 분석과 구문 분석 과정을 통해 파싱 트리를 구축한다.
  >
  > <img src='resources/parsing.png' width='100px' align='cetner'>

  <br/>

  > DOM Tree
  >
  > - HTML 내용과 속성을 Node로 갖고 각 Node의 관계를 나타내는 트리이다.
  > - 문서 마크업의 속성과 관계를 포함한다.
  > - DOM은 마크업과 1:1 관계를 맺는다.
  >
  > <img src='resources/domtreecode.png' width='400px' align='cetner'>
  >
  > <br/>
  >
  > <img src='resources/domtreenode.png' width='400px' align='cetner'>
  >
  > <br/>
  >
  > <br/>
  >
  > CSSOM Tree
  >
  > - DOM 생성과 마찬가지로 태그들을 토큰화한 것을 Node로 변환하여 CSSOM으로 변환
  > - 브라우저가 모든 CSS를 파싱하고 처리할 때까지 페이지가 화면에 그려지지 않는다.
  >
  > <br/>
  >
  > Rendering Tree
  >
  > - DOM 과 CSSOM을 결합한 것으로, DOM의 각 Node에 일치하는 CSSOM 규칙을 찾아 연결한다.
  >
  > - 페이지를 렌더링하는 필요한 시각적인 Node만 포함한다.
  >
  >   - 렌더러가 DOM 요소에 부합하지만 1:1로 대응하는 것은 아니다.
  >
  >   - 예를 들어, 요소와 같은 비시각적인 DOM은 렌더 트리에 추가되지 않는다.
  >
  >   - 또한, <code>display: none</code> 스타일이 지정된 노드도 제외된다.
  >
  >     <small>display: none은 자리를 차지하지 않는다. 반면에 visibility: hidden은 자리는 차지하지만, 눈에 보이지는 않아 노드가 존재한다.</small>

<br/>

## 예상질문❔

Q1) 브라우저의 동작 과정을 설명해라.

A1) 브라우저가 서버로부터 HTML, CSS, JS, 이미지 파일 등을 응답 받으면 해당 파일이 렌더링 엔진 의 HTML 파서와 CSS 파서에 의해 파싱되어  DOM, CSSOM 트리로 변환된다. 이 두 트리는 렌더 트리로 결합된다. 이 렌더 트리를 가지고 웹 브라우저에 표시하는 것이다.

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/SJH/How%20browser%20rendering%20works.md
- https://github.com/fake-developers/1st/blob/main/BJY/Browser%20Working%20Process.md
