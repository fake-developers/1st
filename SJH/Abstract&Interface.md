# 추상클래스(Abstract)와 인터페이스(Interface)

<br>

***추상 클래스와 인터페이스는 상속받는 클래스 혹은 구현하는 인터페이스 안에 있는 추상 메소드를 구현하도록 강제한다.***

<br>

### 추상 클래스(Abstract)

- 미완성된 클래스

- 클래스 구현부 내부에 추상 메소드가 하나이상 포함되거나 abstract로 정의된 클래스

- 클래스의 프레임만 구성되어 있다.

- 직접 객체 생성이 불가능하다.
  
  - 즉, 인스턴스를 생성할 수 없다.
  
- 추상 클래스에서 정의된 추상적인 기능은 하위 클래스에서 상세 구현한다.

- #### 추상 클래스의 목적

  - 동일한 부모를 가지는 클래스를 묶는 개념으로 **상속을 받아서 기능을 이용하고, 확장시키는 것이다.**
  - 새로운 클래스를 작성하는데 있어서 그 바탕이 되는 부모 클래스로서 중요한 의미를 갖는다.
  
- #### 추상 클래스 상속

  - **단일 상속만 가능**

  - ex_)

    <img src="https://user-images.githubusercontent.com/58902042/106489074-b9b0bf00-64f7-11eb-8ea3-ec5892b3723d.PNG" height=110> 
    - Animal 추상 클래스

    <img src="https://user-images.githubusercontent.com/58902042/106489130-c6cdae00-64f7-11eb-94cc-6994faff6fd9.PNG" height=120><img src="https://user-images.githubusercontent.com/58902042/106489607-4eb3b800-64f8-11eb-9600-c76ad9871cd1.PNG" height=120>

    - Animal 추상 클래스를 상속받는 Dog, Cat 클래스
      

    <img src="https://user-images.githubusercontent.com/58902042/106489611-4f4c4e80-64f8-11eb-98dd-0e9dcdc0971e.PNG" height=200> 

    - 선언 후, 메인 메서드에서 실행

  

  :bulb: *추상 클래스를 상속 받는 클래스는 추상 클래스에서 선언했던 추상 메서드를 반드시 구현해야 한다.  그렇지 않으면 에러가 발생한다.*

<br>

### 인터페이스(Interface)

- 밑 그림만 있는 기본 설계도 즉, 뼝대

- 추상 클래스보다 한 단계 더 추상화 되었다고 볼 수 있다.
  - 안의 모든 메서드가 추상 메서드로 되어있다.
  - 자바8에서는 default 키워드를 이용해서 일반 메소드의 구현도 가능은 함

- 추상 클래스와 마찬가지로 직접 객체 생성이 불가능하다.

- 미리 정해진 규칙에 맞게 구현하도록 표준을 제시하는데 사용된다.

- 인터페이스끼리 다중 상속 가능

- #### 인터페이스의 목적

  - 함수의 구현을 강제화하여, **구현 객체가 같은 동작을 한다는 것**을 보장하는 것이다.
  
- #### 인터페이스 제약사항

  - 모든 멤버변수는 `public static final`이어야 한다. 단, 이는 생략 가능
  - 모든 메서드는 `public abstract` 여야 한다. 단, 이는 생략 가능
    - static 메서드와 default 메서드는 제외(Java 8 이후)

- #### 인터페이스 상속

  - **다중 상속 가능**

  - ex_)
  
    <img src="https://user-images.githubusercontent.com/58902042/106490421-27a9b600-64f9-11eb-8d87-afe99013d31c.PNG" height=180>
  
    - 부모 인터페이스(Changeable, Powerable)을 모두 상속받는 자식 인터페이스(Controlable)
    - Controlable 안에 정의된 멤버는 하나도 없지만 부모로부터 상속받은 추상메서드 change, power를 멤버로 갖게 된다.
  
    <img src="https://user-images.githubusercontent.com/58902042/106491041-cafacb00-64f9-11eb-8291-39f830d04a6e.PNG" height=140>
  
    - Controlable 인터페이스를 구현하는 Control 클래스
    - 만일 구현하는 인터페이스의 메서드 중 일부만 구현한다면 abstract를 붙여 추상클래스로 선언해야 한다.
  
    <img src="https://user-images.githubusercontent.com/58902042/106491096-dd750480-64f9-11eb-8b95-c5ba74edb8af.PNG" height=70> 
  
    - 상속과 구현을 동시에 할 수도 있다.
  
- #### 인터페이스 장점

  **1. 개발시간을 단축시킬 수 있다.**

  - 일단 인터페이스가 작성되면, 이를 사용하여 프로그램을 작성하는 것이 가능. 
     - 인터페이스가 공통이므로 동시 개발 가능

  **2. 표준화가 가능하다.**

  - 프로젝트에 사용되는 기본 틀을 인터페이스로 작성한 후 개발되도록 한다.
   - 일관되고 정형화된 프로그램 개발 가능

  **3. 서로 관계없는 클래스들에게 관계를 맺어 줄 수 있다.**

  - 하나의 인터페이스를 공통적으로 구현함으로써 관계 매핑

  **4. 독립적인 프로그래밍이 가능하다.**

     - 클래스의 선언과 구현을 분리시킬 수 있다.
  - 클래스와 클래스 간의 직접적인 관계를 인터페이스를 이용해서 간접적인 관계로 변경하면, 한 클래스의 변경이 관련된 다른 클래스에 영향을 미치지 않는 독립적인 프로그래밍이 가능하다.

