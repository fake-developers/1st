# CSR과 SSR의 차이

- #### 들어가기 앞서

  - 렌더링이란 무엇인가?

    - 서버로 부터 HTML 파일을 받아 브라우저에 뿌려주는 과정

    <br>

- #### 개념

  - **CSR이란?**

    - Client Side Rendering 
    - 최초에 서버에서 한 번  관련파일을 모두 로딩한 후, 사용자의 요청이 올 때마다 리소스를 서버에 제공하여 클라이언트가 해석하고 렌더링 하는 방식
    - SPA개발에 쉬운 Angular JS, Backbone JS와 같은 JS 프레임워크가 등장 + 이 후 클라이언트가 무거워지자 view만 관리하는 React JS 등장

    ![CSR](https://user-images.githubusercontent.com/58902042/103725584-414eff00-501a-11eb-98ee-3a7a9f1f6ae7.PNG)

  - **SSR이란?**
    
    - Server Side Rendering 
    - 요청시마다 새로고침이 일어나며 서버에 새로운 페이지에 대한 요청을 하는 방식
    
    ![SSR](https://user-images.githubusercontent.com/58902042/103725615-59268300-501a-11eb-97cd-2db4c78cd095.PNG)

  <br>

- #### 초기 렌더링 속도
  
    - CSR 
      -  페이지, JS, 각종 리소스를 다운 받은 후 브라우져에서 렌더링 하기 때문에 **초기 로딩이 느리다.**
    - SSR 
      -  View를 서버에서 렌더링 하기 때문에 **초기 로딩이 짧다.**
    
- #### 인터랙션(상호작용)
  
    - CSR 
      - 초기에 모든 파일을 받아왔기 때문에 클라이언트의 행동에 따라 필요한 부분만 다시 읽어들이므로 **빠른 인터랙션이 가능**하다.
    - SSR 
      - 모든 요청에 관해 전체 페이지를 렌더링하기 때문에 **인터랙션이 느리다.**
    
- #### SEO(검색 엔진 최적화)
  
    - CSR 
      -  View를 생성하기 위해 자바스크립트를 통해 동적 렌더링하는 CSR방식
      - 대부분의 웹 크롤러, 봇이 자바스크립트를 크롤링하지 못하기 때문에 HTML에서 만 컨텐츠를 수행하여 HTML을 빈 페이지로 인식하여 **SEO 사용 불가능**
    - SSR 
      -   view를 서버에서 전부 렌더링하여 HTML에 모든 컨텐츠가 저장되어 있기 때문에 **SEO 사용 가능**
    
- #### 보안

    - CSR 
      - **쿠키**에 사용자 정보를 저장
    - SSR
      - 서버 측에서 **세션**으로 사용자 정보 관리

<br>

------------------------------------

##### <관련정보>

- SPA 
  -  서버로부터 처음에만 페이지를 받아오고 이후 동적으로 페이지를 구성해서 새로운 페이지를 받아오지 않는 웹 어플리케이션
  - 단 하나의 HTML파일을 기반으로 JS를 이용해 동적으로 화면을 바꾸는 방식의 웹 어플리케이션
  - SPA에서 CSR으로 렌더링 하는 방식 사용(SPA!=CSR)
- MPA 
  -  서버로부터 완전한 페이지를 받아오고 이후에 데이터를 수정하거나 조회하는 새로운 요청이 있을 경우, 완전한 페이지를 다시 받아오는 웹 어플리케이션
  - 화면마다  HTML파일 존재, 사용자가 그 화면을 요청할 때마다, 웹 서버가 필요한 데이터와 HTML로 파싱해서 보여주는 방식의 웹어플리케이션
  - MPA에서 SSR으로 렌더링 하는 방식 사용(MPA!=SSR)

<br>

------------------------------------

###### <참조>

<br>

- <https://velog.io/@namezin/CSR-SSR>
- <https://kim-mj.tistory.com/275>
- <https://goodgid.github.io/Server-Side-Rendering-and-Client-Side-Rendering/>
- <https://brownbears.tistory.com/411>
- <https://medium.com/%EC%95%84%EB%AA%BD%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4/csr-ssr-spa-mpa-ede7b55c5f6f>
- <https://kyj7337.github.io/posts/SSRCSR>

