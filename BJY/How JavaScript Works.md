## 자바스크립트의 동작 원리

<br>

### <u>자바스크립트 엔진</u>

Call Stack, Task  Queue(Event Queue), Memory Heap 이라는 세가지 영역으로 구분된다.

~~~
엔진의 주요 2개 구성요소

- Memory Heap : 메모리 할당이 일어나는 곳
- Call Stack : 호출 스택이 쌓이는 곳

+
Event Loop로 Task Queue의 task들을 관리할 수 있다.
~~~

![js_engine](https://user-images.githubusercontent.com/61674527/104438502-6a9bfc00-55d3-11eb-80e4-966b5fffb196.jpg)

> 자바스크립트 엔진의 대표적인 예는 Google V8 엔진이다. V8은 Chrome과 node.js에서 사용한다.

<br>

### <u>런타임</u> 

거의 모든 자바스크립트 개발자들이 setTimeout과 같은 브라우저 내장 API를 사용한다.

하지만, 이 API를 자바스크립트 엔진에서 제공하지 않는다.

![js-engine-runtime](https://user-images.githubusercontent.com/61674527/104438563-7ab3db80-55d3-11eb-8a79-a48732ad504c.jpg)

자바스크립트 엔진 이외에도 자바스크립트에 관여하는 다른 요소가 많다.

DOM, Ajax, setTimeout과 같이 브라우저에 제공하는 API들을 Web API라고 한다.

> Ajax : 비동기식 자바스크립트와 xml. 브라우저가 가지고있는 XMLHttpRequest 객체를 이용해서 전체 페이지를 새로 고치지 않고도 페이지의 일부만을 위한 데이터를 로드하는 기법
>
> setTimeout() : 일정 시간 후에 특정 코드, 함수를 의도적으로 지연한 뒤 실행하고 싶을 때 사용

![runtime](https://user-images.githubusercontent.com/61674527/104820868-364a6900-587b-11eb-8c8e-8f423625d204.gif)

<br>

### <u>호출 스택(Call Stack)</u>

코드가 실행되면서 스택 프레임이 쌓이는 장소.
자바스크립트는 기본적으로 싱글 쓰레드 기반 언어 = 호출 스택이 하나. 이러한 특징으로 함수가 실행되는 방식을 "Run to Completion"이라고 한다. 단 하나의 함수가 실행되면, 해당 함수의 실행이 끝날 때까지 다른 어떤 Task들도 수행될 수 없다는 것을 의미한다.

어떤 요청이 들어올 때마다 해당 요청을 순차적으로 Call Stack에 담아 처리한다. 메소드가 수행될 때, Call Stack에 새로운 프레임이 Push되고 메소드의 실행이 끝나면 해당 프레임은 Pop 된다.

~~~javascript
function add(x, y){
   return x+y;
}
function first(){
   var i = add(1,1); 
   console.log(i);
}
first();
~~~

![call_stack](https://user-images.githubusercontent.com/61674527/104438619-87383400-55d3-11eb-9870-b8ad38011bdc.jpg)

![call_stack_overflow](https://user-images.githubusercontent.com/61674527/104438668-961ee680-55d3-11eb-8f78-003895417904.jpg)

<br>

### <u>Heap</u> 

동적으로 생성된 객체(인스턴스)가 할당되는 곳.

동적으로 할당되는 변수의 경우, 컴파일러는 얼마나 많은 메모리를 필요로 할 지 알 수 없어서, 스택에 변수를 위한 공간을 할당할 수 없다. 컴파일러는 동적 변수를 런타임 시점에 Heap공간에 할당받는다.

<br>

### <u>Task Queue(Event Queue)</u>

런타임 환경에서는 처리해야하는 Task들을 임시로 저장하는 대기 Queue.

Event Loop는 Call Stack과 Task Queue의 상태를 체크하여, Call Stack이 비어 있을 때,
Task Queue의 첫번째 콜백을 Call Stack으로 밀어넣는다.

<br>

***

<em>자바스크립트는 싱글 스레드 프로그래밍 언어라 한번에 하나의 작업만 수행한다. 하지만 Web API, TaskQueue, EventLoop 덕분에 멀티 스레드처럼 실행하듯 보여진다.</em>

<br>

<br>

<br>

### REFERENCE

* https://joshua1988.github.io/web-development/translation/javascript/how-js-works-inside-engine/#%EB%93%A4%EC%96%B4%EA%B0%80%EA%B8%B0
* [setTimeout()](https://webisfree.com/2014-04-08/[javascript]-%EC%8B%9C%EA%B0%84-%EC%A7%80%EC%97%B0-%ED%95%A8%EC%88%98-%EC%9D%BC%EC%A0%95-%EC%8B%9C%EA%B0%84-%EB%92%A4-%EC%8B%A4%ED%96%89%EC%8B%9C%ED%82%A4%EA%B8%B0-settimeout()-%7B%7D)
* https://coding-factory.tistory.com/143
* https://medium.com/humanscape-tech/javascript-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC%EB%A5%BC-%EC%82%B4%ED%8E%B4%EB%B4%85%EC%8B%9C%EB%8B%A4-aef465c9c43
* https://velog.io/@ksh4820/Event-Loop
* https://github.com/fake-developers/1st/blob/SJH-02/SJH/How%20JavaScript%20works.md

