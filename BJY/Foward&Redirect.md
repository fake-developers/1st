## Foward & Redirect

<br/>

*  **웹에서 페이지 전환 방식**
   * JSP 환경에서 현재 작업중인 페이지에서 다른 페이지로 이동하는 페이지 전환기능

<br/>

### <u>Forward</u>

![forward](https://user-images.githubusercontent.com/61674527/117671026-5ebbf180-b1e3-11eb-9391-f5d03028b4f4.png)

<br>

- Web Container 차원에서의 페이지 이동만 존재
  - 실제로 웹 브라우저는 다른 페이지로 이동했음을 알 수 없다.
- 웹 브라우저에는 최초에 URL이 표시되고 이동한 페이지의 URL 정보는 볼 수 없다.
- 동일한 web container 차원에서의 페이지 이동만 가능
- 현재 실행중인 페이지와 forward에 의해 호출된 페이지는 request, response 객체를 공유
  - 말그대로 '건네주기'
  - 따라서, 사용자가 최초로 요청한 요청정보가 다음 URL에서도 유효
- 클라이언트와 통신없이 서버에서만 처리
  - redirect보다 나은 성능을 보여준다.

<br>

#### 예시

>1. 고객이 고객센터로 상담원에게 123번으로 전화를 건다.
>2. 상담원은 해당 문의사항에 대해 잘 알지 못해 옆의 다른 상담원에게 해당 문의사항에 답을 얻는다.
>3. 상담원은 고객에게 문의사항을 처리해준다.

<br/>

#### 동작과정

![forward동작과정](https://user-images.githubusercontent.com/61674527/117675146-48b03000-b1e7-11eb-8bf8-104c02745f08.png)

1. 웹 브라우저에서 Servlet1에 요청을 보냄
2. Servlet1은 요청을 처리한 후, 그 결과를 HttpServletRequest에 저장
3. Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송(forward)
   - 이때 특정 값을 전달하기 위해 request의 setAttribute() 메서드 이용
   - 값을 넘길 서블릿인 Servlet2를 지정하기 위해 request의 getRequestDispather() 메서드 이용
   - 마지막으로 RequestDispather의 forward() 메서드를 통해 전달할 request와 response를 인자로 받는다.
4. Servlet2는 Servlet1으로 부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청을 처리한 후 웹 브라우저에게 결과를 전송

<br>

### <u>Redirect</u>

![redirect](https://user-images.githubusercontent.com/61674527/117674617-c9baf780-b1e6-11eb-9f05-95426e4a9824.png)



<br/>

- Web Container는 redirect 명령이 들어오면 웹 브라우저에게 다른 페이지로 이동하라는 명령을 내린다.
- 웹 브라우저는 URL을 지시된 주소로 바꾸고 그 주소로 이동
- **다른 web container에 있는 주소로 이동**
- 새로운 페이지에서 request, response 객체가 새롭게 생성
  - 최초받은 URL1에서 클라이언트에 redirect할 URL2를 리턴
  - 클라이언트에게 전혀 새로운 요청을 생성하여 URL2에 다시 요청
  - 따라서, 처음 보냈던 최초의 요청정보는 더이상 유효하지 않음

<br>

#### 동작 과정

![redirect동작과정](https://user-images.githubusercontent.com/61674527/117675490-92991600-b1e7-11eb-883b-44dda384ef02.png)

1. 브라우저가 redirect01.jsp를 요청

2. 서버가 redirect01에 대한 응답 객체 브라우저에 전달

   - 응답 객체에는 redirect02로 다시 요청하라는 내용이 담겨있다.
   - 응답코드 : 302, Location헤더 값 : redirect02.jsp

3. 웹 브라우저는 응답 데이터 속에서 WAS의 리다이렉트 요청을 확인하고 redirect02.jsp를 다시 요청

   - 웹 브라우저는 응답을 받으면 헤더에 포함된 URL로 재요청한다.
   - 서블릿이나 JSP는 redirect하기 위해 HttpServletResponse클래스의 sendRedirect() 메서드 사용

   ```
   response.sendRedirect("redirect02.jsp");
   ```

4. WAS는 redirect02요청에 대한 결과를 출력

<br/>

### <u>Foward VS Redirect</u>

**URL 변화 여부**

* foward : 변화 없음
* redirect : 변화 있음

**객체의 재사용 여부**

* foward : 재사용
* redirect : 재사용 하지 않음

**각 방식의 적용 사례**

- 글쓰기 기능을 수행 시, 응답 페이지는  : **redirect**
  - forward의 경우 요청 정보가 그대로 살아있기 때문에, 똑같은 글이 여러번 등록될 수 있다.
  - redirect의 경우 처음 글을 작성할 때 보냈던 요청정보는 존재하지 않는다.
  - 또한, 글쓰기 기능을 하는 URL1이 아닌 URL2로 요청 보내기 때문에 글쓰기가 여러번 수행되지 않는다.

- 시스템 (Session 또는 DB 등)에 변화가 생기는 요청의 경우 redirect가 바람직하다.
  - ex) 로그인, 회원가입, 글쓰기
- 시스템에 변화가 생기지 않는 단순조회 (리스트보기, 검색)의 경우 forward 방식으로 응답하는 것이 바람직하다.

<br/>

<br/>

<br/>

### REFERENCE

* https://github.com/fake-developers/1st/blob/JYJ-10/JYJ/ForwardAndRedirect.md
* https://github.com/fake-developers/1st/blob/SJH-10/SJH/Forward%26Redirect.md
* https://wondongho.tistory.com/65
* https://doublesprogramming.tistory.com/63
* https://velog.io/@denmark-choco/HTTPRedirect%EC%99%80-Forward%EC%9D%98-%EC%B0%A8%EC%9D%B4

