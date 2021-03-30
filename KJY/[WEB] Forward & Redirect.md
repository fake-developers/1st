# [WEB] Forward & Redirect

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-30)* 

<br/>

#### :pushpin: 페이지 전환 방식

* 웹은 현재 페이지에서 다른 페이지로 페이지 전환을 하기 위해 2가지 기능을 제공함 (JSP환경)
  * forward 방식
  * redirect 방식

<br/>

## 1. Forward

* ![img](https://blog.kakaocdn.net/dn/b9U3fY/btqyeoHglrc/l6VDZbutBoO49LXwQEf8D1/img.png)

* '건내주기'

* WAS의 서블릿/JSP가 요청을 받은 후 처리하다가, 추가적인 처리를 같은 웹 어플리케이션 안에 포함된 다른 서블릿/JSP에게 위임하는 경우

* **웹 컨테이너(Web Container) 차원에서 페이지 이동만 있는 것**
  
  * 동일한 web container 차원(내부)에서의 페이지 이동만 가능
    * 자원 공유 가능
  
* 실제 웹 브라우저가 다른 페이지로 이동했는지 알 수 없음
  * 웹 브라우저에서는 최초에 호출한 URL이 표시됨
  * 이동한 페이지의 URL 정보는 볼 수 없음
  
* 클라이언트와 통신 없이, 서버에서만 처리됨

  * 클라이언트 입장에서는 한 번의 요청으로 결과물을 받아볼 수 있ㅇ음

  * redirect보다 나은 성능을 보여줌

* **현재 실행중인 페이지와, Forwarding에 의해 호출될 페이지는 Request와 Response 객체를 공유함**
  
  * 객체를 요청에 담고, 해당 요청을 사용할 다음 자원에 전송함
  
* **시스템에 변화가 생기지 않는** 단순 조회, 검색의 경우에 사용

* 단점 : 사용자가 새로고침(F5)시, 요청처리가 내부적으로 생기기 때문에 현재 보여지는 화면이 그대로 나올 수 없는 경우가 생길 수 있음

<br/>

#### 1-1. 동작과정

1. 웹 브라우저에서 Servlet1에게 요청을 보냄

2. Servlet1은 요청을 처리한 후, 그 결과를 HttpServletRequest에 저장

3. Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송 (forward)

   * 이때 객체 정보는 Request Scope, Session Scope, Page Scope를 통해 전달됨

   * ```java
     //값 설정 (key: nextServlet에서 호출할 이름, value: 실제 전달받을 값)
     request.setAttribute("dice", diceValue);
     
     //전달. 포워딩을 수행할 서블릿 지정
     RequestDispatcher requestDispatcher = request.getRequestDispatcher("/nextServlet");    //JSP 경로도 가능
     requestDispatcher.forward(request, response);
     ```

4. Servlet2는 Servlet1으로 부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청을 처리한 후 웹 브라우저에게 결과를 전송

<br/>

## 2. Redirect

* ![img](https://blog.kakaocdn.net/dn/F3O4A/btqydA2GDYr/tgFznDMjbIe9YK2buOruvK/img.png)

* HTTP 프로토콜로 정해진 규칙

* 서버가 클라이언트로부터 요청을 받은 후, 클라이언트에게 특정 URL로 이동하라고 요청하는 경우

* 웹 컨테이너(Web Container)로 명령이 들어옴

  -> 웹 브라우저에게 다른 페이지로 이동하라고 명령을 내림

  -> 웹 브라우저는 URL을 바꾸고 해당 주소로 이동함

* **다른 웹 컨테이너에 있는 주소로 이동**

  * Client에서 새로운 Location에 대해 요청을 하기 때문에, Web Container 내부에서 자원을 공유할 수 없음
    * 자원을 공유하려면 QueryString을 생성해야 함

* **새로운 페이지에서는 Request와 Response 객체가 새롭게 생성됨**

* 최초 요청을 받은 URL1에서 클라이언트에게 redirect할 URL2를 반환

  -> 클라이언트에서는 새로운 요청을 생성하여 URL2에 다시 요청을 보냄

  -> 처음 보냈던 최초 Request, Response 객체는 유효하지 않고 새롭게 생성됨

* **시스템(Session,DB)에 변화가 생기는** 로그인, 회원가입, 글쓰기 등에 이용

* 단점 : 요청 객체를 잃어버리는 경우가 생길 수 있음

<br/>

#### 2-1. 동작과정

![img](https://blog.kakaocdn.net/dn/dyfZbw/btqCkP2O1vU/buwzgkaPukjmloawGOMNUK/img.png)

1. 서버에서 클라이언트에게 요청을 받으면 응답객체를 반환
   * 응답 객체에는 상태코드 : 302, Location 값 : 이동할 URL을 담음

2. 클라이언트는 서버로부터 받은 **상태 값이 302이면 Location헤더값으로 재요청**을 보내게 됨
   * 서버는 새로운 Resource를 응답함
   * 이때 브라우저의 주소창은 전송받은 URL로 바뀌게 됨

* 서블릿/JSP는 리다이렉트하기 위해 **HttpServletResponse 클래스의 sendRedirect() 메소드**를 사용함

  * ```java
    //redirect01.jsp
    response.sendRedirect("redirect02.jsp");
    ```

<br/>

## 3. Forward VS Redirect

|                  | redirect | forward |
| ---------------- | -------- | ------- |
| URL 변화 여부    | O        | X       |
| 객체 재사용 여부 | X        | O       |

#### 3-1. 사례

* 고객 : 클라이언트, 123번 : URL, 상담원 : 서버
* **사례 1 (forward)**
  1. 고객이 고객센터 상담원에게 123번으로 전화를 건다.
  2. 상담원은 해당 문의사항에 대해 잘 알지 못해, 옆의 다른 상담원에게 물어 답을 얻는다.
  3. 상담원은 고객에게 문의사항을 처리해준다.
* **사례 2 (redirect)**
  1. 고객이 고객센터 상담원에게 123번으로 전화를 건다.
  2. 상담원은 고객에게 이야기 한다. "고객님, 해당 문의사항은 124번으로 다시 문의해주시겠어요?"
  3. 고객은 다시 124번으로 문의해서 일을 처리한다.
* **forward**
  * 실제 웹 브라우저가 다른 페이지로 이동했는지 알 수 없음
    * 고객은 상담원이 누구한테 물어봤는지의 여부를 알 수 없다.
  * 이동한 페이지의 URL 정보는 볼 수 없음
    * 고객은 123번으로만 전화했기 때문에 알 수 없다.
  * 동일한 web container 차원(내부)에서의 페이지 이동만 가능
    * 상담원이 옆의 상담원에게 물어봄
  * 현재 실행중인 페이지와, Forwarding에 의해 호출될 페이지는 Request와 Response 객체를 공유함
    * 고객이 요청한 문의사항은 고객이 전화를 끊을 때까지 유효하다.
* **redirect**
  *  web container는 redirect명령이 들어오면 웹 브라우저에게 다른 페이지로 이동하라고 명령을 내림
    * 고객은 전화를 끊고, 다른 번호로 다시 전화를 건다.
  * 웹 브라우저는 URL을 바꾸고 해당 주소로 이동함
    * 고객은 전화를 끊고 124번으로 전화를 건다.
  * 다른 웹 컨테이너에 있는 주소로 이동
    * 123 -> 124
  * 새로운 페이지에서는 Request와 Response 객체가 새롭게 생성됨
    * 123번에서 고객이 요청했던 문의사항은 사라지고, 124번으로 건 뒤 문의사항을 다시 말해야 한다.

<br/>

## 4. Spring에서 Redirect 사용 (예시)

```java
//게시물을 추가한 후에 게시물 목록을 보도록 redirect하는 코드
package com.mang.board.controller;

import com.mang.board.vo.BoardVO;
import java.util.List;

@Controller
@RequestMapping("/board")
public class BoardController {

	@Resource(name="boardService")
	private BoardService boardService;

	@PostMapping(value="/insertBoardInfo")
	public String insertBoardInfo(HttpServletRequest request, @ModelAttribute BoardVO boardVO) throws Exception{
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
```



<br/>

## :page_with_curl: Reference

[HTTP_Redirect와 Forward의 차이](https://velog.io/@denmark-choco/HTTPRedirect%EC%99%80-Forward%EC%9D%98-%EC%B0%A8%EC%9D%B4)

[웹에서 forward와 redirect의 차이](https://jw910911.tistory.com/23)

[Redirect와 Forward의 차이에 대해](https://nesoy.github.io/articles/2018-04/Redirect-Forward)

[포워드(forward)와 리다이렉트(redirect) 차이](https://vitalholic.tistory.com/48)

[redirect & forward 개념과 차이점](https://goodncuteman.tistory.com/58)

[[Web] Forward와 Redirect 차이](https://mangkyu.tistory.com/51)

[[부스트코스] forward란? (forward와 redirect 차이)](https://bellog.tistory.com/80)

[[부스트코스] 리다이렉트(redirect)란?](https://bellog.tistory.com/79?category=911042)

[Redirect VS, Forward (Redirect와 forward의 차이)](https://doublesprogramming.tistory.com/63)