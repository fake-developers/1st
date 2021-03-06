## MVC 패턴



### <u>MVC란?</u>

소프트웨어 공학에서 사용되는 소프트웨어 디자인 패턴이다. 
애플리케이션을 Model,View,Controller 세가지의 역할로 구분한 개발 방법론이다.

~~~
디자인 패턴

프로그램 개발에서 자주 나타나는 문제를 해결하는 방식을 이름을 붙여서 재이용하기 좋은 형태로 정리해둔 것
~~~

![mvc](https://user-images.githubusercontent.com/61674527/104108682-ff6bd480-5309-11eb-85eb-741af4d77229.jpg)



### <u>MVC패턴의 특징</u> 

- 로직을 처리하는 모델과 출력을 처리하는 뷰가 분리되어 있다.
- 즉, 개발자와 디자이너의 분업이 가능하다.
- 주로 대형 프로젝트에서 쓰인다.



### <u>MVC패턴 구성</u>

#### <u>Model</u> 

- 프로그램이 목표하는 작업을 원활하게 수행하기 위해 필요한 물리적 개체, 규칙, 작업 등의 요소들을 구분되는 역할로써 정의해놓은 것
- 뷰에 필요한 비지니스(도메인) 영역의 로직을 처리
- DTO, DAO로 분류할 수 있음
- 데이터를 가진 객체, 파라미터로 주로 쓰임
- DB의 테이블과 대응하는 경우가 많다.

~~~
DTO(Data Transfer Object) = VO(Value Object)
계층간 데이터 교환을 위한 자바빈즈.
DAO(Data Access Object)
데이터베이스의 데이터에 접근하기 위해 생성하는 객체.
데이터베이스에 접근하기 위한 로직과 비즈니스 로직을 분리하기 위해 사용함.
~~~

***

#### <u>View</u>

- 비지니스 영역에 대한 결과 화면 담당
- 객체를 전달받아 상태를 바로 출력하는 역할만을 담당 (도메인 로직의 어떤 것도 알고있으면 안됨)
- View에서는 도메인 객체의 상태를 따로 저장하고 관리하는 클래스 변수 / 인스턴스 변수가 있을 필요가 없다.

***

#### <u>Controller</u>

- 사용자의 입력 처리와 화면의 흐름 제어(model과 view에 간섭한다.) 
  즉 model과 view를 연결시켜주는 다리 역할
- 도메인 객체들의 조합을  통해 프로그램의 작동 순서나 방식을 제어
- 사용자가 접근한 URL에 따라 사용자 요청사항을 파악한 후, 그 요청에 맞는 데이터를 Model에 의뢰하고, 데이터를 View에 반영해 사용자에게 알려준다.



### <u>MVC패턴의 장단점</u> 

* #### 장점

1. 유지보수가 쉽다.
2. 유연하고 확장하기 쉽다.
3. 중복 코딩의 문제점 또한 사라지게 된다.

* #### 단점

1. model과 view의 완전한 분리가 어렵다.
   - model과 view의 의존성이 완전히 분리될 수 없기 때문에, 구조가 복잡해 질 수 있다.
   - Controller에 다수의 Model과 View가 연결되는 복잡한 상황이 유발 되는 상황이 생길 수 있음
   - Massive View Controller (MVC가 너무 복잡하고 비대해질 경우의 형태) 
2. 설계시간이 많이 소요되며, 개발자 수준이 높아야 한다.

~~~
MVP패턴

MVC패턴의 Massive View Controller의 대안방안.
MVP는 View와 Model을 완전히 분리하고, Presenter가 서로 간의 상호작용을 해줌으로써 서로의 영향을 최소화 시킨다.
~~~







### REFERENCE

* https://github.com/fake-developers/1st/blob/KJY-01/KJY/%5BSW%5D%20MVC%20%ED%8C%A8%ED%84%B4.md
* https://github.com/fake-developers/1st/blob/SJH-01/SJH/MVC%20Pattern.md

