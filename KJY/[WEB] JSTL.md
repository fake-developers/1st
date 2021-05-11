# [WEB] JSTL

:writing_hand: *Assembled by JiYoung-Kwon (2021-05-11)* 



## 1. JSTL이란?

* JSP 표준 라이브러리( **JSP Standard Tag Library** )의 약어
* 자주 사용될 수 있는 커스텀 태그들을 모아서 표준으로 모아놓은 태그 라이브러리
  * 반복과 조건, 데이터 관리 포맷, XML 조작, 데이터베이스 액세스 등
  * EL(Expression Language)를 사용하여 표현함
* http://tomcat.apache.org/taglibs/

#### 1-1. 종류

|  라이브러리명   | 접두어(prefix) |              주요 기능              |                  URI                  |
| :-------------: | :------------: | :---------------------------------: | :-----------------------------------: |
|    core tags    |       c        | 변수 지원, 제어문, 페이지 관련 처리 |   http://java.sun.com/jsp/jstl/core   |
|  function tags  |       fn       |    collection 처리, String 처리     | http://java.sun.com/jsp/jstl/fuctions |
| formatting tags |      fmt       |       포맷 처리, 국제화 지원        |   http://java.sun.com/jsp/jstl/fmt    |
|    SQL tags     |      sql       |          DB관련 CRUD 처리           |   http://java.sun.com/jsp/jstl/sql    |
|    XML tags     |       x        |            XML 관련 처리            |   http://java.sun.com/jsp/jstl/xml    |

#### 1-2. 사용법

* 위의 표를 참고하여 JSP 상단에 `<%@ taglib prefix="접두어" uri="URI 경로" %>`를 작성
* prefix는 임의로 지정할 수 있으나, JSTL에서 제안하는 표준 접두어를 사용하는 것을 권장

#### 1-3. 장점

1. 빠른 개발 : JSP를 단순화하는 많은 태그를 제공
2. 코드 재사용성 : 다양한 페이지에서 JSTL 태그 사용 가능
3. 스크립트릿 태그를 사용할 필요가 없음(사용하지 않음)

<br/>

## 2. Core Tags

* `<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>  `

* JSTL 태그 라이브러리 중에 가장 많이 사용하는 태그

* | 기능      | 태그 - 부모태그(자식태그)                       |
  | --------- | ----------------------------------------------- |
  | 변수      | remove, set                                     |
  | 흐름 제어 | choose(when, otherwise), forEach, forTokens, if |
  | URL 관리  | import(param), redirect(param), url(param)      |
  | 기타      | catch, out                                      |

#### \<c:out>

* JSP expression tag와 비슷하지만 expression에서만 사용할 수 있음

* `<% = ... %>`과 유사한 표현식 태그

* ```jsp
  <c:out value="출력값" default="기본값" />
  <c:out value="출력값">기본값</c:out>
  ```

* value 값이 null이면 기본값이 출력되고 기본값이 없으면 빈 문자열이 출력됨

* value에 EL 표현식을 쓸 수 있음

  * 예시) `<c:out value="${'Welcome to JSTL'}"/> `

#### \<c:set>

* 변수를 선언하는 태그

* 'scope'에서 평가된 표현식의 결과를 설정하는 데 사용

* 표현식을 평가하고 결과를 사용하여 java.util.Map 또는 JavaBean 값을 설정하므로 유용함

* jsp:setProperty action 태그와 유사함

* ```jsp
  <c:set var="변수이름" value="값" />
  
  <!-- 예시 -->
  <!-- [scope = "session"] : session 영역에 저장 -->
  <c:set var="Income" scope="session" value="${4000*4}"/>  
  <c:out value="${Income}"/>  
  
  <!-- 결과 -->
  16000
  ```

* 내부적으로 자바 변수로 선언되는게 아니라, page 데이터 영역의 애트리뷰트로 선언됨

  * 따라서,  `<%=변수이름%>` 형태로 출력될 수 없음

#### \<c:remove>

* 변수를 제거할 때 사용

* 첫 번째 범위 또는 지정된 범위에서 변수를 제거

