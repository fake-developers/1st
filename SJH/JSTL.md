# JSTL

- JSP 표준라이브러리(JSP Standard Tag Library)의 약어
- **자주 사용될 수 있는 커스텀 태그들을 모아서 표준으로 모아놓은 태그 라이브러리**

<BR>

## JSTL의 목적 

- 간단한 프로그램 로직의 구사(자바의 변수 선언, if문, for문 등에 해당하는 로직)
- 다른 JSP페이지 호출 (`<c:redirect>`,`<c:import'>`)
- 날짜, 시간, 숫자의 포맷
- JSP 페이지 하나를 가지고 여러가지 언어의 웹 페이지 생성
- 데이터베이스로의 입력,수정,삭제,조회
- XML 문서의 처리
- 문자열을 처리하는 함수 호출

<BR>

## JSTL의 장점

- 빠른 개발 -> JSP를 단순화하는 많은 태그를 제공
- 코드 재사용성 -> 다양한 페이지에서 JSTL 태그 사용 가능
- 스크립틀릿 태그를 사용할 필요가 없음 (스크립틀릿 태그를 사용하지 않음)

<BR>

## JSTL의 종류

| **라이브러리명** | 접두어 | **주요 기능**                       | **URI**                               |
| ---------------- | ------ | ----------------------------------- | ------------------------------------- |
| 코어             | c      | 변수 지원, 제어문, 페이지 관련 처리 | http://java.sun.com/jsp/jstl/core     |
| 함수             | fn     | collection 처리, String 처리        | http://java.sun.com/jsp/jstl/fuctions |
| 포매팅           | fmt    | 포맷 처리, 국제화 지원              | http://java.sun.com/jsp/jstl/fmt      |
| 데이터베이스     | sql    | DB관련 CRUD 처리                    | http://java.sun.com/jsp/jstl/sql      |
| XML              | x      | XML관련 처리                        | http://java.sun.com/jsp/jstl/xml      |

<BR>

## JSTL 사용법

- JSP 페이지 에서 taglib 지시자를 이용해 JSTL 라이브러리의 URL 식별자와 접두어를 연결
-  `<%@ taglib prefix="접두어" uri="URI 경로" %>` 

<BR>

## JSTL 태그 사용법

- #### Core Tags

  - `<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %> `

  | **기능**  | **태그 - 부모태그(자식태그)**                   |
  | --------- | ----------------------------------------------- |
  | 변수      | remove, set                                     |
  | 흐름 제어 | choose(when, otherwise), forEach, forTokens, if |
  | URL 관리  | import(param), redirect(param) ,url(param)      |
  | 기타      | catch, out                                      |

  **\<c:out>**

  - 출력문을 만드는 태그

  - JSP expression tag와 비슷하지만 expression에서만 사용가능
  - <%= ...%>와 유사한 표현식

  ~~~java
  <c:out value="출력값" default="기본값" />
  <c:out value="출력값">기본값</c:out>
  
  <c:out value="hello">
  ~~~

  - value 값이 null이면 기본값이 출력되고 기본값이 없으면 빈 문자열 출력
  - value에 EL 표현식 사용가능
  - escapeXml 항목 사용하여 태그를 포함해서 출력할지 적용해서 출력할지 결정가능
    - `<c:out value="${aaa}" escapeXml="true"></c:out>`

  **\<c:set>**

  - 변수를 다룰 때 사용
  - 이 태그로 생성한 변수는 JSP 의 로컬 변수가 아니라 서블릿 보관소(JspContext, ServletRequest, HttpSession, ServletContext)에 저장

  ~~~java
  <c:set var="변수명" value="값" scope="page(기본값)|request|session|application" />
  <c:set var="변수명" scope="page(기본값)|request|session|application">값</c:set>
     
  <c:set var="Income" scope="session" value="${4000*4}"/>  
  <c:out value="${Income}"/> 
  ~~~

  - ${변수명}으로 사용 가능
  - 변수는 내부적으로 자바 변수로 선언되는게 아니라 page 데이터 영역의 애트리뷰트로 선언되므로 <%=변수이름%> 형태로 출력 불가

  **\<c:remove>**

  - 보관소에 저장된 값을 제거

  ~~~java
  <c:remove var="변수명" scope="page(기본값) | request | session | application" />
  ~~~

  - 첫 번째 범위 또는 지정된 범위에서 변수 제거
  - \<c:set>와 마찬가지로 scope 속성으로 보관소를 명시 가능, 보관소의 기본값은 page

  **\<c:if>**

  - 조건을 테스트 하는데 사용
  - else if, else문 없음

  ~~~java
  <c:if test="조건식" var="변수명" scope="page(기본값) | request | session | application">내용</c:if>
      
  <c:set var="income" scope="session" value="${4000*4}"/>  
  <c:if test="${income > 8000}">  
     <p>My income is: <c:out value="${income}"/><p>  
  </c:if>
  ~~~

  - test의 조건식이 true일 경우 본문 내용을 표시
  - var, scope 속성은 test 결과를 저장하는데 사용

  **\<c:choose>, \<c:when>, \<c:otherwise>**

  - if-else문 처럼 사용 가능
  - when 태그는 한 개 이상 존재해야하며, \<c:otherwise> 태그는 0개 혹은 1개가 올 수 있다.

  ~~~java
  <c:choose>
      <c:when test="조건식"></c:when>
      <c:when test="조건식"></c:when>
      ...
      <c:otherwise></c:when>
  </c:choose>
      
  <c:choose>  
      <c:when test="${income <= 1000}">  
         Income is not good.  
      </c:when>  
      <c:when test="${income > 10000}">  
          Income is very good.  
      </c:when>  
      <c:otherwise>  
         Income is undetermined...  
      </c:otherwise>  
  </c:choose>
  ~~~

  - choose 태그 : java switch문 처럼 사용
  - when 태그 : 조건이 true 인 경우 본문을 포함하는 choose의 하위 태그
  - otherwise : 모든 이전 조건이 false인 경우에만 실행하는 choose의 하위 태그

  **\<c:forEach>**

  - 중첩된 본문 내용을 고정된 횟수만큼 또는 컬렉션에 반복하는데 사용되는 반복 태그

  | 속성      | 설명                              | 비고     |
  | --------- | --------------------------------- | -------- |
  | var       | 사용할 변수명                     | Required |
  | items     | Collection 객체(List, ArrayList)  | Required |
  | begin     | 시작 index(default = 0)           |          |
  | end       | 종료 index(default = items크기-1) |          |
  | step      | 증감 수                           |          |
  | varStatus | 반복상태를 알 수 있는 변수        |          |

  ~~~java
  <c:forEach var="변수명" items="목록 데이터" begin="시작 인덱스" end="종료 인덱스">콘텐츠</c:forEach>
      
  <c:forEach var="item" items="${list}" begin=0 end=5 step=1 varStatus="status"> 번호 : ${status.count} 이름 : ${item.name} 나이 : ${item.age} 주소 : ${item.addr} </c:forEach>
  ~~~

  **\<c:forTokens>**

  - 제공된 구분 기호로 구분된 토큰을 반복
  - 문자열을 토큰으로 나누고 각 토큰을 반복하여 출력을 생성하는데 사용
  - c:forEach 태그와 유사한 속성을 가짐
  - 구분자는 여러개를 넣으면 여러개 가능

  ~~~java
  <c:forTokens var="변수명" items="문자열" delims="구분자">콘텐츠</c:forTokens>
      
  <c:forTokens items="Rahul-Nakul-Rajesh" delims="-" var="name">  
     <c:out value="${name}"/><p>  
  </c:forTokens>
  //결과
  Rahul
  Nakul
  Rajesh
      
  <c:forTokens var="temp" items="ㅋㅋㅋ^ㅎㅎㅎ@ㅉㅉㅉ!ㅍㅍㅍ" delims="^@!">
  	${temp}<br>
  </c:forTokens>
  //결과
  ㅋㅋㅋ
  ㅎㅎㅎ
  ㅉㅉㅉ
  ㅍㅍㅍ
  ~~~

  **\<c:url>**

  - 선택적 쿼리 매개 변수를 사용하여 URL을 만들때 사용
  - response.encodeURL() 메서드에 대한 호출을 작성하는 대체 방법으로 사용

  ~~~java
  <c:url var="변수명" value="url">
      <c:param name="파라미터명" value="값" />
      <c:param name="파라미터명" value="값" />
      <c:param name="파라미터명" value="값" />
  </c:url>
  
  <c:url var="calcUrl" value="http://localhost:8080/calc">
      <c:param name="v1" value="10" />
      <c:param name="v2" value="20" />
      <c:param name="op" value="+" />
  </c:url>
  ${calcUrl}
  //결과
  localhost:8080/calc?v1=10&v2=20&op=%2B
  
  <c:url value="/RegisterDao.jsp"/>  
  ~~~

  **\<c:redirect>**

  - 브라우저르 새 URL로 리다이렉션
  - 문맥 기준 URL과 c:param 태그를 지원
  - 내부적으로 HttpServletResponse의 sendRedirect()를 호출
  - 자동 URL 재 작성을 사용하여 브라우저를 대체 URL로 리다이렉션하는데 사용

  ~~~java
  <c:redirect url="url"/>
  
  <c:redirect url="https://velog.io/@ye050425"/>  
  ~~~

  **\<c:catch>**

  - 본문에서 발생하는 Throwable 예외를 포착하고 선택적으로 노출시키는데 사용
  - 일반적으로 오류 처리에 사용되며 프로그램에서 발생하는 문제를 보다 쉽게 처리

  ~~~java
  <c:catch var ="catchtheException">  
     <% int x = 2/0;%>  
  </c:catch>  
    
  <c:if test = "${catchtheException != null}">  
     <p>The type of exception is : ${catchtheException} <br />  
     There is an exception: ${catchtheException.message}</p>  
  </c:if>  
      
  //결과//
  The type of exception is : java.lang.ArithmeticException: /by zero
  There is an exception: /by zero
  ~~~

  **\<c:import>** 

  - jsp의 include와 유사
  - 서버 내부 또는서버 외부의 모든 자원 컨텐츠를 포함하는 추가 기능이 존재
  -  url 속성에 콘텐츠가 있는 주소를 지정하면 해당 주소로 요청하고 응답 결과를 받아서 반환

  ~~~java
  <c:import url="url" var="변수명" scope="page(기본값) | request | session | application" />
      
  <c:import url="https://www.nlotto.co.kr/common.do?method=getLottoNumber&drwNo=800" />
  //로또 800회차 당첨결과를 JSON으로 반환받은 결과 출력
  ~~~