- #### 인터페이스의 이해

  <img src="https://user-images.githubusercontent.com/58902042/106575411-671ae580-657f-11eb-9f26-535511b448ae.PNG" height=280>

  - 실행 결과 : <img src="https://user-images.githubusercontent.com/58902042/106575815-d7296b80-657f-11eb-9bef-b7d0b856f3bc.PNG" height=25> 

  - 위의 코드와 같이  Class A와 Class B가 있다고 할때, Class A는 Class B의 인스턴스를 생성하고 메서드를 호출한다.

    <img src="https://user-images.githubusercontent.com/58902042/106576131-2b345000-6580-11eb-9475-807d4e8b6ca9.PNG" height=100> 

  - 이 두 클래스는 서로 직접적인 관계를 가지게 된다.
  - Class A를 작성하려면 Class B가 이미 작성되어 있어야 하고, Class B의 methodB()의 선언부가 변경되면 이를 사용하는 Class A도 변경되어야하는 단점이 있다.

  <img src="https://user-images.githubusercontent.com/58902042/106575510-844fb400-657f-11eb-95e9-cc738b764efe.PNG" height=280 width=700>

  - 실행 결과 : <img src="https://user-images.githubusercontent.com/58902042/106576812-e826ac80-6580-11eb-8024-181c29b31f8b.PNG" height=25>

  - 이때 위와 같이 인터페이스를 매개체로 해서 Class A가 인터페이스를 통해 Class B의 메서드에 접근하도록 만들면 Class B가 변경되거나 다른 클래스로 대체되어도 Class A는 전형 영향을 받지 않는다.

    <img src="https://user-images.githubusercontent.com/58902042/106576615-b57cb400-6580-11eb-9c7c-f3f9335173c8.PNG" height=150> 

  - 이제 Class A가 Class B를 사용하지 않는다.

  - 따라서 인터페이스를 통해서만 연결된느 간접적인 관계로 바뀌었다.

    <img src="https://user-images.githubusercontent.com/58902042/106576618-b6ade100-6580-11eb-9f38-3dd57212d0ca.PNG" height=150> 

  - 인터페이스 I 는 실제 구현 내용을 감싸고 있는 껍데기이며, Class A는 껍데기 안에 어떤 알맹이(Class)가 있는지 몰라도 된다.

<br>

### 클래스와 인터페이스 사이 관계

<img src="https://user-images.githubusercontent.com/58902042/106485793-540f0380-64f4-11eb-83c0-dfc8166cbc6e.PNG" height= 180>

- **extends** : 같은 클래스, 인터페이스끼리 상속 받을 때
- **implements** : 클래스가 인터페이스를 구현 할 때
- 인터페이스는 인터페이스로만 상속 받을 수 있다.

<br>

### 추상 클래스 vs 인터페이스 

- #### 공통점
  1. 선언만 있고 구현 내용은 없는 클래스
  2. 인스턴스화 할 수 없다.
  3. 추상클래스를 extends로 상속받은 자식들과 인터페이스를 implements하고 구현한 자식들만 객체를 생성할 수 있다.
     - 즉, 자식들이 반드시 무언가를 구현하도록 위임할 때 사용된다.

- #### 차이점

  1. 인터페이스는 클래스가 아니지만 추상 클래스는 클래스이다.
  2. 인터페이스는 다중상속이 가능하고, 추상 클래스는 단일상속만 한다.
  3. 추상클래스는 상속을 받아 기능을 확장 즉, 부모의 유전자를 물려받는다.(IS-A) 인터페이스는 구현하는 모든 클래스에 대해 특정한 메서드가 반드시 존재하도록 강제하는 역할(유전자가 아니라 사교적으로 필요에 따라 결합하는 관계)

<br>

| 구분      | 추상 클래스                                                  | 인터페이스                                                   |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 선언      | abstract class 클래스명 {   변수;   메서드() {...}   abstract 메서드(); } | interface 인터페이스명 {    상수;    // public final static    메서드(); // public abstract } |
| 상속구현  | class Sub **extends** super {   메서드 재정의 // overriding } | class Sub **implements** Interface1, Interface2 {   메서드 재정의 // overriding } |
| 상속 특징 | 단일 상속                                                    | 다중 상속                                                    |





------

**<참조>**

- https://cbw1030.tistory.com/47

- https://you9010.tistory.com/155

- https://pridiot.tistory.com/50
- https://loustler.io/languages/oop_interface_and_abstract_class/

- https://brunch.co.kr/@kd4/6