* ```jsp
  <!-- 모든 scope에서 해당 이름을 가진 변수 다 제거 -->
  <c:remove var="변수이름" />
  
  <!-- 특정 영역의 변수 제거 예시 -->
  <c:remove var="변수이름" scope="request" />
  ```

#### \<c:choose>, \<c:when>, \<c:otherwise>

* choose

  * 일종의 switch문처럼 작동
  * 상호 배타적인 조건부 작업에 대한 컨텍스트를 설정하는 조건부 태그

* when

  * 조건이 'true' 인 경우, 본문을 포함하는 choose의 하위 태그

* otherwise

  * choose의 하위 태그
  * when 태그를 따르며, 평가된 모든 이전 조건이 'false'일 경우에만 실행

* ```jsp
  <c:choose>
  	<c:when test="${1 > 0}">
  		1은 0보다 큽니다.<br>
  	</c:when>
  	<c:when test="${2 > 0}">
  		2도 0보다 큽니다.<br>
  	</c:when>
  	<c:otherwise>
  		왠만한 숫자는 0보다 크지요<br>
  	</c:otherwise>
  </c:choose>
  ```

#### \<c:forEach>

* 중첩된 본문 내용을 고정 된 횟수만큼 또는 컬렉션에 반복하는데 사용되는 반복 태그

* for문과 비슷함

* 자바 스크립트를 포함하는 동안, 스크립트릿을 통해 또는 루프 용으로 사용하기에 좋은 대안으로 사용

* 객체 컬렉션을 반복하므로 가장 일반적으로 사용

* ```jsp
  <!-- 1,3,5,7 ... -->
  <c:forEach var="임시변수명" begin="1" end="10" step="2">
  	${임시변수명}<br>
  </c:forEach>
  
  <!-- 배열의 내용을 순서대로 출력. 향상된 for문과 비슷 -->
  <c:forEach var="배열 요소를 저장할 임시변수 이름" items="${배열이름}">
  	${배열 요소를 저장할 임시변수 이름}<br>
  </c:forEach>
  ```

#### \<c:forTokens>

* 문자열에 포함된 토큰을 분리해서, 각각의 토큰에 대해 반복 처리를 수행하도록 만드는 기능

* ```jsp
  <c:forTokens var="temp" items="ㅋㅋㅋ ㅎㅎㅎ ㅉㅉㅉ" delims=" ">
  	${temp}<br>
  </c:forTokens>
  
  <!-- 결과 -->
  ㅋㅋㅋ
  ㅎㅎㅎ
  ㅉㅉㅉ
  
  <!-- delims에 여러 개를 넣으면 여러 토큰 가능 -->
  <c:forTokens var="temp" items="ㅋㅋㅋ^ㅎㅎㅎ@ㅉㅉㅉ!ㅍㅍㅍ^ㄷㄷㄷ" delims="^@!">
  	${temp}<br>
  </c:forTokens>
  ```

#### \<c:if>

* 조건을 테스트하는 데 사용

* 평가된 표현식이 true인 경우 본문 내용을 표시함

* ```jsp
  <c:set var="income" scope="session" value="${4000*4}"/>  
  <c:if test="${income > 8000}">  
     <p>My income is: <c:out value="${income}"/><p>  
  </c:if>
  ```

#### \<c:import>

* jsp 'include'와 유사

* url 속성에 콘텐츠가 있는 주소를 지정하면, 해당 주소로 요청하고 응답 결과를 받아서 반환함

* ```jsp
  <c:import url="url" var="변수명" scope="page(기본값) | request | session | application" />
  
  <!-- url에 로또 800회차 당첨 결과를 JSON으로 반환받을 결과를 출력하는 예제 -->
  <c:import var="lottoResult" url="https://www.nlotto.co.kr/common.do?method=getLottoNumber&drwNo=800" />
  <textarea rows="10" cols="80">
      ${lottoResult}
  </textarea>
  ```

#### \<c:redirect>

