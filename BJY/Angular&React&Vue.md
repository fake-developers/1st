## Angular, React, Vue

<br>

~~~
SPA

서버로부터 처음에만 페이지를 받아오고 이후에는 동적으로 페이지를 구성해서 새로운 페이지를 받아오지 않는 웹 애플리케이션
~~~

<br>

### <u>Angular, React, Vue</u>

대표적인 SPA 라이브러리

***

### <u>Angular</u>

`Google`

#### <u>특징</u>

* 완전한 프레임워크로, 프로젝트의 생성, 테스트 빌드, 배포를 위한 모든 기능을 제공한다.
* TypeScript를 사용한다.
* `Angular CLI`를 제공하여 개발환경을 지원한다. 파일 생성, 빌드, 패키징, 라이트 서버 기능 등 개발에 필요한 거의 모든 기능을 자체적으로 제공
* 모듈과 컴포넌트 기반으로 동작한다.
* 웬만한 기능의 라이브러리는 모두 포함시켜서 자체적으로 제공한다.  (라우팅, HTTP, Form 등)
* SSR을 위한 기능을 구비하고 있다.

~~~
Angular CLI

기본 구조, 컴포넌트 생성, 빌드, 유닛테스트, 개발서버, 배포를 관리할 수 있도록 도와주는 커멘드라인 인터페이스.
~~~

#### <u>장점</u>

* **프레임워크다.**
  * 개발에 필요한 모든 것이 거의 갖추어져 있다.
* **유지 관리가 용이하다.**
  * 코드 유지 관리성 -> TypeScript를 사용
  * 지속적인 기술 지원
  * 스타일에 맞춘 코딩
* **Angular CLI**
  * 프로젝트 생성을 도와준다. 
    명령어 하나로 프로젝트를 생성하고 알아서 모든 의존성 패키지를 함께 설치해준다.
  * 라이트한 서버 제공
  * Webpack 내장,  빌드, 컴파일, 자바스크립트 압축을 알아서 해준다.
* **모바일 앱 용 대안이 있다**.
  * Native Script
  * Ionic

#### <u>단점</u>

* **프레임워크다.**
  * 앵귤러만의 패턴 존재.
* **학습 곡선**
  * 어렵고 복잡하고 공부할 것이 많다.

#### <u>언제 사용하는가?</u>

* **사용자와의 interaction이 풍부한 애플리케이션**
  
  기능이 복잡한 경우에 기존의 방식(jQuery)으로 작성보다 Angular을 통해 생산성 향상 가능
* **엔터프라이즈 규모의 애플리케이션**
  
  코딩하는 스타일이 정해져 있어서 여러 명이 동시에 개발하는 경우

***

### <u>React</u>

`Facebook`

#### <u>특징</u>

* Component 기반이다. 
  `UI를 구성하는 개별적인 View 단위`
* 라이브러리의 특성을 갖는다.
* 단일방향 테이터 흐름 & Flux
* `JSX`
* `Props & State`
* `Virtual DOM`

~~~
JSX (Javascript + XML)

자바스크립트에 대한 확장 구문으로서 리액트에 element를 제공해준다.
~~~

~~~
Props & State

데이터를 사용할 때 다루는 개념
- props : 부모 컴포넌트가 자식 컴포넌트에 값을 전달할 때 사용. 읽기 전용 
- state : 컴포넌트 자기 자신이 가지고 있는 값이다. setState()로 값 변경 가능
~~~

<img width="400" src="https://user-images.githubusercontent.com/61674527/104439292-4bea3500-55d4-11eb-81fc-8aa47ed0e273.jpg">

~~~
Virtual DOM

DOM의 상태 메모리에 저장하고 변경 전과 변경 후의 상태를 비교한 뒤 최소한의 내용만 반영하는 기능. 
가상 DOM은 DOM의 상태를 메모리 위에 계속 올려두고 DOM에 변경이 있을 때만 변경 반영
~~~

#### <u>장점</u>

* **Component**
  * 생산성과 유지 보수를 용이하게 한다.
* **Virtual DOM**
  * 어플리케이션의 성능 향상
* **다른 프레임워크와 혼용 가능**
  * 프레임워크가 아닌 라이브러리이기 때문
* **브라우저측의 초기 렌더링 딜레이를 줄임**
  * 서버 & 클라이언트 사이드 렌더링 지원

#### <u>단점</u>

* **VIEWONLY,VIEW 이외 기능**
  * Third party library(=패키지,모듈)을 이용하거나 직접 구현해야 한다.
* **IE8 이하 지원하지 않음**

#### <u>언제 사용하는가?</u>

* **지속해서 데이터가 변화하는 대규모 애플리케이션 구축**

***

### <u>Vue</u>

#### <u>특징</u>

* UI 화면단 라이브러리. `MVVM패턴`의 뷰 모델에 해당.
* 컴포넌트 기반 프레임워크
* Angular의 양방향 데이터 바인딩과 React의 단방향 데이터 흐름의 장점을 결합함
* Angular, React에 비해 나중에 만들어졌지만 빠른 속도로 성장 중이다.

~~~
MVVM : 모델(Model)-뷰(View)-뷰 모델(View Model) 

뷰(View) : 보이는 화면
돔(DOM) : html문서에 들어가는 요소(tag, class, attributes)
돔 리스너(DOM Listener) : 돔 변경 내역에 따라 즉각 반영하여 로직 수행
모델(Model) : 데이터
데이터 바인딩(Data Binding) : view에 표시되는 내용과 모델 데이터 동기화
뷰 모델(View Model) : 뷰와 모델의 중간 영역
~~~

![mvvm](https://user-images.githubusercontent.com/61674527/104439376-60c6c880-55d4-11eb-978d-e45916821ffd.jpg)

#### <u>장점</u>

* **개발 과정에서 원하는 것을 정확하게 이용**
  * 코드가 깔끔하고 배우기 쉽기 때문이다.
* **유연하고 가벼움.**
* **전체 아키텍처를 새롭게 구성할 필요가 없다**
  * angular와 달리 기존의 웹 어플리케이션의 일부 UI만 적용하는것이 가능
* **빠른 UI렌더링이 가능**
  * react와 마찬가지로 가상 DOM 지원

#### <u>단점</u>

* **TypeScript와의 결합이 용이하지 않음**
* **템플릿 특성**
  * 런타임 에러가 나기 쉽다
  * 테스트 하기 어려움
  * 재구조화가 쉽지 않다.
* **작은 개발 생태계**

#### <u>언제 사용하는가?</u>

* **작은 규모의 어플리케이션 개발**

<br>

<br>

<br>

### REFERENCE

* https://paperblock.tistory.com/52
* https://medium.com/react-native-seoul/react-%EB%A6%AC%EC%95%A1%ED%8A%B8%EB%A5%BC-%EC%B2%98%EC%9D%8C%EB%B6%80%ED%84%B0-%EB%B0%B0%EC%9B%8C%EB%B3%B4%EC%9E%90-01-react-js%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-ad8ba252ee28
* https://velog.io/@jinsk9268/React-%EB%9E%80
* https://jw910911.tistory.com/41
* https://hyejin-dev.tistory.com/3
* https://studyingych.tistory.com/52
* https://velog.io/@leyuri/Vue.js-%EC%86%8C%EA%B0%9C
* https://mkil.tistory.com/435
* https://wickies.tistory.com/120

