# 자바스크립트 동작 원리

- ### 들어가기 앞서

  - **자바스크립트를 처리하는 과정**
    1. 브라우저가 서버로부터 받은 HTML,CSS, JS 파일등을 응답받은후,
    
    2. HTML,CSS는 렌더링 엔진으로 파싱되고 JS는 자바스크립트 엔진으로 처리된다.
    
    3. THML파서가 script 태그를 만나면 자바스크립트 코드를 실행 하기 위해 DOM 생성 프로세스를 중지하고 자바스크립트 엔진으로 제어 권한을 넘긴다.
    4. 제어 권한을 받은 자바스크립트 엔진이 script태그 내의 자바스크립트 코드 또는 자바스크립트 파일을 로드하고 파싱하여 실행한다. 
    5. 자바스크립트의 실행이 완료되면 다시 HTML 파서로 제어 권한을 넘겨 브러우저가 중지했던 시점부터 DOM 생성을 재개한다.

<br>

- ### 자바스크립트

  - Java Script는 단 하나의 호출스택을 사용하는 **싱글 스레드**이다.
  - **콜백을 사용**한다.
  - 즉, **단일 스레드 프로그래밍 언어**라는 뜻

   ~~~
    <논 블로킹>
    - 통신이 완료될 때까지 기다리지 않고 다른 작업을 수행할 수 있다.
   ~~~

<br>


- ### 자바스크립트 런타임

  ![runtime](https://user-images.githubusercontent.com/58902042/104404050-2988f500-559d-11eb-8ee3-febb9b08da31.PNG)

  - **<u>자바 스크립트 엔진</u>**

    - Memory Heap과 Call stack으로 구성되어 있다.
    
    - 자바스크립트가 Call stack이 하나이기때문에 **stack overflow**가 발생할 수 있다.
    
      `=> 이것에 대한 해결 방안이 비동기 콜백`
  - **<u> Web APIs</u>**
    
    - 브라우저에서 제공하는 API
    - Call Stack에서 실행된 비동기 함수가 Web API를 호출하고
    - Web API는 Callback Queue에 콜백함수를 순차적으로 적재한다.
    
  - **<u> Callback Queue</u>**

    - Event 실행 관리를 위해 사용되는 Queue

  - **<u> Event Loop</u>**

    - Callback Event Queue에서 하나씩 꺼내 동작시키는 Loop
    - Call Stack과 Callback Queue의 상태를 체크하여 
    - Call Stack이 빈 상태가 되면 Callback Queue의 첫번째 콜백을 Call Stack으로 넣어준다.
    
  - **<예제>**
  
    <small>이미지를 클릭해야 끝까지 움직입니다.</small>
  
  ![runtime](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdd1dcM%2FbtqKMOtNjTd%2FrvlcflUHVxvLncUJ8dNAp1%2Fimg.gif)
  

<br>

>- ### 자바스크립트 엔진
>
> - JavaScript로 작성한 코드를 해석하고 실행하는 인터프리터
>   
>   - ex. V8
>
>​											<img src = "https://user-images.githubusercontent.com/58902042/104337354-bea5d280-5538-11eb-95a1-66e502815913.PNG" height=300 width=300>
>
>- **자바스크립트 엔진 구성요소**
>
>  - Memory Heap : 메모리 할당이 일어나는 곳
>
>  - Call Stack : 호출 스택이 쌓이는 곳
>
>​    
>
>
>- **자바스크립트 엔진의 구동방식**
>
>![JS Engine](https://user-images.githubusercontent.com/58902042/104334094-4ee21880-5535-11eb-8ccb-c6bd59f200e4.PNG)
>
>1. 자바스크립트 소스코드를 가져와 Parser에게 넘긴다.
>
>2. Parser는 파싱을 통해 AST(Abstract Syntax Tree)로 변환시킨다.
>
>3. AST를 인터프리터(lgnition)를 통해 byte code로 변환하여 실행한다.
>
>4. 그 동안, 프로파일러는 입력받은 코드에서 최적화할 수 있는 >부분을 찾아 기록한다.
>
>5. 최적화한 코드를 수행할 차례가 다가오면, byte code >대신 컴파일러가 변환한 Optimized code로 수행한다.
>
>    ~~~
>    <Parser>
>    : 코드의 의미를 이해하기 위해 token이라는 작은 단위들로 코드를 쪼개는 일
>    <AST>
>    : Parsser에서 분해된 token들을 기반으로 트리구조 생성
>    ~~~



<br>

----------

<참조>

- [javascript 동작원리](https://velog.io/@namezin/javascript-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC)
- [[JS]자바스크립트의 작동원리](https://frontcode.tistory.com/30?category=685416)
- [JavaScript의 동작원리를 살펴봅시다.](https://medium.com/humanscape-tech/javascript-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC%EB%A5%BC-%EC%82%B4%ED%8E%B4%EB%B4%85%EC%8B%9C%EB%8B%A4-aef465c9c43)
- [자바스크립트 동작원리와 이벤트 루프](https://kyung-a.tistory.com/11)
- [브라우저 동작 원리](https://poiemaweb.com/js-browser)

