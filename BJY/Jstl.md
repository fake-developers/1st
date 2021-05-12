## JSTL

<br/>

### <u>JSTL이란?</u>

JSTL은 JSP 표준라이브러리(JSP Standard Tag Library)의 약어이다. 자주 사용될 수 있는 커스텀 태그들을 모아서 표준으로 모아놓은 태그 라이브러리다.

**목적**

* 간단한 프로그램 로직의 구사(자바의 변수 선언, if문, for문 등에 해당하는 로직)
* 다른 JSP페이지 호출 (`<c:redirect>`,`<c:import'>`)
* 날짜, 시간, 숫자의 포맷
* JSP 페이지 하나를 가지고 여러가지 언어의 웹 페이지 생성
* 데이터베이스로의 입력,수정,삭제,조회
* XML 문서의 처리
* 문자열을 처리하는 함수 호출

#### 종류

| **라이브러리명** | 접두어 |            **주요 기능**            |                **URI**                |
| :--------------: | :----: | :---------------------------------: | :-----------------------------------: |
|       코어       |   c    | 변수 지원, 제어문, 페이지 관련 처리 |   http://java.sun.com/jsp/jstl/core   |
|       함수       |   fn   |    collection 처리, String 처리     | http://java.sun.com/jsp/jstl/fuctions |
|      포매팅      |  fmt   |       포맷 처리, 국제화 지원        |   http://java.sun.com/jsp/jstl/fmt    |
|   데이터베이스   |  sql   |          DB관련 CRUD 처리           |   http://java.sun.com/jsp/jstl/sql    |
|       XML        |   x    |            XML관련 처리             |   http://java.sun.com/jsp/jstl/xml    |

<br/>

#### 사용법

`<%@ taglib prefix="접두어" uri="URI 경로" %>` 

<br>

### <u>core의 주요 기능</u>

* `<c:set>` : 변수 선언, 할당

  ~~~jsp
  <c:set var="변수이름" value="값" />
  ~~~

  * 선언 이후에 `${변수이름}`로 사용하면 된다.
    * 내부적으로 자바 변수로 선언되는게 아니라 page 데이터 영역의 애트리뷰트로 선언되기 때문에 `<%=변수이름%>`형태로 출력될 수 없다.
  * 다른 영역에 저장하고 싶다면 scope="session"을 추가
  * scope 속성 : 범위 4가지(page, request, session, application), default 는 page
  * ex. int count = 10; = `<c:set var="count" value="10">`

* `<c:out>` : 출력
  * ex. System.out.println("hello");을 간단하게 `<c:out value="hello">`

* `<c:remove>` : 변수값 remove

  ~~~jsp
  <c:remove var="변수이름" />
  ~~~

  * scope 속성을 사용하면 특정 영역의 변수만 제거

* `<c:if>` : if문, else문 없음
  
  * var 속성 : 조건식의 값을 저장할 변수
  * scope 속성 : boolean 변수가 사용될 범위를 뜻함
  * ex. `<c:if test="조건식"> 참일때 실행할 문장 </c:if>`

  ~~~jsp
  <c:remove var="aaa"/>
  
  <c:if test="${empty aaa ? true : false}" var="result">
  	없다네ㅋㅋㅋ<br>
  </c:if>
  
  ${result}
  
  <!-- 실행결과 -->
  <!-- 없다네ㅋㅋㅋ
  	 true -->
  ~~~
  
  
  
* `<c:choose>, <c:when>, <c:otherwise>` : if-else 문 처럼 사용 가능
  
  * 일종의 스위치문이다.
  * when 이 true 이면 해당 블럭 실행
  * 모든 when 이 false 이면 otherwise 블럭 실행
  
  ```jsp
    <c:choose>
        <c:when test="${empty boardList}">
            등록된 글이 없습니다.
        </c:when>
        <c:when test="조건식">
            ...
        </c:when>
        <c:otherwise>
            ...
        </c:otherwise>
    </c:choose>
  ```
  
* `<c:forEach>` : for문이다

