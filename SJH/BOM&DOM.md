
# BOM과 DOM

- #### 들어가기 앞서
  - Object Model 이란?
  	- 웹 브라우저의 구성요소들은 객체화되어 있다. 
  	- 이 객체들 제어하여 웹 브라우저를 제어할 수 있고, 서로 계층적인 관계로 구조화 되어있다.
  	- Object Model은 크게 DOM, BOM으로 분류할 수 있다.
      <br/>

- #### 정의
  - **BOM**
  	
  	- Browser Object Model
  	- 브라우저와 관련된 내용들 <small>(ex. 즐겨찾기, 기록, URL 정보 등)</small>, 즉 객체들의 집합을 BOM이라고 한다.
  	
  - **DOM**

    - Document Object Model
    - 브라우저가 웹 문서를 이해할 수 있도록 트리구조로 구성한 것이다.
	  - **DOM의 종류**
      - W3C DOM 표준은 세가지 모델로 구문된다.
        - Core DOM : 모든 문서 타입을 위한 DOM 모델
        - HTML DOM : HTML 문서 타입을 위한 DOM 모델
        - XML DOM: XML 문서 타입을 위한 DOM 모델
    - 문서 (열려있는 페이지)에 대한 모든 정보를 객체화 시켜 관리한다.
        ex. body 내부에 img 요소 등
    
    ![DOM](https://user-images.githubusercontent.com/61674527/103727230-2088a880-501e-11eb-8df2-8e9e4d752913.jpg){:height="100" weight="50"}
    
    
  
  <br/>
  
- #### 역할

  - **BOM**
  	- 웹 브라우저 창을 관리할 목적으로 제공되는 객체 모음을 대상으로 하는 모델로, 자바스크립트 등에서 사용 가능하다.
  	- window 객체를 통해 접근할 수 있다.
  	
  	- window 객체 모델
  	  - navigator object : 브라우저명과 버전 정보를 속성으로 가진다.
  	  - window object: 최상위 객체로, 각 프레임별 하나씩 존재한다.
  	  - document object: 현재 문서에 대한 정보이다.
  	  - location object: 현재 URL에 대 한 정보로 브라우저에서 사용자가 요청하는 URL이다.
  	  - history object: 현재의 브라우저가 접근했던 URL history를 보여준다.
  	  - screen object: 브라우저의 외부 환경에 대한 정보를 제공한다.
  	
  - **DOM**
  - html, xml 문서의 프로그래밍 인터페이스로 문서와 문서의 요소(element)에 접근하기 위해 사용된다.
    - 문서 구조, 스타일, 내용 등<small>(html이나 css의 내용)</small>을 변경할 수 있도록 태그(요소)들을 제어한다.

<br/>

<참조>

- <https://github.com/fake-developers/1st/blob/JYJ-01/JYJ/BOMandDOM.md>
- <https://github.com/fake-developers/1st/blob/BJY-01/BJY/BOM%26DOM.md>
