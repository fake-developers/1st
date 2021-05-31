# JSON

- JavaScript Object Notation이라는 의미의 축약어
- 데이터를 저장하거나 전송할 때 많이 사용되는 **경량의 DATA 교환 형식**
- **속성-값 쌍으로 이루어진 데이터 오브젝트를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷**
- 비동기 브라우저/서버 통신([AJAX](./AJAX.md))을 위해, 넓게는 XML을 대체하는 주요 데이터 포맷 

- 텍스트 기반이므로 어떠한 프로그래밍 언어에서도 JSON 데이터를 읽고 사용할 수 있다.
- 공식 인터넷 미디어 타입은 `application/json` 이며, JSON의 파일 확장자는 `.json`이다.

<BR>

## JSON 특징

- 자바스크립트를 기반으로 확장하여 만들어졌다.
- 자바스크립트 객체 표기법을 따른다.
- 자바스크립트의 문법과 굉장히 유사하지만 **텍스트 형식** 일 뿐이다.
- 프로그래밍 언어와 운영체제에 독립적이다.

<br>

## JSON 문법

- JSON은 자바스크립트의 객체 표기법에서 리터럴(literal)과 프로퍼티(property)를 표현하는 방식만 가져와서 사용한다.

  - 리터럴(literal)

    - 변수와 다르게 해석되는 값 그 자체

      ~~~javascript
      12 //숫자 리터럴
      "JSON" //문자 리터럴
      TRUE // BOOLEAN 리터럴
      ~~~

      \> 프로퍼티 값에 리터럴 그 자체가 들어간다는 것

  - 프로퍼티(property)

    - 객체 내부의 속성

      ~~~javascript
      {
      	"name": "식빵"
      	"family" : "웰시코기"
      }//두 쌍의 프로퍼티를 가지는 객체
      ~~~

- 따라서, 브라우저 영역세어도 쉽고 빠르게 그 의미를 해석할 수 있으며, 다른 프로그래밍 언어에서도 구현하기 쉽다.

- 데이터의 값으로는 다음과 같은 타입이 올 수 있다.

  1. 숫자(number)
  2. 문자열(string)
  3. 불리언(boolean)
  4. 객체(object)
  5. 배열(array)
  6. NULL

<BR>

## JSON 구조

- JSON은 자바스크립트의 객체 표기법으로부터 파생된 부분 집합
- 따라서,  JSON데이터는 자바스크립트 객체 표기법에 따른 구조로 구성된다.
  1. JSON 데이터는 key / value가 존재할 수 있으며 key값이나 문자열은 항상 쌍따옴표를 이용하여 표기
  2. JSON 데이터는 쉼표(,)로 나열된다.
  3. 객체는 중괄호({})로 둘러쌓아 표현한다.
  4. 배열은 대괄호([])로 둘러쌓아 표현한다.

<BR>

## JSON 형식

**1. name-value형식의 쌍 (객체)**

- 중괄호({})로 둘러쌓아 표현

- 쉼표(,)를 사용하여 여러 프로퍼티를 포함

  - 4개의  프로퍼티를 가지는 JSON 객체

  ~~~JSON
  {
  	"name": "식빵",
      "family": "웰시코기",
      "age": 1,
      "weight": 2.14
  }
  ~~~

  - 객체안에 객체 -> 계층 구조 형성

  ~~~JSON
  {
      "dog": {
          "name": "식빵",
          "family": "웰시코기",
          "age": 1,
          "weight": 2.14,
          "owner": {
              "ownerName": "홍길동",
              "phone": "01012345678"
          }
      }
  }
  ~~~

  

  - JSON 객체를 그림으로 나타내면 다음과 같다.

  <img src="https://user-images.githubusercontent.com/58902042/116865588-dec2e400-ac44-11eb-8a71-ac942d4ce589.png" height=120> 

**2. 값들의 순서화된 리스트 형식 (배열)**

- 대괗로([])로 둘러쌓아 표현

- 쉼표(,)를 사용하여 여러 JSON 데이터를 포함

  - 배열이름 "hobby", 2개의 문자열 요소를 가지는 JSON 배열

  ~~~JSON
  {
    "firstName": "Kwon",
    "lastName": "YoungJae",
    "email": "kyoje11@gmail.com",
    "hobby": ["puzzles","swimming"]
  }
  ~~~

  - 배열이름 "dog", 3개의 JSON 객체를 요소로 가지는 JSON 배열

  ~~~JSON
  "dog": [
      {"name": "식빵", "family": "웰시코기", "age": 1, "weight": 2.14},
      {"name": "콩콩", "family": "포메라니안", "age": 3, "weight": 2.5},
      {"name": "젤리", "family": "푸들", "age": 7, "weight": 3.1}
  ]
  ~~~

  - JSON 배열을 그림으로 그리면 다음과 같다.

  <img src="https://user-images.githubusercontent.com/58902042/116865977-9821b980-ac45-11eb-8d0e-580646c86fd6.png" height=120> 

<BR>

## JSON의 문제점

- AJAX는 단순히 데이터만 받는 것이 아니라 JavaScript 그 자체도 전달가능
  - 즉, **JSON 데이터를 받았는데 그것이 단순 데이터가 아니라 JavaScript가 될 수 있다는 뜻(데이터 인줄 알고 받았는데 악성 스크립트가 될 수** 있다.)
  - 위와 같은 이유로 받은 내용에서 순수하게 데이터만 추출하기 위한 JSON 관련 라이브러리를 따로 사용하기도 한다.
- XML 문서는 XML [DOM](./BOM&DOM.md) 을 이용하여 해당문서에 접근한다.
  - JSON은 문자열을 전송받은 후 해당 문자열을 바로 파싱하므로, 속도는 더 빠르다.
  - 하지만,  JSON은 **전송받은 데이터 무결성을 사용자가 직접 검증** 해야 한다.
  - 따라서 데이터의 검증이 필요한 곳에서는 아직 XML문서를 더 많이 사용한다.
- JSON으로 가져올 수 있는 데이터는 **해당 자바스크립트가 로드된 서버의 데이터에 한정** 된다.
  - JSON은 단순히 데이터 포맷일 뿐이며 그 데이터를 불러오기 위해서는 XMLHttpRequest()라는 JavaScript 함수를 사용해야 하는데 이 함수가 동일 서버에 대한 것만 지원하기 때문이다.

<br>

## JSON 형식 텍스트 JavaScript Object로 변환하기

~~~json
var jsonText = '{ "name": "Someone else", "lastName": "Kim" }';  // JSON 형식의 문자열
var realObject = JSON.parse(jsonText);
var jsonText2 = JSON.stringify(realObject);
~~~

- **JSON.parse( JSON으로 변환할 문자열 )** : JSON 형식의 텍스트를 자바스크립트 객체로 변환한다.
- **JSON.stringify( JSON 문자열로 변환할 값 )** : 자바스크립트 객체를 JSON 텍스트로 변환한다.

-----------

**<참조>**

- [JSON이란 무엇인가?](https://velog.io/@surim014/JSON%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)

- [JSON이란?](https://genesis8.tistory.com/195)
- [JSON 문법](https://tcpschool.com/json/json_basic_syntax)

