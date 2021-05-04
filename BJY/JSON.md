## JSON(JavaScript Object Notation)

<br/>

### <u>정의</u>

*  JSON은 경량(Lightweight)의 DATA-교환 형식
*  Javascript에서 객체를 만들 때 사용하는 표현식을 의미한다.
*  JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작아서, 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 사용한다.

<br/>

### <u>형식</u>

> #### 기본 자료형
>
> * 수(Number)
> * 문자열(String)
> * 참/거짓(Boolean)
> * 배열(Array)
> * 객체(Object)
> * null

#### - name-value 형식의 쌍 (pair)

* 여러가지 언어들에서 object,hashtable,struct로 실현되었다.
* `{String key : String Value}`

~~~javascript
{
  "firstName": "Kwon",
  "lastName": "YoungJae",
  "email": "kyoje11@gmail.com"
}
~~~

#### - 값들의 순서화된 리스트 형식

* 여러가지 언어들에서 배열(Array), 리스트(List)로 실현되었다.
* `[value1,value2,....]`

~~~javascript
{
  "firstName": "Kwon",
  "lastName": "YoungJae",
  "email": "kyoje11@gmail.com",
  "hobby": ["puzzles","swimming"]
}
~~~

<br/>

### <u>특징</u>

1. 서버와 클라이언트 간의 교류에서 일반적으로 많이 사용된다.
2. 자바스크립트 객체 표기법과 아주 유사하다.
3. 자바스크립트를 이용하여 JSON 형식의 문서를 쉽게 자바스크립트 객체로 변환할 수 있는 이점이 있다.
4. **JSON 문서 형식은 자바스크립트 객체의 형식을 기반으로 만들어졌다.**
5. 자바스크립트의 문법과 굉장히 유사하지만 **텍스트 형식일 뿐**이다.
6. 다른 프로그래밍 언어를 이용해서도 쉽게 만들 수 있다.
7. 특정 언어에 종속되지 않으며, 대부분의 프로그래밍 언어에서 JSON 포맷의 데이터를 핸들링 할 수 있는 라이브러리를 제공한다.

<br/>

### <u>XML VS JSON</u>

* 데이터를 나타낼 수 있는 방식은 여러가지가 있지만, 대표적인 것이 XML이고, 이후 가장 많이 사용되는 것이 아마도 JSON일 것이다.

> **XML**
>
> 데이터 값 양쪽으로 태그가 있다.

> **JSON**
>
> 태그로 표현하기 보다는 중괄호({}) 같은 형식으로 하고, 값을 ','로 나열하기에 그 표현이 간단하다.

#### 공통점

1. 데이터를 저장하고 전달하기 위해 고안되었다.
2. 계층적인 데이터 구조를 가진다.
3. 프로그래밍 언어에 의해 파싱될 수 있다.
4. XMLHttpRequest 객체를 이용하여 서버로부터 데이터를 전송받아올 수 있다.

#### 차이점

1. JSON은 종료 태그를 사용하지 않는다.
2. JSON의 구문이 XML의 구문보다 더 짧다.
3. JSON 데이터가 XML 데이터보다 더 빨리 읽고 쓸 수 있다.
4. XML은 배열을 사용할 수 없지만, JSON은 배열을 사용할 수 있다.
5. XML은 XML 파서로 파싱되며, JSON은 자바스크립트 표준 함수인 eval() 함수로 파싱된다.

<br/>

### <u>JSON의 문제점</u>

> **AJAX를 사용해 데이터를 주고 받을 때 그 데이터 포맷으로 JSON을 사용한다.**

AJAX 는 단순히 데이터만이 아니라 JavaScript 그 자체도 전달할 수 있다. 이 말은 JSON데이터라고 해서 받았는데 단순 데이터가 아니라 JavaScript가 될 수도 있고, 그게 실행 될 수 있다는 것이다. (데이터인 줄 알고 받았는데 악성 스크립트가 될 수 있다.)

위와 같은 이유로 받은 내용에서 순수하게 데이터만 추출하기 위한 JSON 관련 라이브러리를 따로 사용하기도 한다.

<br/>

<br/>

<br/>

<br/>

### REFERENCE

* [JSON이란 무엇인가?](https://velog.io/@surim014/JSON%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
* [JSON이란 무엇일까??](https://nesoy.github.io/articles/2017-02/JSON)
* [JSON 기초](http://tcpschool.com/json/json_intro_basic)
* [JSON과 XML](http://tcpschool.com/json/json_intro_xml)
* [JSON 이란?](https://genesis8.tistory.com/195)