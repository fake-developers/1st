## 브라우저의 동작 과정

<br>

### <u>웹 애플리케이션 구동 과정</u>

1. URL Entered : 사용자가 웹 브라우저에서 사이트 주소 입력
2. DNS Lookup : DNS를 이용하여 사이트 주소에 해당되는 Server IP 접근
3. Socket Connection : Client(브라우저)와 Server 간 접속을 위한 TCP 소켓 연결
4. HTTP Request : Client 에서 HTTP Header와 데이터가 서버로 전송
5. Content Download : 해당 요청이 Server에 도달하면 사용자가 원하는 문서를 다시 웹 브라우저에 전송
6. Browser Rendering : 웹 브라우저의 렌더링 엔진에서 해당 문서를  파싱

<br>

###  <u>브라우저 주요 기능</u>

사용자가 선택한 자원을 서버에 요청하고 받아 화면에 표시

- URI 입력하는 주소 표시 줄
- 이전 버튼, 다음 버튼
- 북마크(즐겨찾기)
- 새로고침 버튼
- 홈버튼

<br>

### <u>브라우저의 구조</u>

![browser](https://user-images.githubusercontent.com/61674527/104438829-c8c8df00-55d3-11eb-9df7-6eed43a54993.jpg)

~~~
- 사용자 인터페이스 : 주소표시줄, 이전/다음 버튼, 북마크 등 사용자가 활용하는 서비스들
- 브라우저 엔진 : 사용자 인터페이스와 렌더링 엔진 사이의 동작 제어
- 렌더링 엔진 : 요청한 콘텐츠 표시
- 통신 : http 요청과 같은 네트워크 호출에 사용 (플랫폼의 독립적인 인터페이스로 구성되어있음)
- UI 백앤드 : 플랫폼에서 명시하지 않은 일반적 인터페이스. 콤보 박스 창같은 기본적 장치를 그림
- 자바스크립트 해석기 : 자바스크립트 코드를 해석하고 실행
- 자료 저장소 : 쿠키 등 모든 종류의 자원을 하드 디스크에 저장하는 계층
~~~

<br>

###  <u>렌더링 </u>

#### <u>렌더링 엔진</u>

요청받은 내용을 브라우저 화면에 표시 
`웹킷, 게코 등`

#### <u>렌더링 주요 동작 과정</u>

렌더링 최적화의 과정은 항상 측정을 먼저하고 최적화를 진행해야한다.

![browser_render](https://user-images.githubusercontent.com/61674527/104438870-d716fb00-55d3-11eb-9fe0-10775c39afb7.jpg)

1. DOM Tree 생성
2. CSSOM 생성
3. Render Tree(DOM + CSSOM) 생성
4. Render Tree 배치
5. Render Tree 그리기

~~~
- DOM Tree : HTML의 내용과 속성을 Node로 갖고 각 Node의 관계를 나타내는 트리
- CSSOM : 태그들을 토큰화, 토큰을 Node로 변환하여 CSS Object Model로 변환한 것
          브라우저가 모든 CSS를 파싱하고 처리할 때까지 페이지가 화면에 그려지지 않는다.
~~~

~~~
Render Tree

DOM의 Node에 일치하는 CSSOM 규칙을 찾아 연결.
페이지를 렌더링하는 데 필요한 가시적인 Node만 포함.
화면에 최종적으로 그려지는 내용이 됨.
~~~



![webkit](https://user-images.githubusercontent.com/61674527/104438926-e5fdad80-55d3-11eb-8244-93d647882ab6.jpg)

####  <u>브라우저의 동작 과정</u>

사용자가 선택한 자원을 해석하여 브라우저 화면에 띄우기까지의 과정

1. 브라우저가 서버로부터 HTML, CSS, JS, 이미지 파일등을 응답받는다.
2. HTML, CSS 파일이 렌더링 엔진의 HTML 파서와 CSS 파서에 의해 파싱된다.
3. 파싱된 파일들이 DOM, CSSOM 트리로 변환되고 렌더 트리로 결합된다.
4. 이렇게 생성된 렌더 트리를 기반으로 브라우저가 웹페이지를 표시한다.

<br/>

### <u>파싱</u>

**문서 파싱은 브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 것**

파싱 결과는 보통 문서 구조를 나타내는 Node Tree이다.

* **어휘분석(Tokenizing)** : 문서의 자료를 토큰으로 분해하는 과정

* **구문 분석** : 언어의 구문 규칙을 적용하는 과정
  
  
  
  ![구문분석](https://user-images.githubusercontent.com/61674527/104439018-fc0b6e00-55d3-11eb-8d63-c4df902826c5.jpg)

<br>

<br>

<br>

### REFERENCE

* https://yilpe93.github.io/Web/browser/
* https://kim6394.tistory.com/217#recentEntries
* https://github.com/fake-developers/1st/blob/SJH-02/SJH/How%20browser%20rendering%20works.md