- #### functions tags

  - `<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %>  `
  - 많은 표준 함수를 제공, 대부분은 일반적인 문자열 조작 함수
  - JSTL 함수 라이브러리를 포함시키는데 사용되는 구문

  | JSTL Functions          | Description                                                  |
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

  더 자세한 내용은 [여기](https://velog.io/@ye050425/JSP-JSTL-%EC%A0%95%EB%A6%AC#xml-tags) 를 참조

- #### Formatting tags

  - `<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>  `
  - 서식 태그는 메시지 형식, 번호 및 날짜 형식 등을 지원
  - 국제화 된 웹 사이트에서 텍스트, 시간, 날짜 및 숫자를 표시하고 형식화하는데 사용
  - 라이브러리를 포함하는데 사용되는 구문

  | Formatting Tags  | Descriptions                                                 |
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

  더 자세한 내용은 [여기](https://velog.io/@ye050425/JSP-JSTL-%EC%A0%95%EB%A6%AC#xml-tags) 를 참조

- #### XML tags

  - `<%@ taglib uri="http://java.sun.com/jsp/jstl/xml" prefix="x" %>  `
  - JSP 중심의 XML 문서 조작 및 작성 방법을 제공하는데 사용
  - XML 데이터와 상호 작용하는데 사용되는 사용자 정의 태그 제공
  - 흐름 제어, 변환 등을 제공
  - 라이브러리를 포함하는데 사용되는 구문

  | Descriptions                                                 | XML Tags    |
  | ------------------------------------------------------------ | ----------- |
  | <%= ...> 태그와 유사하지만 XPath 표현식                      | x:out       |
  | 태그 본문 또는 속성에 지정된 XML 데이터를 구문 분석하는 데 사용 | x:parse     |
  | 변수를 XPath 표현식의 값으로 설정하는 데 사용                | x:set       |
  | 상호 배타적 인 조건부 작업에 대한 context를 설정하는 조건부 태그 | x:choose    |
  | 가 된 조건이 'true'인 경우 본문이 포함됨                     | x:when      |
  | 태그 및 이전의 모든 조건이 '거짓'인 경우에만 실행            | x:otherwise |
  | 테스트 XPath 표현식을 평가하는 데 사용되며, true 인 경우 본문 내용을 처리 | x:if        |
  | XSL (Extensible Stylesheet Language) 변환을 제공하기 위해 XML 문서에서 사용 | x:transform |
  | XSLT 스타일 시트에서 매개 변수를 설정하기 위해 변환 태그와 함께 사용 | x:param     |

  - 실행을 위해서 \lib: 안에 아래 두 파일이 있어야 함
    - Xalan.jar: Download this jar file from the link:
      http://xml.apache.org/xalan-j/index.html
    - XercesImpl.jar: Download this jar file from the link:
      http://www.apache.org/dist/xerces/j/

  더 자세한 내용은 [여기](https://velog.io/@ye050425/JSP-JSTL-%EC%A0%95%EB%A6%AC#xml-tags) 를 참조

- #### SQL tags

  - `<%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%>  `
  - SQL 지원 제공
  - 사용하면 Microsoft SQL Server, mySQL, Oracle 과 상호작용 가능

  | SQL Tags          | Descriptions                                                 |
  | ----------------- | ------------------------------------------------------------ |
  | sql:setDataSource | 프로토 타이핑에만 적합한 간단한 데이터 소스를 만드는 데 사용 |
  | sql:query         | sql 속성 또는 본문에 정의 된 SQL 쿼리를 실행하는 데 사용     |
  | sql:update        | sql 속성 또는 태그 본문에 정의 된 SQL 업데이트를 실행하는 데 사용 |
  | sql:param         | SQL 문의 매개 변수를 지정된 값으로 설정하는 데 사용          |
  | sql:dateParam     | SQL 문의 매개 변수를 지정된 java.util.Date 값으로 설정하는 데 사용 |
  | sql:transaction   | 중첩 된 데이터베이스 조치에 공통 연결을 제공하는 데 사용     |

  더 자세한 내용은 [여기](https://velog.io/@ye050425/JSP-JSTL-%EC%A0%95%EB%A6%AC#xml-tags) 를 참조

<br>

------

**<참조>**

- [JSTL:::: 개념, 설치법, 코어 라이브러리 포매팅 라이브러리 함수 라이브러리 사용법](https://seven00.tistory.com/entry/JSTL%EA%B0%9C%EB%85%90%EC%84%A4%EC%B9%98%EB%B2%95%EC%BD%94%EC%96%B4-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%8F%AC%EB%A7%A4%ED%8C%85-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%95%A8%EC%88%98-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EC%82%AC%EC%9A%A9%EB%B2%95)

- [[JSP] JSTL 정리](https://velog.io/@ye050425/JSP-JSTL-%EC%A0%95%EB%A6%AC#xml-tags)

- [JSTL (종류, 사용법, core, fuctions)](https://sjh836.tistory.com/136)
- [JSP 정리 - JSTL(Jsp Standard Tag Library)](https://programmingsummaries.tistory.com/84)
- [[JSP] JSTL 사용 방법 - 주요 태그 문법 정리](https://atoz-develop.tistory.com/entry/JSP-JSTL-%EC%82%AC%EC%9A%A9-%EB%B0%A9%EB%B2%95-%EC%A3%BC%EC%9A%94-%ED%83%9C%EA%B7%B8-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%A6%AC)

