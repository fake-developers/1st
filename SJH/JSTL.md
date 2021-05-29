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

- **Core Tags**
  - 



------

**<참조>**

- [JSTL:::: 개념, 설치법, 코어 라이브러리 포매팅 라이브러리 함수 라이브러리 사용법](https://seven00.tistory.com/entry/JSTL%EA%B0%9C%EB%85%90%EC%84%A4%EC%B9%98%EB%B2%95%EC%BD%94%EC%96%B4-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%8F%AC%EB%A7%A4%ED%8C%85-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%95%A8%EC%88%98-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EC%82%AC%EC%9A%A9%EB%B2%95)

- [[JSP] JSTL 정리](https://velog.io/@ye050425/JSP-JSTL-%EC%A0%95%EB%A6%AC#xml-tags)

