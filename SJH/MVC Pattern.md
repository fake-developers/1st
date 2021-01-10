# MVC 패턴

- #### 들어가기 앞서

  - 디자인 패턴이란?? 

    - 프로그램 개발에서 자주 나타나는 문제를 해결하는 방식을 이름을 붙여서 재이용하기 좋은 형태로 정리해둔 것

- #### MVC 패턴이 뭘까?

  - 소프트웨어 공학에서 사용되는 소프트웨어 디자인 패턴 중 하나

  - 애플리케이션을 Model, View, Controller 세 가지의 역할로 구분한 개발 방법론

    <hr>

    ![mvc](C:\Users\jungh\OneDrive\바탕 화면\1st\SJH\img\mvcpattern.PNG)

  - **model**

    : 뷰에 필요한 비지니스(도메인) 영역의 로직을 처리

    : DTO, DAO로 분류 가능

    ~~~
    DTO(Data Transfer Object) = VO(Value Object)
    계층간 데이터 교환을 위한 자바빈즈.
    DAO(Data Access Object)
    데이터베이스의 데이터에 접근하기 위해 생성하는 객체.
    데이터베이스에 접근하기 위한 로직과 비즈니스 로직을 분리하기 위해 사용함.
    ~~~

  - **view**

    : 비지니스 영역에 대한 결과 화면 담당

    : 도메인의 상태를 따로 저장하고 관리하는 클래스 변수 또는 인스턴스 변수가 있을 필요 없음

  - **controller**

    : 사용자의 입력 처리와 화면의 흐름 제어(model과 view에 간섭한다.)

- #### MVC 패턴의 특징

  - 로직을 처리하는 모델과 출력을 처리하는 뷰가 분리되어 있다.
  - 즉, 개발자와 디자이너의 분업이 가능하다.
  - 주로 대형 프로젝트에서 쓰인다.

- #### MVC 패턴의 장점과 단점

  - 장점 :

    1. 유지보수가 쉽다.
    2. 유연하고 확장하기 쉽다.
    3. 중복코딩의 문제점 또한 사라지게 된다.

  - 단점 :

    1. model과 view의 완전한 분리가 어렵다.
       - model 과 view의 의존성이 완전히 분리될 수 없기때문에, 구조가 복잡해 질 수 있다.
    2. 설계시간이 많이 소요되며, 개발자 수준이 높아야 한다.

    `+` MVC가 너무 복잡하고 비대해질 경우의 형태를 Massive ViewController라고 부른다.(MVC의 한계를 표현)

  => 대안방안으로 MVP 패턴이 존재한다. 


------------

##### <추가 자료>

- MVC와 비교했을 때 MVP가 좋은 점
  - MVP는 View와 Model을 완전히 분리하고, Presenter가 서로 간의 상호작용을 해줌으로써 서로의 영향을 최소화 시킨다.

</br>

##### <참조>

- <https://ko.wikipedia.org/wiki/%EB%AA%A8%EB%8D%B8-%EB%B7%B0-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC>
- <https://bomb0730.tistory.com/19>
- https://velog.io/@ljinsk3/MVC-%ED%8C%A8%ED%84%B4
- <https://coding-factory.tistory.com/69>
- <https://beomy.tistory.com/43>

