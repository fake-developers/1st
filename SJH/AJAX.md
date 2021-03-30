# AJAX

- Asynchronous Javascript And Xml(비동기식 자바스크립트와 xml)의 약자
- **JavaScript를 사용한 비동기 통신, 클라이언트와 서버간에 다양한 데이터(JSON, XML, HTML, 텍스트 파일 등..)를 주고 받는 기술**
- 빠르게 동작하는 동적인 웹 페이지를 만들기 위한 개발 기법의 하나
  - 브라우저가 가지고 있는 XMLHttpRequest 객체를 이용하여,
  - 전체 페이지를 새로 고치지 않고도 페이지의 일부분만을 위한 데이터를 로드하는 기법

<BR>

## AJAX 특징

- **비동기 방식**

  - 페이지를 리로드하지 않고 데이터를 불러오는 방식

  - 즉, AJAX를 통해 서버에 요청을 한 후 멈춰 있는 것이 아니라 프로그램은 계속 돌아간다는 것이다.

    <img src="https://media.vlpt.us/post-images/surim014/233bbf90-2d60-11ea-a24d-4f910e80580b/image.png" height=240> 

    - **필요한 부분만을 불러와 사용할 수 있으므로 효율적** 이다. 

- **페이지 새로고침 없이, 일부만 갱신 가능**

  - XMLHttpReuqest객체를 통해 서버에 request하여 일부분만 갱신가능
  - **JSON이나 XML 형태로 필요한 데이터만 받아 갱신하기 때문에 그만큼의 자원과 시간 절약**

<BR>

## AJAX 장단점

- **장점**
  - 웹페이지 속도향상
  - 서버의 처리가 완료될 때까지 기다리지 않고 처리 가능
  - 서버에서 Data만 전송하면 되므로 전체적인 코딩의 양이 줄어든다.
    - 전체 페이지를 보내지 않고 요청에 맞는 값만 보내면 된다는 뜻
  - 기존 웹에서 불가능했던 다양한 UI를 가능하게 한다
    - Flickr(미국 사진 공유 커뮤니티)의 경우, 사진의 제목이나 태그를 페이지 리로드 없이 수정 가능
- **단점**
  - 히스토리가 관리되지 않는다.
  - 페이지 이동 없는 통신이므로 보안상의 문제가 생길 수 있다.
  - 연속적으로 데이터를 요청하면 서버 부하가 증가할 수 있다.
  - XMLHttpRequest를 통해 통신하는 경우, 사용자에게 아무런 진행 정보가 주어지지 않는다.(따라서, 요청이 완료되지 않았는데 사용자가 페이지를 떠나거나 오작동할 우려 발생)
  - AJAX를 쓸 수 없는 브라우저에 대한 문제 이슈가 있다.
  - AJAX는 클라이언트가 서버에 데이터를 요청하는 *클라이언트 풀링 방식* 을 사용하므로 *서버 푸시 방식* 의 실시간 서비스는 만들 수 없다.
    - 클라이언트 풀링 방식 :  사용자가 직접 원하는 정보를 서버에게 요청하여 얻는 방식
    - 서버 푸시 방식 : 사용자가 요청하지 않아도 서버가 자동으로 특정 정보를 제공하는 것
  - *동일-출처 정책* 으로 인해 다른 도메인과 통신이 불가능하다.
    - 동일- 출처 정책 : 어떤 출처에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 보안 방식
  - 바이너리 데이터를 보내거나 받을 수 없다.

<br>

## AJAX 구성요소

- Ajax는 기존에 사용되던 여러기술을 함께 사용되어 이루어진다.
  - 웹 페이지의 표현을 위한 **HTML** 과 **CSS**
  - 데이터에 접근하거나 화면 구성을 동적으로 조작하기 위해 사용되는 **[DOM 모델](./BOM&DOM.md)**
  - 데이터의 교환을 위한 **JSON** 이나 **XML**
  - 웹 서버와 비동기식 통신을 위한 **XMLHttpRequest 객체**
  - 위에서 언급한 모든 기술을 결합하여 사용자의 작업 흐름을 제어하는데 사용되는 **자바스크립트**

<br>

## AJAX 진행과정

1. **XMLHttpRequest Object를 만든다.**

   - request를 보낼 준비를 브라우저에게 시키는 과정
   - 이것을 위해서 필요한 method를 갖춘 object가 필요함

   ~~~javascript
   var httpRequest = new XMLHttpRequest();
   ~~~

