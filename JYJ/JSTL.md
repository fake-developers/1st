# JSTL

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYoung-Kwon, JiYe Bae*

<hr>



## JSLT

- <b>JSTL 이란?</b>
- JSP 표준 라이브러리 (JSP Standard Tag Library)의 약어이다.
  - 자주 사용될 수 있는 커스텀 태그들을 표준으로 모아놓은 태그 라이브러리이다.
  - 반복과 조건, 데이터 관리 포맷, XML 조작, 데이터베이스 액세스 등
    - EL (Expression Language)를 사용하여 표현한다.
- http://tomcat.apache.org/taglibs/

<br/>

<br/>

- <b>JSTL의 종류</b>

  |  라이브러리 명  | 접두어 (prefix) |              주요 기능              |                  URI                  |
  | :-------------: | :-------------: | :---------------------------------: | :-----------------------------------: |
  |    core tags    |        c        | 변수 지원, 제어문, 페이지 관련 처리 |   http://java.sun.com/jsp/jstl/core   |
  |  function tags  |       fn        |    collection 처리, String 처리     | http://java.sun.com/jsp/jstl/fuctions |
  | formatting tags |       fmt       |       포맷 처리, 국제화 지원        |   http://java.sun.com/jsp/jstl/fmt    |
  |    SQL tags     |       sql       |          DB관련 CRUD 처리           |   http://java.sun.com/jsp/jstl/sql    |
  |    XML tags     |        x        |            xml 관련 처리            |   http://java.sun.com/jsp/jstl/xml    |
  
  - 사용법
    - 위의 표를 참고하여 JSP 상단에 <code><%@taglib prefix="접두어" uri="URI 경로" %></code>를 작성한다.
    - prefix는 임의로 지정 가능하나, JSTL에서 제안하는 표준 접두어를 사용하는 것을 권장한다.

<br/>

<br/>

- <b>JSTL의 장점</b>
  - 빠른 개발
  - JSP를 단순화하는 많은 태그를 제공한다.
  - 코드 재사용성
    - 다양한 페이지에서 JSTL 태그를 사용할 수 있다.
  - 스크립트릿 태그를 사용할 필요가 없다. (사용하지 않는다.)
  

<br/>

<br/>

<br/>

#### Core Tags

- <b>core tags 사용</b>
  - <code><%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %></code>

<br/>

