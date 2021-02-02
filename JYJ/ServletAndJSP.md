# 서블릿과 JSP

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : Jeonghea Shin*

<hr>
- <b>서블릿이란?</b>

  ``` java
  import java.io.*;
  import javax.servlet.*;
  import javax.servlet.http.*;
  
  public ThreeParams extends HttpServlet {
      public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          
          response.setContentType("text/html");
          printWriter out = response.getWriter();
          
          String title = "Reading Three Request Parameters";
          String docType = "<!DOCTYPE html PUBLIC \"-//W3C//DTD HTML 4.01 Transitional//EN\">\n";
          
          out.println(docType + 
              "<HTML>\n" +
              "<HEAD><TITLE>" + title + "</TITLE></HEAD>\n" +
              "<BODY BGCOLOR=\"#FDF5E6\">\n" +  
              "<H1 ALIGN=\"CENTER\">" + title + "</H1>\n" + 
              "<UL>\n" + 
              "<LI><B>param1</B>: " + request.getParameter("param1") + "\n" +
              "<LI><B>param2</B>: " + request.getParameter("param2") + "\n" +
              "<LI><B>param3</B>: " + request.getParameter("param3") + "\n" +
              "</UL>\n" +
              "</BODY></HTML>");
          )
      }
  }
  ```

  - <b>웹 기반의 요청에 대한 동적인 처리를 수행하기 위해 자바로 작성된 프로그램이다.</b>
  - .java가 확장자
  - java 코드 안에 HTML 코드를 사용한다.
  - 웹 개발을 위해 만든 표준이다.
  - <b>서블릿이 수정된 경우 java 코드를 컴파일한 후 동적인 페이지를 처리하기 때문에 전체 코드를 업데이트하고 다시 컴파일한 후 재배포하는 작업이 필요하다.</b>
    - 개발 생산성이 저하된다.

  <br/>

  <br/>

- <b>서블릿의 단점</b>
  - 비효율적인 측면이 많다.
      - 서블릿은 자바에 대한 지식이 필요하다.
      - 화면 인터페이스 구성에 너무 많은 코드들이 필요하다.
  - <b>때문에 서블릿을 작성하지 않고 웹프로그래밍을 쉽게 할 수 있게 해주는 기술이 바로 JSP 이다.</b>

<br/>

<br/>

<br/>

- <b>JSP란?</b>

    ``` html
    <HTML>
    <HEAD>
    <TITLE>Reading Three Request Parameters</TITLE>
    <LINK REL=STYLESHEET HREF="JSP-Styles.css" TYPE="text/css">
    </HEAD>
    
    <BODY>
    <H1>Reading Three Request Parameters</H1>
    <UL>
        <LI><B>param1</B>: <%= request.getParameter("param1") %>
        <LI><B>param2</B>: <%= request.getParameter("param2") %>
        <LI><B>param3</B>: <%= request.getParameter("param3") %>
    </UL>
    </BODY>
    </HTML>
    ```

    - 서블릿의 단점을 보완해서 만든 서블릿 기반의 서버 스크립트 기술

        - Servlet의 모든 기능 + 추가적인 기능

        <small>* 스크립트 기술 : ASP, PHP 처럼 미리 약속된 규정에 따라 간단한 키워드를 조합하여 입력하면, 실행 시점에 각각의 키워드에 매핑이 되어 있는 어떤 코드로 변환 후에 실행되는 형태</small>

    - HTML 코드 안에 Java 코드

    - JSP가 수정된 경우 재배포할 필요 없이 WAS가 알아서 처리한다.

        - 쉬운 배포가 장점이다.

<br/>

<br/>

- <b>서블릿 vs JSP</b>

  | Servlet                                                      | JSP                                                     |
  | ------------------------------------------------------------ | ------------------------------------------------------- |
  | 웹 기반 요청에 대한 동적 처리가 가능한 서버 사이드 자바 프로그램 | Java 언어 기반의 서버 사이드 스크립트 언어              |
  | 자바 코드안에 HTML 코드가 존재한다. (하나의 클래스)          | HTML 코드 안에 자바 코드                                |
  | HTML 태그를 문자열 ("") 스트림으로 처리한다.                 | 자바코드를 <%%> 태그 안에 처리한다.                     |
  | 웹 개발을 위해 만든 표준이다.                                | 서블릿을 보완하고 기술을 확장한 스크립트 방식 표준이다. |
  | DB와 통신, 비즈니스 로직 호출, 데이터 리딩 체크 작업에 유용하다. | 요청 결과를 나타내는 HTML 작성 시 유용하다.             |
  | 데이터 프로세싱 부분에 활용하기 좋다.                        | 프레젠테이션 부분에 활용하기 좋다.                      |
  | 수정 시, 재배포 작업이 필요하다.                             | 수정 시, 재배포 작업이 필요 없다.                       |

  <br/>

  <br/>

- <b>결론</b>

  - 결과적으로, <b>Servlet과 JSP는 만드는 방법에 차이가 있을 뿐 동일한 역할</b>을 한다.
  - 초기에 자바 웹 개발은 서블릿을 이용한 개발이었으나,
    - 이후, JSP 기술이 발표되면서 현재는 Servlet과 JSP를 혼합하여 사용하는 형태로 개발이 이루어지고 있다.
    - 대표적으로 MVC 패턴이 있다.
  - MVC 패턴
    - JSP와 Servlet을 모두 이용해 프레젠테이션 로직과 비즈니스 로직을 분리한다.
    - JSP 기술의 장점을 최대한 활용할 수 있는 프리젠테이션 계층을 담당한다.
    - 서블릿은 사용자의 요청을 분석하고 비즈니스 층과 통신하여 처리하고 그 결과를 다시 사용자에게 응답하는 컨트롤러 층을 담당한다.
    - model은 자바 빈즈로, DTO와 DAO를 통해 데이터 스토리지에 접근한다.

<br/>

<br/>

## 예상질문❔

Q1) JSP란 무엇인가?

A1) 웹 기반의 요청에 대한 동적인 처리를 수행하기 위해 자바로 작성된 프로그램이다. 자바에 대한 지식이 필요하고 화면에 많은 코드들이 필요하여 비효율적이라 JSP를 사용한다.

<br/>

Q2) JSP란 무엇인가?

A2) 서블릿의 단점을 보완해서 만든 서블릿 기반의 서버 스크립트 기술이다. JSP가 수정된 경우 재배포할 필요 없이 WAS가 알아서 처리하여 배포가 쉽다.

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/SJH/Servlet&JSP.md

