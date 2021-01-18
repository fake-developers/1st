# 자바스크립트 동작 원리

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYe Bae, Jeonghea Shin*

<hr>


- <b>자바스크립트</b>

  - 단 하나의 호출 스택을 사용하는 싱글 스레드이다.

  - <b>콜백</b>을 사용한다.

  - 논 블로킹* 특징을 가지고 있다.

    ```
    통신이 완료될 때까지 기다리지 않고 다른 작업을 수행하는 것
    ```

  <br/>

- <b>자바스크립트를 처리하는 과정</b>

  - 브라우저가 서버로부터 받은 HTML, CSS, JS 파일 등을 응답 받는다.
- HTML, CSS는 렌더링 엔진으로 파싱되고 JS는 자바스크립트 엔진으로 처리된다.
  - HTML 파서가 script 태그를 만나면 자바스크립트 코드를 실행하기 위해 DOM 생성 프로세스를 중지하고 자바스크립트 엔진으로 제어 권한을 넘긴다.
- 제어 권한을 받은 자바스크립트 엔진이 script 태그 내의 자바스크립트 코드 또는 자바스크립트 파일을 로드하고 파싱하여 실행한다.
  - 자바스크립트의 실행이 완료되면 다시 HTML 파서로 제어 권한을 넘겨 브라우저가 중지했던 시점부터 DOM 생성을 재개한다.

<br/>

- <b>자바스크립트 런타임</b>

  <img src='resources/jsRuntime.png' align='center' width='500px'>

  - 거의 모든 자바스크립트 개발자들이 setTimeout과 같은 브라우저 내장 API를 사용하는데, 이 API를 자바스크립트 엔진에서 제공하지 않는다.

  - 자바스크립트 엔진

    - 자바스크립트로 작성한 코드를 해석하고 실행하는 인터프리터이다.
    - Memory Heap과 Call stack으로 구성되어 있다.
    - 자바스크립트가 Call stack이 하나이기 때문에 stack overflow가 발생할 수 있다.
      - 이를 비동기 콜백으로 해결할 수 있다.

    > 자바스크립트 엔진의 구동 방식
    >
    > <img src='resources/jsEngine.png' width='450px' align='center'>
    >
    > 1. 자바스크립트 코드를 가져와 Parser에게 보낸다.
    > 2. Parser는 파싱을 통해 AST(Abstract Syntax Tree)로 변환시킨다.
    > 3. AST를 인터프리터를 통해 바이트코드로 변환하여 실행한다.
    > 4. 실행되는 동안 프로파일러는 입력받은 코드에서 최적화할 수 있는 부분을 찾아 기록한다.
    > 5. 최적화한 코드를 수행할 차례가 오면 바이트 코드 대신 컴파일러가 변환한 Optimized code로 수행한다.

    <br/>

  - Call Stack

    - 요청이 들어올 때마다 해당 요청을 순차적으로 Call Stack에 담아 처리한다.
    - 메소드가 수행될 때, Call stack에 새로운 프레임이 Push 된다.
    - 메소드가 끝나면 해당 프레임은 Pop 된다.

    <br/>

  - Heap

    - 동적으로 생성된 객체 (인스턴스)가 할당되는 곳이다.
    - 컴파일러는 동적 변수를 런타임 시점에 Heap 공간에 할당 받는다.

  - Web APIs

    - 브라우저에서 제공하는 API <small>ex) Ajax, DOM, setTimeout ... </small>

      > Ajax 
      >
      > ``` 
      > 비동기식 자바스크립트와 xml로, 브라우저의 XMLHttpRequest 객체를 이용해 전체 페이지를 새로 고치지 않고도 페이지 일부만을 위한 데이터를 로드하는 기법이다.
      > ```
      >
      > <br/>
      >
      > setTimeout()
      >
      > ```
      > 일정 시간 후에 특정 코드, 함수를 의도적으로 지연한 뒤 실행하고 싶을 때 사용한다.
      > ```

    - Call Stack에서 실행된 비동기 함수가 Web API를 호출한다.

    - Web API는 Callback Queue에 콜백함수를 순차적으로 적재한다.

    <br/>

  - Callback Queue

    - Event 실행 관리를 위해 사용되는 큐이다.

    <br/>

  - Event Loop

    - Callback Event Queue에서 하나씩 꺼내 동작시키는 Loop이다.
    - Call Stack과 Callback Queue의 상태를 체크한다.
    - Call Stack이 빈 상태가 되면 Callback Queue의 첫번째 콜백을 Call Stack으로 넣어준다.

  <br>

  

<br/>

## 예상질문❔

Q1) 자바스크립트 엔진은 무엇인가?

A1) 자바스크립트로 작성한 코드를 해석하고 실행하는 인터프리터로, Memory Heap과 Call stack으로 구성되어 있다.

<br/>

Q2) 자바스크립트 런타임은 무엇인가?

A2) 자바스크립트 개발자들이 주로 사용하는 내장 API 등의 도구를 제공하는 자바스크립트 구동 환경이다.

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/SJH/How%20JavaScript%20works.md
- https://github.com/fake-developers/1st/blob/main/BJY/How%20JavaScript%20Works.md
