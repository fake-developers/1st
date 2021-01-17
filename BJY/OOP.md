## 객체 지향 프로그래밍 (Object Oriented Programming)

<br/>

### <u>객체 & 클래스</u>

`붕어빵과 붕어빵을 찍는 기계`

#### 객체

* 대상을 나타내는 단어

* 자신의 고유의 이름, 상태(state) 그리고 행동(behavior)을 갖는다.

  > 상태(속성, 특성)를  멤버변수라고 표현할 수 있고,
  >
  > 행동(기능)을 메소드 혹은 멤버함수라고 표현한다.

* ex) 사람 개인 한 명 한 명, 책 한 권 한 권

#### 클래스

* 객체의 상태와 행동을 어떻게 만들지를 결정한 청사진
* ex) 버튼이라는 객체의 다음으로 이동하는 행동과  상태등이 클래스에 정의 되어져있다.

~~~
인스턴스

클래스가 메모리에 생성된 상태. 클래스로부터 생성된 객체라고도 한다.
~~~

<br/>

### <u>객체지향 프로그래밍이란?</u>

객체의 관점에서 프로그래밍 하는 것을 의미한다.

객체들의 유기적인 관계를 통해서 프로세스가 진행이 된다. 즉, 애플리케이션을 구성하는 요소들을 객체로 바라보고, 객체들을 유기적으로 연결하여 프로그래밍 하는 것이다.

캡슐화, 다형성, 상속을 이용하여 코드 재사용을 증가시키고, 유지보수를 감소시키는 장점을 얻기 위해서 객체들을 연결 시켜 프로그래밍 하는 것이다.

![OOP](https://user-images.githubusercontent.com/61674527/104850421-512be480-5932-11eb-8c75-bf2a9791cd2e.jpg)



<br/>

### <u>객체지향 프로그래밍의 특징</u> 

#### <u>추상화(Abstraction)</u>

공통의 속성이나 기능을 묶어 이름을 붙이는 것

* 목적과 관련이 없는 부분을 제거하여 필요한 부분만을 표현하기 위한 개념이다.
* 객체 지향적 관점에서 클래스를 정의하는 것을 추상화라고 정의 내릴 수 있다.

> ex) 물고기, 사자, 토끼, 뱀이 있다고 하자.
>
> **물고기, 사자, 토끼, 뱀 → 객체**
>
> 이 객체들을 하나로 묶으려 할 때, 동물 또는 생물이라는 추상적인 객체로 크게 정의.
>
> **동물 or 생물로 묶는 것 → 추상화** 

#### <u>캡슐화(Encapsulation)</u>

데이터 구조와 데이터를 다루는 방법들을 결합시켜 묶는 것

* 변수와 함수를 하나로 묶는 것을 말한다.

* 무작정 묶는 것이 아니라 객체가 맡은 역할을 수행하기 위한 하나의 목적을 하나로 묶는 것이라고 생각해야한다.

* 정보은닉을 할 수 있는 장점이 있다.

  > 접근 제어자(public, protected, default, private)를 사용해 접근을 허용하지 않는 멤버들을 설정하여 정보 은닉을 구체화할 수 있다.
  >
  > | 접근 <br />제어자 | 같은 클래스의<br /> 멤버 | 같은 패키지의<br /> 멤버 | 자식 클래스의<br /> 멤버 | 그 외의 <br />영역 |
  > | :---------------: | :----------------------: | :----------------------: | :----------------------: | :----------------: |
  > |      public       |            O             |            O             |            O             |         O          |
  > |     protected     |            O             |            O             |            O             |         X          |
  > |      default      |            O             |            O             |            X             |         X          |
  > |      private      |            O             |            X             |            X             |         X          |

#### <u>상속(Inheritance)</u>

상위 개념의 특징을 하위 개념이 물려받는 것

* 코드의 중복을 줄일 수 있다.

  상속의 관계를 맺으면 자식 객체를 생성할 때 부모 클래스의 속성들을 자동으로 물려받기 때문에 자식 클래스에서 정의 할 필요가 없다.

> ex) 포유류라는 클래스는 고양이와 강아지 클래스에 속성들을 물려준다.
>
> 고양이 클래스, 강아지 클래스 → 자식 클래스
>
> 포유류 → 부모 클래스

#### <u>다형성(Polymorphism)</u>

형태가 같지데 다른 기능을 하는 것

* 부모클래스에서 물려받은 가상 함수를 자식 클래스 내에서 오버라이딩 되어 사용된다.
* 같은 이름의 속성을 유지함으로서, 속성을 사용하기 위한 인터페이스를 유지하고, 메서드 이름을 낭비하지 않을 수 있다.

~~~
오버라이딩

상위 클래스가 가지고 있는 메소드를 하위 클래스가 재정의해서 사용하는 것
~~~

> ex) 고양이 클래스에 "울음"이라는 속성이 정의 되어있다고 하자.
>
> 사자는 고양이 과이므로 사자 클래스는 고양이 클래스를 상속받는다. 
> → "울음"이라는 속성이 자동으로 추가된다.
>
> 사자 울음소리와 고양이 울음소리는 다르다. 
>
> 그래서 사자 클래스에서 상속받은 "울음"속성을 사자 울음소리에 맞게 재정의 

<br/>

### <u>객체지향 프로그래밍의 장점</u>

#### 장점

* **재사용성**

  상속을 통해 프로그래밍시 코드에 재사용을 높일 수 있음.

* **생산성 향상**

  잘 설계된 클래스를 만들어서 독립적인 객체를 사용함으로써 개발의 생산성을 향상시킬 수 있음.

* **자연적인 모델링**

  우리 일상생활의 모습의 구조가 객체에 자연스럽게 녹아들어 있기 때문에 생각하고 있는 것을 그대로 자연스럽게 구현할 수 있다.

* **유지보수의 우수성**

  프로그램 수정시 추가, 수정을 하더라도 캡슐화를 통해 주변 영향이 적기 때문에 유지보수가 쉬워서 매우 경제적이라 할 수 있다.

#### 단점

* **개발 속도가 느림**
  객체가 처리하려는 것에 대한 정확한 이해가 필요하기 때문에 설계단계부터 많은 시간이 소모된다.

* **실행속도가 느림**

  객체지향언어는 대체적으로 실행속도가 느리다.

* **코딩난이도 상승**

  다중 상속이 지원되는 C++같은 경우에 너무 복잡해져 코딩의 난이도가 상승할 수 있다.

<br/>

<br/>

<br/>

### REFERENCE

* [OOP](https://victorydntmd.tistory.com/117)

* [OOP(2)](https://vandbt.tistory.com/10)

* [OOP(3)](https://88240.tistory.com/228)

* [OOP(4)](https://radait.tistory.com/4)

* [클래스와 객체](https://velog.io/@shchoice/java-oop-2) 

* [클래스와 객체(2)](https://gmlwjd9405.github.io/2018/09/17/class-object-instance.html)

* [접근제어자](http://www.tcpschool.com/java/java_modifier_accessModifier)

* [오버라이딩](https://hyeonstorage.tistory.com/185)

  
