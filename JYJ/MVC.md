# MVC 패턴

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYoung-Kwon, Jeonghea Shin*

<hr>

- MVC 패턴이란?

  ​		Model, View, Contoller의 약자로, 소프트웨어 공학에서 사용되는 소프트웨어 <mark>디자인 패턴</mark>이다.

  <img src="resources/mvc.png" height="300px" align="center">

  ​		사용자가 Controller를 조작하면 Controller는 Model을 통해 데이터를 가져온다.

  ​		가져온 정보를 바탕으로 시각적인 표현을 담당하는 View를 제어해 사용자에게 전달한다.

  <br/>

  <br/>

- MVC 패턴의 구성


  - Model : 백 그라운드에서 동작하는 로직 처리를 담당한다.
  - View : 사용자가 보게될 결과 화면을 출력한다.
  - Controller : 사용자의 입력 처리와 흐름 제어를 담당한다.

  <br/>

- MVC 패턴의 특징

- 도메인 (비즈니스) 로직과 UI 로직을 분리하여 유지보수를 독립적으로 수행할 수 있게 한다.
  - 로직처리 모델과 출력 처리 모델이 분리되어 있어 개발자와 디자이너의 분업이 가능하다.

  <br/>

- MVC 패턴의 장단점

  - 장점
    - 유지보수의 용이성
    - 유연성과 확장성
    - 중복 코딩의 문제점 해소

  <br/>

  - 단점

    - 모델과 뷰의 완전한 분리가 어렵고, 그로 인해 구조가 복잡해질 수 있다.

    - 설계 시간이 많이 소요되며, 개발자 수준이 높아야 한다.

      <small>+) 한계 : MVC가 너무 복잡하고 비대해진 형태를 Massive View Controller라고 하며, 대안 방안으로 MVP 패턴이 존재한다.</small>

  <br/>


<br/>

## 예상질문❔

Q1) MVC 패턴이란 무엇인가?

A1) 소프트웨어 디자인 패턴 중 하나로, 모델과 뷰, 컨트롤러로 로직을 분리하여 개발한다.

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/KJY-01/KJY/%5BSW%5D%20MVC%20%ED%8C%A8%ED%84%B4.md
- https://github.com/fake-developers/1st/blob/SJH-01/SJH/MVC%20Pattern.md
