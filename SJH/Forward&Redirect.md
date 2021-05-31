# Forward & Redirect

- 웹에서 **페이지 전환 방식**
  - JSP 환경에서 현재 작업중인 페이지에서 다른 페이지로 이동하는 페이지 전환기능

<br>

## Forward 방식

- **Web Container 차원에서의 페이지 이동만 존재**
  - 실제로 웹 브라우저는 다른 페이지로 이동했음을 알 수 없다.
- 웹 브라우저에는 최초에 URL이 표시되고 이동한 페이지의 URL 정보는 볼 수 없다.
- 동일한 web container 차원에서의 페이지 이동만 가능
- **현재 실행중인 페이지와 forward에 의해 호출된 페이지는 request, response 객체를 공유**
  - 말그대로 '건네주기'
  - 따라서, 사용자가 최초로 요청한 요청정보가 다음 URL에서도 유효
- 클라이언트와 통신없이 서버에서만 처리
  - redirect보다 나은 성능을 보여준다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb9U3fY%2FbtqyeoHglrc%2Fl6VDZbutBoO49LXwQEf8D1%2Fimg.png" height=350>

- **사례**

  - 고객 : 클라이언트, 123번 : URL, 상담원 : 서버

  1. 고객이 123번으로 고객센터 상담원에게 전화를 건다.
  2. 상담원은 해당 문의사항에 대해 잘 안지 못해서 옆의 상담원에게 해당 문의사항의 답을 얻는다.
  3. 상담원은 고객에게 문의사항을 처리해준다.

- **동작 과정**

  <img src="https://t1.daumcdn.net/cfile/tistory/9964974A5D510DA10B">

  1. 웹 브라우저에서 Servlet1에 요청을 보냄

  2. Servlet1은 요청을 처리한 후, 그 결과를 HttpServletRequest에 저장

  3. Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송(forward)

     - 이때 특정 값을 전달하기 위해 request의 setAttribute() 메서드 이용
     - 값을 넘길 서블릿인 Servlet2를 지정하기 위해 request의 getRequestDispather() 메서드 이용
     - 마지막으로 RequestDispather의 forward() 메서드를 통해 전달할 request와 response를 인자로 받는다.

     ~~~java
     //key, value를 이용하며, key에는 servlet2에서 값을 호출할 이름 입력
     request.setAttribute("dice", diceValue);
     //서블릿 지정
     RequestDispatcher requestDispatehcer = request.getRequestDispatcher("/next");
     requestDispatehcer.forward(request, response);
     ~~~

  4. Servlet2는 Servlet1으로 부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청을 처리한 후 웹 브라우저에게 결과를 전송

<br>

## Redirect 방식

- Web Container는 redirect 명령이 들어오면 웹 브라우저에게 다른 페이지로 이동하라는 명령을 내린다.
- 웹 브라우저는 URL을 지시된 주소로 바꾸고 그 주소로 이동
- **다른 web container에 있는 주소로 이동 **
- **새로운 페이지에서 request, response 객체가 새롭게 생성**
  - 최초받은 URL1에서 클라이언트에 redirect할 URL2를 리턴
  - 클라이언트에게 전혀 새로운 요청을 생성하여 URL2에 다시 요청
  - 따라서, 처음 보냈던 최초의 요청정보는 더이사아 유효하지 않음

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FF3O4A%2FbtqydA2GDYr%2FtgFznDMjbIe9YK2buOruvK%2Fimg.png" height=350>

 

- **사례**

  - 고객 : 클라이언트, 123번 : URL, 상담원 : 서버

  1. 고객이 123번으로 고객센터 상담원에게 전화를 건다.
  2. 상담원은 고객에게 다음과 같이 이야기 한다. "고객님 해당 문의사항은 124번으로 다시 문의 해주시겠어요?"
  3. 고객은 124번으로 문의해서 일을 처리한다.

- **동작 과정**

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdyfZbw%2FbtqCkP2O1vU%2FbuwzgkaPukjmloawGOMNUK%2Fimg.png">

  1. 브라우저가 redirect01.jsp를 요청

  2. 서버가 redirect01에 대한 응답 객체 브라우저에 전달

     - 응답 객체에는 redirect02로 다시 요청하라는 내용이 담겨있다.
     - 응답코드 : 302, Location헤더 값 : redirect02.jsp

  3. 웹 브라우저는 응답 데이터 속에서 WAS의 리다이렉트 요청을 확인하고 redirect02.jsp를 다시 요청

     - 웹 브라우저는 응답을 받으면 헤더에 포함된 URL로 재요청한다.
     - 서블릿이나 JSP는 redirect하기 위해 HttpServletResponse클래스의 sendRedirect() 메서드 사용

     ~~~
     response.sendRedirect("redirect02.jsp");
     ~~~

  4. WAS는 redirect02요청에 대한 결과를 출력 

- **Spring에서 Redirect 사용 예시**

  - 게시물을 추가한 후 게시물 목록을 보도록 redirect해주는 코드

  ~~~java
  package com.mang.board.controller;
  import com.mang.board.vo.BoardVO;
  import java.util.List;
  
  @Controller 
  @RequestMapping("/board") 
  public class BoardController { 
      @Resource(name="boardService") 
      private BoardService boardService; 
      
      @PostMapping(value="/insertBoardInfo") 
      public String insertBoardInfo(HttpServletRequest request,  @ModelAttribute BoardVO boardVO) throws Exception{ 
          int rsCnt = boardService.insertBoardInfo(request, boardVO); 
          if(rsCnt < 1) { 
              return "/cmmn/error"; 
          }
          return "redirect:/board/retrieveBoardList"; 
      } 
      
      @GetMapping(value="/retrieveBoardList")
      public String retrieveBoardList(Model model) throws Exception {
          List boardList = boardService.retrieveBoardList(); 
          model.addAttribute("boardList", boardList);
          return "/board/boardListView"; 
      }
  }
  ~~~

  

<BR>

## Forward vs Redirect

|                  | redirect | forward |
| ---------------- | -------- | ------- |
| URL 변화 여부    | O        | X       |
| 객체 재사용 여부 | X        | O       |

- **사용에 따른 구별**
  - Forward 
    - **시스템(session, DB)에 변화가 생기지 않는 단순조회**
    - ex_) 리스트 보기, 검색
  - Redirect
    - **시스템(session, DB)에 변화가 생기는 요청**
    - ex_) 로그인, 회원가입, 글쓰기

<br>

----------

**<참조>**

- [Redirect VS, Forward (Redirect와 forward의 차이)](https://doublesprogramming.tistory.com/63)
- [redirect & forward 개념과 차이점](https://goodncuteman.tistory.com/58)
- [[Web] Forward와 Redirect 차이](https://mangkyu.tistory.com/51)

- [[부스트코스] forward란? (forward와 redirect 차이)](https://bellog.tistory.com/80)
- [[부스트코스] 리다이렉트(redirect)란?](https://bellog.tistory.com/79?category=911042)

- [HTTP_Redirect와 Forward의 차이](https://velog.io/@denmark-choco/HTTPRedirect%EC%99%80-Forward%EC%9D%98-%EC%B0%A8%EC%9D%B4)