* 리다이렉트 처리 시 사용
* 내부적으로 HttpServletResponse의 sendRedirect()를 호출함
* `<c:redirect url="url" />`

#### \<c:url>

* URL을 만들 때 사용

* 이 태그를 사용하면, 매개변수를 포함한 URL을 쉽게 만들 수 있음

* ```jsp
  <c:url var="변수명" value="url">
      <c:param name="파라미터명" value="값" />
      <c:param name="파라미터명" value="값" />
      <c:param name="파라미터명" value="값" />
  </c:url>
  ```

#### \<c:param>

* 포함하는 'import'태그의 URL에 매개 변수를 추가

* URL 내에 적절한 URL 요청 매개 변수 지정 가능

* 필요한 URL 인코딩을 자동으로 수행

* value 속성은 매개 변수 값을 나타내고 name 속성은 매개 변수 이름을 나타냄\

* ```jsp
  <c:url value="/index1.jsp" var="completeURL"/>  
   <c:param name="trackingId" value="786"/>  
   <c:param name="user" value="Nakul"/>  
  </c:url>  
  ${completeURL}
  
  <!-- 결과 -->
  /~~~/index1.jsp?trackingId=786&user=Nakul
  ```

#### \<c:catch>

* 본문에서 발생하는 Throwable 예외를 포착하고 선택적으로 노출시키는 데 사용

* 일반적으로 오류 처리에 사용되며, 프로그램에서 발생하는 문제를 보다 쉽게 처리

* ```jsp
  <c:catch var ="catchtheException">  
     <% int x = 2/0;%>  
  </c:catch>  
    
  <c:if test = "${catchtheException != null}">  
     <p>The type of exception is : ${catchtheException} <br />  
     There is an exception: ${catchtheException.message}</p>  
  </c:if>  
  
  <!-- 결과 -->
  The type of exception is : java.lang.ArithmeticException: / by zero
  There is an exception : / by zero
  ```

<br/>

## 3. function Tags

- 많은 표준 함수를 제공, 대부분은 일반적인 문자열 조작 함수

- `<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %>`

- | JSTL Functions          | Description                                                  |
  | ----------------------- | ------------------------------------------------------------ |
  | fn:contains()           | 프로그램에서 지정된 하위 문자열을 포함하는 입력 문자열인지 테스트하는 데 사용 |
  | fn:containsIgnoreCase() | 입력 문자열에 대소 문자를 구분하지 않고 지정된 하위 문자열이 포함되어 있는지 테스트하는 데 사용 |
  | fn:endsWith()           | 입력 문자열이 지정된 접미어로 끝나는 지 테스트하는 데 사용   |
  | fn:escapeXml()          | XML 마크업으로 해석되는 문자를 escape                        |
  | fn:indexOf()            | 지정된 하위 문자열이 처음 나타나는 문자열 내에서 인덱스를 반환 |
  | fn:trim()               | 문자열의 양쪽 끝에서 공백을 제거                             |
  | fn:startsWith()         | 주어진 문자열이 특정 문자열 값으로 시작되는지 여부를 확인하는 데 사용. |
  | fn:split()              | 문자열을 하위 문자열 배열로 분할                             |
  | fn:toLowerCase()        | 문자열의 모든 문자를 소문자로 변환                           |
  | fn:toUpperCase()        | 문자열의 모든 문자를 대문자로 변환                           |
  | fn:substring()          | 주어진 시작 및 끝 위치에 따라 문자열의 하위 집합을 반환      |
  | fn:substringAfter()     | 특정 하위 문자열 다음에 문자열의 하위 집합을 반환            |
  | fn:substringBefore()    | 특정 하위 문자열 앞의 문자열 하위 집합을 반환                |
  | fn:length()             | 문자열 내부의 문자 수 또는 컬렉션의 항목 수를 반환           |
  | fn:replace()            | 모든 문자열을 다른 문자열 시퀀스로 바꿈                      |

- ```jsp
  <!-- 예시 -->
  <a class="<c:if test="${fn:startsWith(servletPath, '/board')}">active</c:if>" href="/board">
      
  <c:set var="String" value="Welcome to JSP programming"/>  
  <c:if test="${fn:endsWith(String, 'programming')}">  
     <p>String ends with programming<p>  
  </c:if> 
  ```

  

여러 function tags 예시는 [이 곳을 참고](https://velog.io/@ye050425/JSP-JSTL-%EC%A0%95%EB%A6%AC#cforeach-tag)

<br/>

## 4. Formatting tags

* 서식 태그는 메시지 형식, 번호 및 날짜 형식 등을 지원
* 국제화 된 웹 사이트에서 텍스트, 시간, 날짜 및 숫자를 표시하고 형식화하는 데 사용
* `<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %> `

* | Formatting Tags  | Descriptions                                                 |
  | ---------------- | ------------------------------------------------------------ |
  | fmt:parseNumber  | 통화, 백분율 또는 숫자의 문자열 표현을 구문 분석하는 데 사용 |
  | fmt:timeZone     | 본문 또는 시간대에 중첩 된 구문 분석 조치를 시간 형식화에 지정 |
  | fmt:formatNumber | 특정 형식 또는 정밀도로 숫자 값을 형식화하는 데 사용         |
  | fmt:parseDate    | 시간과 날짜의 문자열 표현을 구문 분석                        |
  | fmt:bundle       | 태그 본문에서 사용될 ResourceBundle 객체를 만드는 데 사용    |
  | fmt:setTimeZone  | 시간대 구성 변수 내에 시간대를 저장                          |
  | fmt:setBundle    | 자원 번들을로드하고이를 번들 구성 변수 또는 명명 된 범위 변수에 저장variable or the named scoped variable. |
  | fmt:message      | 국제화 된 메시지를 표시                                      |
  | fmt:formatDate   | 제공된 패턴 및 스타일을 사용하여 시간 및 / 또는 날짜를 형식화함 |

#### \<fmt:formatDate>

* 날짜 객체로부터 원하는 형식으로 날짜를 표현하고자 할때 사용

* ```jsp
  <fmt:formatDate value="<%=new Date() %>" type="both"/>
  ```

  * 위의 경우 :  날짜와 시간이 모두 출력됨
    * type에 date / time 중 하나만 쓰면 하나만 출력됨

#### \<fmt:parseDate>

* 날짜 형식으로 작성된 문자열로 java.util.Date 객체를 생성하고, 지정된 보관소에 저장

* ```jsp
  <fmt:parseDate var="변수명" value="날짜 형식 문자열" pattern="패턴" scope="page(기본값) | request | session | application" />
  
  <!-- 예제 -->
  <fmt:parseDate var="date1" value="2020-02-15" pattern="yyyy-MM-dd" />
  <fmt:formatDate value="${date1}" pattern="MM/dd/yy" />
  
  <!-- 결과 -->
  02/15/20
  ```

#### \<fmt:formatNumber>

* 숫자와 관련된 태그

* ```jsp
  <fmt:formatNumber value="12345678" groupingUsed="true"/><br>
  <fmt:formatNumber value="3.141592" pattern="#.##"/>
  ```

  * 위의 경우 : 세 자리마다 끊어서 쉼표가 출력됨
  * 아래의 경우 : 소수점 둘째자리까지만 출력됨



여러 Formatting tags 예시는 [이 곳을 참고](https://velog.io/@ye050425/JSP-JSTL-%EC%A0%95%EB%A6%AC#cforeach-tag)

<br/>

## 5. XML tags

* JSP 중심의 XML 문서 조작 및 작성 방법을 제공하는 데 사용

* XML 데이터와 상호 작용하는 데 사용되는 사용자 정의 태그 제공

* 흐름 제어, 변환 등을 제공

* `<%@ taglib uri="http://java.sun.com/jsp/jstl/xml" prefix="x" %>`

* 사용하기 위해서는 아래 두 파일이 \lib 안에 존재해야 함

  * Xalan.jar: Download this jar file from the link:
    http://xml.apache.org/xalan-j/index.html
  * XercesImpl.jar: Download this jar file from the link:
    http://www.apache.org/dist/xerces/j/

* | XML Tags    | Descriptions                                                 |
  | ----------- | ------------------------------------------------------------ |
  | x:out       | <%= ...> 태그와 유사하지만 XPath 표현식                      |
  | x:parse     | 태그 본문 또는 속성에 지정된 XML 데이터를 구문 분석하는 데 사용 |
  | x:set       | 변수를 XPath 표현식의 값으로 설정하는 데 사용                |
  | x:choose    | 상호 배타적 인 조건부 작업에 대한 context를 설정하는 조건부 태그 |
  | x:when      | 가 된 조건이 'true'인 경우 본문이 포함됨                     |
  | x:otherwise | 태그 및 이전의 모든 조건이 '거짓'인 경우에만 실행            |
  | x:if        | 테스트 XPath 표현식을 평가하는 데 사용되며, true 인 경우 본문 내용을 처리 |
  | x:transform | XSL (Extensible Stylesheet Language) 변환을 제공하기 위해 XML 문서에서 사용 |
  | x:param     | XSLT 스타일 시트에서 매개 변수를 설정하기 위해 변환 태그와 함께 사용 |

* ```jsp
  <h2>Vegetable Information:</h2>  
  <c:set var="vegetable">  
  <vegetables>  
      <vegetable>  
        <name>onion</name>  
        <price>40/kg</price>  
      </vegetable>  
   <vegetable>  
        <name>Potato</name>  
        <price>30/kg</price>  
      </vegetable>  
   <vegetable>  
        <name>Tomato</name>  
        <price>90/kg</price>  
      </vegetable>  
  </vegetables>  
  </c:set>  
  <x:parse xml="${vegetable}" var="output"/>  
  <b>Name of the vegetable is</b>:  
  <x:out select="$output/vegetables/vegetable[1]/name" /><br>  
  <b>Price of the Potato is</b>:  
  <x:out select="$output/vegetables/vegetable[2]/price" />  
  ```

<br/>

## 6. SQL tags

* SQL 지원을 제공

* 사용하면 Microsoft SQL Server, mySQL, Oracle 과 상호작용 가능

* `<%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql" %>  `

* | SQL Tags          | Descriptions                                                 |
  | ----------------- | ------------------------------------------------------------ |
  | sql:setDataSource | 프로토 타이핑에만 적합한 간단한 데이터 소스를 만드는 데 사용 |
  | sql:query         | sql 속성 또는 본문에 정의 된 SQL 쿼리를 실행하는 데 사용     |
  | sql:update        | sql 속성 또는 태그 본문에 정의 된 SQL 업데이트를 실행하는 데 사용 |
  | sql:param         | SQL 문의 매개 변수를 지정된 값으로 설정하는 데 사용          |
  | sql:dateParam     | SQL 문의 매개 변수를 지정된 java.util.Date 값으로 설정하는 데 사용 |
  | sql:transaction   | 중첩 된 데이터베이스 조치에 공통 연결을 제공하는 데 사용     |

<br/>

## :page_with_curl: Reference

* [JSTL (종류, 사용법, core, functions)](https://sjh836.tistory.com/136)
* [Jsp〃[EL]과 [JSTL] 한방에 정리 + Core](https://hunit.tistory.com/203)
* [JSP 정리 - JSTL (Jsp Standard Tag Library)](https://programmingsummaries.tistory.com/84)
* [[JSP] JSTL 사용 방법 - 주요 태그 문법 정리](https://atoz-develop.tistory.com/entry/JSP-JSTL-%EC%82%AC%EC%9A%A9-%EB%B0%A9%EB%B2%95-%EC%A3%BC%EC%9A%94-%ED%83%9C%EA%B7%B8-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%A6%AC)
* [JSTL의 이해 및 실습](http://wiki.gurubee.net/pages/viewpage.action?pageId=26740270)
* [JSTL 이란?](https://wiserloner.tistory.com/402)
* [[JSP] JSTL 정리](https://velog.io/@ye050425/JSP-JSTL-%EC%A0%95%EB%A6%AC#xml-tags)