| 속성      | 설명                              | 비고     |
| --------- | --------------------------------- | -------- |
| var       | 사용할 변수명                     | Required |
| items     | Collection 객체(List, ArrayList)  | Required |
| begin     | 시작 index(default = 0)           |          |
| end       | 종료 index(default = items크기-1) |          |
| step      | 증감 수                           |          |
| varStatus | 반복상태를 알 수 있는 변수        |          |

```jsp
  <c:forEach var="item" items="${list}" begin=0 end=5 step=1 varStatus="status">
      번호 : ${status.count}
      이름 : ${item.name}
      나이 : ${item.age}
      주소 : ${item.addr}
  </c:forEach>
```

* `<c:forTokens>` : 문자열에 포함된 토큰을 분리해서 각각의 토큰에 대해 반복 처리를 수행하도록 만드는 기능이다.

  * items 속성에는 토큰을 포함하는 문자열을 지정하고 delims 속성에는 토큰을 구분자를 기술한다.
  * 속성은 forEach 문의 속성에서 delims 속성이 추가된다.

  ~~~jsp
  <c:forTokens var="temp" items="ㅋㅋㅋ^ㅎㅎㅎ@ㅉㅉㅉ!ㅍㅍㅍ^ㄷㄷㄷ" delims="^@!">
  	\${temp}<br>
  </c:forTokens>
  
  <!-- 결과는 ㅋㅋㅋ,ㅎㅎ,ㅉㅉㅉ 등이 따로 분리되어 출력된다.-->
  ~~~

* `<c:import>` : 해당 페이지에 다른 페이지를 넣는 기능

  * jsp:include 와 차이는 jsp:include 는 코드가 작성된 부분에 출력되지만
    c:import 는 페이지의 내용을 변수에 저장할 수 있다.

  ~~~jsp
  여기는 기본 페이지 입니다 
  <c:import url="https://search.naver.com/search.naver" var="result"> 		<c:param name="query" value="아이유"/> 
  </c:import> 
  여기는 기본 페이지 입니다 
  ${result }
  ~~~

  <img src="https://user-images.githubusercontent.com/61674527/117991049-ab850100-b378-11eb-9ded-963393011c90.JPG" alt="import결과" style="zoom: 67%;" />

<br/>

### <u>formatting의 주요 기능</u>

* `<fmt:formatDate value="<%=new Date() %>" type="both"/>` : 날짜와 관련된 태그

  * 위와 같이 할 경우, 날짜와 시간이 모두 출력되게 된다.
  * type에 date, time 둘 중 하나를 쓰면 하나만 나오게 된다.

  

* `<fmt:formatNumber>` : 숫자와 관련된 태그

  ~~~jsp
  <fmt:formatNumber value="12345678" groupingUsed="true"/><br>
  <fmt:formatNumber value="3.141592" pattern="#.##"/>
  ~~~

  * 위의 경우 세자리마다 끊어서 쉼표가 출력되고, 아래의 경우 소수점 둘째자리 까지만 출력된다.

<br>

> http://www.w3big.com/ko/jsp/jsp-jstl.html 에서 더 많은 태그들을 볼 수 있다.

<br/>

<br/>

<br/>

### REFERENCE

* [JSP 정리 - JSTL (Jsp Standard Tag Library)](https://programmingsummaries.tistory.com/84)
* [JSTL(종류, 사용법, core, functions)](https://sjh836.tistory.com/136)
* [JSTL core tag 사용하기](https://sinna94.tistory.com/entry/JSTL-core-tag-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
* [JSTL::::개념,설치법,코어 라이브러리 포매팅 라이브러리 함수 라이브러리 사용법](https://seven00.tistory.com/entry/JSTL%EA%B0%9C%EB%85%90%EC%84%A4%EC%B9%98%EB%B2%95%EC%BD%94%EC%96%B4-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%8F%AC%EB%A7%A4%ED%8C%85-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%95%A8%EC%88%98-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EC%82%AC%EC%9A%A9%EB%B2%95)
* [JSP 표준 태그 라이브러리 (JSTL)](http://www.w3big.com/ko/jsp/jsp-jstl.html)