2. **callback 함수를 만든다.**

   - 서버에서 response가 왔을 때 실행시키는 함수
   - HTML 페이지를 업데이트 한다.

   ~~~javascript
   httpRequest.onreadystatechange = alertContents;
   
   function alertContents() {
       if (httpRequest.readyState === XMLHttpRequest.DONE) {
         if (httpRequest.status === 200) {
           alert(httpRequest.responseText);
         } else {
           alert('request에 뭔가 문제가 있어요.');
         }
       }
     }
   })();
   ~~~

   - AJAX에 어떠한 변화가 일어났을 때, 이에 대응해서 일어나는 것이 바로 `onreadystatechange` 이다.(callback함수를 포함한다고 생각하면 된다.)
   - response가 돌아왔는지 아닌지를 추적하는 property가 `readyState`이다.
     - `XMLHttpRequest.DONE` 은 서버로부터 모든 응답을 받았으며 이를 처리할 준비가 되었다는 것을 뜻한다.

3. **Open a request**

   - 서버에서 response가 왔을 때 실행시키는 함수
   - 두 가지 정보를 브라우저로 넘긴다.
     - 브라우저가 request를 보내기 위해 사용할 method
     - requst가 갈 URL

   ~~~javascript
   httpRequest.open('GET', 'http://www.example.org/some.file', true);
   ~~~

   - 첫번째 파라미터 : http 요구방식
   - 두번째 파라미터 : 요구하고자하는 URL
   - 세번째 파라미터 : 요청을 비동기식으로 수행할지 결정
     - 기본값은 true이며, false로 설정할 경우 `send()` 함수에서 서버로부터 응답이 올 때까지 기다린다.

4. **send the request**

   ~~~javascript
   httpRequest.send();
   ~~~

   - send 메서드의 파라미는 서버에서 쉽게 parse할 수 있는 형식이어야한다.

- ex_)위의 내용을 합친 예제

  ~~~javascript
  <button id="ajaxButton" type="button">Make a request</button>
  
  <script>
  (function() {
    var httpRequest;
    document.getElementById("ajaxButton").addEventListener('click', makeRequest);
  
    function makeRequest() {
      httpRequest = new XMLHttpRequest();
  
      if(!httpRequest) {
        alert('XMLHTTP 인스턴스를 만들 수가 없어요 ㅠㅠ');
        return false;
      }
      httpRequest.onreadystatechange = alertContents;
      httpRequest.open('GET', 'test.html');
      httpRequest.send();
    }
  
    function alertContents() {
      if (httpRequest.readyState === XMLHttpRequest.DONE) {
        if (httpRequest.status === 200) {
          alert(httpRequest.responseText);
        } else {
          alert('request에 뭔가 문제가 있어요.');
        }
      }
    }
  })();
  </script>
  ~~~

<br>

:point_right: *필자는 꼭 중요하다고 생각되는 함수만들 담아왔다. 더 많은 내용이 궁금하다면 [여기](https://developer.mozilla.org/ko/docs/Web/Guide/AJAX/Getting_Started) 를 통해 얻을 수 있다.*

<BR>

## AJAX를 이용한 웹 응용 프로그램의 동작원리 

- Ajax의 동작은 Ajax 구성 요소들을 사용하여 이루어진다.

- Ajax vs 기존 웹

  <img src="http://www.tcpschool.com/lectures/img_ajax_ajax_application.png" width=310> <img src="http://www.tcpschool.com/lectures/img_ajax_other_application.png" width=350> 

  -  사용자에 의한 요청 이벤트가 발생
  - 요청 이벤트가 발생하면 이벤트 핸들러에 의해 자바스크립트가 호출
  - 자바스크립트는 XMLHttpRequest 객체를 사용하여 서버로 요청
    - 이때 웹 브라우저는 요청을 보내고 나서, 서버의 응답을 기다릴 필요 없이 다른 작업을 처리할 수 있다.
    - 하지만, open에서 false를 할 경우, 동기식이 되어 응답을 기다려야한다.
  - 서버는 전달받은 XMLHttpRequest 객체를 가지고 Ajax 요청을 처리
  - 서버는 처리한 결과를 HTML, XML 또는 JSON 형태의 데이터로 웹 브라우저에 전달
    - 이때 전달되는 응답은 새로운 페이지를 전부 보내는 것이 아니라 필요한 데이터만을 전달
  - 서버로부터 전달받은 데이터를 가지고 웹 페이지의 일부분만을 갱신하는 자바스크립트를 호출
  - 결과적으로 웹 페이지의 일부분만이 다시 로딩되어 표시

<br>

-----------------

**<참조>**

- [AJAX란 무엇인가?](https://velog.io/@surim014/AJAX%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)

- [Ajax 시작하기](https://developer.mozilla.org/ko/docs/Web/Guide/AJAX/Getting_Started)
- [Ajax 기초](http://www.tcpschool.com/ajax/ajax_intro_basic)
- [동일 출처 정책](https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy)