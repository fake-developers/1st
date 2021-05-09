# [JavaScript] JSON

:writing_hand: *Assembled by JiYoung-Kwon (2021-05-09)* 

<br/>

## 1. JSON이란?

* JavaScript Object Notation의 약자
* 데이터를 저장하거나 전송할 때 많이 사용되는 **경량의 DATA 교환 형식**
* **속성-값 쌍으로 이루어진 데이터 오브젝트를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷**
* JavaScript에서 객체를 만들 때 사용하는 표현식을 의미
* 비동기 브라우저/서버 통신([AJAX](https://github.com/fake-developers/1st/blob/SJH-10/SJH/AJAX.md))을 위해, 넓게는 XML을 대체하는 주요 데이터 포맷
* 텍스트 기반이므로 어떠한 프로그래밍 언어에서도 JSON 데이터를 읽고 사용할 수 있음
* 공식 인터넷 미디어 타입은 `application/json` 이며, JSON의 파일 확장자는 `.json`임
* JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작아서, 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 사용됨

<br/>

## 2. JSON의 특징

1. 자바스크립트를 기반으로 확장하여 만들어졌음
2. 자바스크립트 객체 표기법을 따름
3. 자바스크립트의 문법과 굉장히 유사하지만 **텍스트 형식** 일 뿐임
4. 프로그래밍 언어와 운영체제에 독립적임
5. 서버와 클라이언트 간의 교류에서 일반적으로 많이 사용됨
6. 자바스크립트를 이용하여 JSON 형식의 문서를 쉽게 자바스크립트 객체로 변환할 수 있는 이점이 있음

<br/>

## 3. JSON 문법

- JSON은 자바스크립트의 객체 표기법에서 리터럴(literal)과 프로퍼티(property)를 표현하는 방식만 가져와서 사용함

  - 리터럴(literal)

    - 변수와 다르게 해석되는 값 그 자체

      ```json
      12 //숫자 리터럴
      "JSON" //문자 리터럴
      TRUE // BOOLEAN 리터럴
      ```

      \> 프로퍼티 값에 리터럴 그 자체가 들어간다는 것

  - 프로퍼티(property)

    - 객체 내부의 속성

      ```json
      {
      	"name" : "식빵",
      	"family" : "웰시코기"
      } //두 쌍의 프로퍼티를 가지는 객체
      ```

- 따라서, 브라우저 영역에서도 쉽고 빠르게 그 의미를 해석할 수 있으며, 다른 프로그래밍 언어에서도 구현하기 쉬움

- 기본 자료형

  * 수(Number)
  * 문자열(String)
  * 참/거짓(Boolean)
  * 배열(Array)
  * 객체(Object)
  * NULL

<br/>

## 4. JSON 구조

* JSON은 자바스크립트의 객체 표기법으로부터 파생된 부분 집합
* 따라서, JSON데 이터는 자바스크립트 객체 표기법에 따른 구조로 구성됨
  1. JSON 데이터는 key / value가 존재할 수 있으며,  key값이나 문자열은 **항상 쌍따옴표를 이용하여 표기**
  2. JSON 데이터는 쉼표(,)로 나열됨
  3. 객체는 중괄호({})로 둘러쌓아 표현
  4. 배열은 대괄호([])로 둘러쌓아 표현

<br/>

## 5. JSON 형식

1. name-value 형식의 쌍 (pair)
   * 여러가지 언어들에서 object, hashtable, struct로 실현되었음
   * `{String key : String Value}`
   * 쉼표(,)를 사용하여 여러 프로퍼티를 포함

  ```json
// 3개의 프로퍼티를 가지는 JSON 객체
{
    "firstName": "Kwon",
    "lastName": "YoungJae",
    "email": "kyoje11@gmail.com"
 }

// 객체 안에 객체 -> 계층 구조 형성
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
  ```

2. 값들의 순서화된 리스트 형식
   * 여러가지 언어들에서 배열(Array), 리스트(List)로 실현됨
   * `[value1,value2,....]`

  ```json
//배열 이름 "hobby" : 2개의 문자열 요소를 가지는 JSON 배열
{
    "firstName": "Kwon",
    "lastName": "YoungJae",
    "email": "kyoje11@gmail.com",
    "hobby": ["puzzles","swimming"]
}
//배열 이름 "dog" : 3개의 JSON 객체를 요소로 가지는 JSON 배열
"dog": [
    {"name": "식빵", "family": "웰시코기", "age": 1, "weight": 2.14},
    {"name": "콩콩", "family": "포메라니안", "age": 3, "weight": 2.5},
    {"name": "젤리", "family": "푸들", "age": 7, "weight": 3.1}
]
  ```

<br/>

## 6. XML vs JSON

* 데이터를 나타낼 수 있는 방식은 여러가지가 있지만, 대표적인 것이 XML이고, 이후 가장 많이 사용되는 것이 아마도 JSON일 것이다.

* **XML**
  * 데이터 값 양쪽으로 태그가 있음

* **JSON**
  * 태그로 표현하기 보다는 중괄호({}) 같은 형식으로 하고, 값을 ','로 나열하기에 그 표현이 간단함

* **공통점**
  1. 데이터를 저장하고 전달하기 위해 고안됨
  2. 계층적인 데이터 구조를 가짐
  3. 프로그래밍 언어에 의해 파싱될 수 있음
  4. XMLHttpRequest 객체를 이용하여 서버로부터 데이터를 전송받아올 수 있음

* **차이점**
  1. JSON은 종료 태그를 사용하지 않음
  2. JSON의 구문이 XML의 구문보다 더 짧음
  3. JSON 데이터가 XML 데이터보다 더 빨리 읽고 쓸 수 있음
  4. XML은 배열을 사용할 수 없지만, JSON은 배열을 사용할 수 있음
  5. XML은 XML 파서로 파싱되며, JSON은 자바스크립트 표준 함수인 eval() 함수 등으로 파싱됨

<br/>

## 7. JSON의 문제점

* **AJAX를 사용해 데이터를 주고 받을 때 그 데이터 포맷으로 JSON을 사용한다.**

  * AJAX 는 단순히 데이터만이 아니라 JavaScript 그 자체도 전달할 수 있음
  * 즉, JSON데이터라고 해서 받았는데 단순 데이터가 아니라 JavaScript가 될 수도 있고, 그게 실행 될 수 있다는 것 **(데이터인 줄 알고 받았는데 악성 스크립트가 될 수 있음)**

  * 위와 같은 이유로, 받은 내용에서 순수하게 데이터만 추출하기 위한 JSON 관련 라이브러리를 따로 사용하기도 함

* XML 문서는 XML DOM을 이용하여 해당문서에 접근함

  - JSON은 문자열을 전송받은 후 해당 문자열을 바로 파싱하므로, 속도는 더 빠름
  - 하지만, JSON은 **전송받은 데이터 무결성을 사용자가 직접 검증** 해야 함
  - 따라서, 데이터의 검증이 필요한 곳에서는 아직 XML문서를 더 많이 사용함

* JSON으로 가져올 수 있는 데이터는 **해당 자바스크립트가 로드된 서버의 데이터에 한정됨**

  - JSON은 단순히 데이터 포맷일 뿐
  - 데이터를 불러오기 위해서는 XMLHttpRequest()라는 JavaScript 함수를 사용해야 함
    * 이 함수가 동일 서버에 대한 것만 지원하기 때문

<br/>

## 8. JSON 형식 텍스트 -> JavaScript Object로 변환

* ```json
  var jsonText = '{ "name": "Someone else", "lastName": "Kim" }';  // JSON 형식의 문자열
  var realObject = JSON.parse(jsonText);
  var jsonText2 = JSON.stringify(realObject);
  ```

  - **JSON.parse( JSON으로 변환할 문자열 )** : JSON 형식의 텍스트를 자바스크립트 객체로 변환함
  - **JSON.stringify( JSON 문자열로 변환할 값 )** : 자바스크립트 객체를 JSON 텍스트로 변환함

<br/>


## :page_with_curl: Reference

* [JSON이란 무엇인가?](https://velog.io/@surim014/JSON이란-무엇인가)
* [JSON이란 무엇일까??](https://nesoy.github.io/articles/2017-02/JSON)
* [JSON 기초](http://tcpschool.com/json/json_intro_basic)
* [JSON과 XML](http://tcpschool.com/json/json_intro_xml)
* [JSON 이란?](https://genesis8.tistory.com/195)

- [JSON 문법](https://tcpschool.com/json/json_basic_syntax)