- <b>JSTL 태그 라이브러리 중 가장 많이 사용하는 태그</b>

  | 기능      | 태그 - 부모 태그 (자식 태그)                    |
  | --------- | ----------------------------------------------- |
  | 변수      | remove, set                                     |
  | 흐름 제어 | choose(when, otherwise), forEach, forTokens, if |
  | URL 관리  | import (param), redirect (param), url (param)   |
  | 기타      | catch, out                                      |

  <br/>

  - <b>\<c:out></b>

    - JSP expression tag와 비슷하지만, expression 에서만 사용할 수 있다.

    - <code><% = ... %></code>와 유사한 표현식 태그

      ```html
      <c:out value ="출력값" default="기본 값"/>
      <c:out value = "출력값">기본값</c:out>
      ```

    - value 값이 null이면 기본값이 출력되고, 기본값이 없으면 빈 문ㅇ자열이 출력된다.

    - value에 EL 표현식을 쓸 수 있다.

      - ex) <code><c:out value="${'Welcome to JSTL'}"/>

    <br/>

    <br/>

  - <b>\<c:set></b>

    - 변수를 선언하는 태그이다.
    - 'scope'에서 평가된 표현식의 결과를 설정하는 데 사용한다.
    - 표현식을 평가하고 결과를 사용하여 java.util.Map 또는 JavaBean 값을 설정하므로 유용하다.
    - jsp:setProperty action 태그와 유사하다.

    ``` html
    <c:set var="변수 이름" value="값"/>
    
    <!-- 예시 -->
    <!-- [socpe = "session"] : session 영역에 저장 -->
    
    <c:set var="Income" scope="session" value="${4000*4}"/>
    <c:out value="${Income}"/>
    
    <!-- 결과 -->
    16000
    ```

    - 내부적으로 자바 변수로 선언되는게 아니라, page 데이터 영역의 애트리뷰트로 선언된다.
      - 따라서, <code><%=변수 이름%></code>형태로 출력될 수 없다.

    <br/>

    <br/>

  - <b>\<c:remove></b>

    - 변수를 제거할 때 사용한다.

    - 첫 번째 범위 또는 지정된 범위의 변수를 제거한다.

      ``` html
      <!-- 모든 scope에서 해당 이름을 가진 변수를 다 제거 -->
      <c:remove var="변수이름"/>
      
      <!-- 특정 영역의 변수 제거 예시 -->
      <c:remove var="변수이름" scope="request"/>
      ```

    <br/>

    <br/>

  - <b>\<c:choose>, \<c:when>, \<c:otherwise></b>

    - choose
      - 일종의 switch 문처럼 작동한다.
      - 상호 배타적인 조건부 작업에 대한 컨텍스트를 설정하는 조건부 태그
    - when
      - 조건이 'true'인 경우, 본문을 포함하는 choose의 하위 태그
    - otherwise
      - choose의 하위 태그
      - when 태그를 따르며, 평가된 모든 이전 조건이 'false'일 경우에만 실행한다.

    ``` html
    <c:choose>
    	<c:when tes="${1 > 0}">
        	1은 0보다 큽니다.<br/>
        </c:when>
        <c:when test="${2 > 0}">
        	2도 0보다 큽니다.<br/>
        </c:when>
        <c:otherwise>
        	웬만한 숫자는 0보다 크지요.<br/>
        </c:otherwise>
    </c:choose>
    ```

    <br/>

    <br/>

  - <b>\<c:forEach></b>

    - 중첩된 본문 내용을 고정된 횟수만큼 또는 컬렉션의 반복에 사용되는 반복 태그이다.
    - for 문과 비슷하다.
    - 자바 스크립트를 포함하는 동안, 스크립트릿을 통해, 또는 루프 용으로 사용하기에 좋은 대안으로 사용한다.
    - 객체 컬렉션을 반복하므로 가장 일반적으로 사용한다.

    ```html
    <!-- 1, 3, 5, 7 -->
    <c:forEach var="임시변수명" begin="1" end="10" step="2">
    	${임시변수명}<br/>
    </c:forEach>
    
    <!-- 배열의 내용을 순서대로 출력, 향상된 for문과 비슷 -->
    <c:forEach var="배열 요소를 저장할 임시변수 이름" items="${배열이름}">
    	${배열 요소를 저장할 임시변수 이름}<br/>
    </c:forEach>
    ```

    <br/>

    <br/>

  - <b>\<c:forTokens></b>

    - 문자열에 포함된 토큰을 분리해서, 각각의 토큰에 대해 반복 처리를 수행하도록 만드는 기능이다.

    ``` html
    <c:forTokens var="temp" items="ㅋㅋㅋ ㅎㅎㅎ ㅉㅉㅉ" delims=" ">
    	${temp}<br/>
    </c:forTokens>
    
    <!-- 결과 -->
    ㅋㅋㅋ
    ㅎㅎㅎ
    ㅉㅉㅉ
    
    <!-- delims에 여러 개를 넣으면 여러 토큰 가능 -->
    <c:forTokens var="temp" items="ㅋㅋㅋ^ㅎㅎㅎ@ㅉㅉㅉ!ㅍㅍㅍ^ㄷㄷㄷ" delims="^@!">
    	${temp}<br/>
    </c:forTokens>
    
    <!-- 결과 -->
    ㅋㅋㅋ
    ㅎㅎㅎ
    ㅉㅉㅉ
    ㅍㅍㅍ
    ㄷㄷㄷ
    ```

    <br/>

    <br/>

  - <b>\<c:if></b>

    - 조건을 테스트하는 데 사용한다.
    - 평가된 표현식이 ture인 경우 본문 내용을 표시한다.

    ``` html
    <c:set var="income" scope="session" value="${4000*4}"/>
    <c:if test="${income > 8000}">
    	<p>
            My income is : <c:out value="${income}"/>
        </p>
    </c:if>
    ```

    <br/>

    <br/>

  - <b>\<c:import></b>

    - jsp 'include'와 유사하다.
    - url 속성에 콘텐츠가 있는 주소를 지정하면, 해당 주소로 요청하고 응답 결과를 받아서 반환한다.

    ``` html
    <c:import url="url" var="변수명" scope="page(기본값) | request | session| application"/>
    
    <!-- url에 로또 800회차 당첨 결과를 JSON으로 반환 받을 결과를 출력하는 예제 -->
    <c:import var="lottoResutl" url="https://www.nlotto.co.kr/common.do?method=getLottoNumber&drwNo=800"/>
    <textarea rows="10" cols="80">
    	${lottoResult}
    </textarea>
    ```

    <br/>

    <br/>

  - <b>\<c:redirect></b>

    - 리다이렉트 처리 시 사용한다.
    - 내부적으로 HttpServletResponse의 sendRedirect()를 호출한다.
    - <code><c:redirect url="url"/></code>

    <br/>

    <br/>

  - <b>\<c:url></b>

    - URL을 만들 때 사용한다.
    - 이 태그를 사용하면, 매개 변수를 포함한 URL을 쉽게 만들 수 있다.

    ``` html
    <c:url var="변수명" value="url">
    	<c:param name="파라미터명" value="값"/>
        <c:param name="파라미터명" value="값"/>
        <c:param name="파라미터명" value="값"/>
    </c:url>
    ```

    <br/>

    <br/>

  - <b>\<c:param></b>

    - 포함하는 'import' 태그의 URL에 매개 변수를 추가한다.
    - URL 내에 적절한 URL 요청 매개 변수를 지정할 수 있다.
    - 필요한 URL 인코딩을 자동으로 수행한다.
    - value 속성은 매개 변수 값을 나타내고 name 속성은 매개 변수 이름을 나타낸다.

    ``` html
    <c:url value="/index.jsp" var="completeURL">
    	<c:param name="trackingId" value="786"/>
    	<c:param name="user" value="Nakul"/>
    </c:url>
    ${completeURL}
    
    <!-- 결과 -->
    /~~~/index1.jsp?trackingId=786&user=Nakul
    ```

    <br/>

    <br/>

  - <b>\<c:catch></b>

    - 본문에서 발생하는 Throwable 예외를 포착하고 선택적으로 노출시키는 데 사용한다.
    - 일반적으로 오류 처리에 사용되며, 프로그램에서 발생하는 문제를 보다 쉽게 처리한다.

    ``` html
    <c:catch var="catchtheException">
    	<% int x = 2/0; %>
    </c:catch>
        
    <c:if test = "${catchtheException != null}">
    	<p>
            The type of exception is : ${catchtheException} br/>
            There is an exception: ${catchtheException.message}
        </p>
    </c:if>
        
    <!-- 결과 -->
    The type of exception is : java.lang.ArithmeticException : / by zero
    There is an exception : / by zero
    ```

    

<br/>

<br/>

<br/>

## 예상질문❔

Q1) JSTL이란 무엇인가?

A1) JSP에서 자주 사용될 수 있는 커스텀 태그들을 표준으로 모아놓은 태그 라이브러리이다.

<br/>

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/KJY/%5BWEB%5D%20JSTL.md
- https://github.com/fake-developers/1st/blob/main/BJY/Jstl.md

