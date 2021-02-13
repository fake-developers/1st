# 업캐스팅 & 다운캐스팅

### 들어가기 앞서

- **캐스팅**이란?
  - 타입을 변환하는 것을 말하며 **형변환**이라고도 한다.
  - 데이터 손실을 막기 위해 다형성을 지켜주는 것
  - 자바의 상속 관계에 있는 부모와 자식 클래스 간에는 서로의 형변환이 가능하다.

<br>

### 업캐스팅(Upcasting)

- **서브 클래스의 객체가 수퍼 클래스 타입으로 형변환** 되는 것

- 자바에서 서블 클래스는 수퍼 클래스의 속성을 상속 받기 때문에

  - 서브 클래스의 객체는 수퍼 클래스의 멤버를 모두 가진다.
  - 따라서, 서브 클래스는 수퍼 클래스로 취급될 수 있다.

- 수퍼 클래스의 레퍼런스 변수가 서브 클래스로 객체화 된 인스턴스를 가리킬 수 있게 된다.

  ![upcasting](https://user-images.githubusercontent.com/61674527/104850375-1629b100-5932-11eb-9b74-91422ffb3713.jpg)

  >- 업캐스팅을 하게되면 Student Class의 수퍼 클래스인 Person Class의 멤버에만 접근가능하다.
  >- 업캐스팅 시에는 **명시적인 타입 캐스팅을 선언하지 않아**도 된다.

- 업캐스팅을 사용하는 이유

  - 관련 서브 클래스들을 한번에 관리할 수 있어 용이하다.
    - 수퍼 클래스에 멤버변수나 메소드를 한번만 작성해놓으면 상속 받은 클래스들이 동일하게 이용 가능하다.

<br>

### 다운 캐스팅(Downcasting)

- 자신의 고유한 특성을 잃은 서브 클래스의 객체를 다시 복구 시켜주는 것

- 업캐스팅 된 것을 다시 원상태로 돌려놓는 것

  ![downcasting](https://user-images.githubusercontent.com/61674527/104850851-d617fd80-5934-11eb-8239-80a317baf3a8.jpg)

  >- **업캐스팅이 선행**되어야 한다.
  >- 업캐스팅과 달리 **명시적으로 타입을 지정**해야 한다.
  >
  >- 무분별한 다운캐스팅은 컴파일 시점에는 오류가 발생하지 않아도 런타임 오류를 발생시킬 가능성이 있다.

<br>

### instanceof

- 다운캐스팅을 할 때, 어떤 객체의 타입인지 구분하기 위해 사용하는 연산자

- instanceof 연산자의 형태

   <img src="https://user-images.githubusercontent.com/58902042/105578408-45716f80-5dc3-11eb-9732-a1b57e0864a4.PNG" height=100>

- instanceof 연산자의 결과 값은 boolean 타입으로 true, false를 반환 값으로 가진다.

- 업캐스팅 했을 때 레퍼런스 변수가 가르키는 객체의 타입이 어떤 것인지 구분하기 어려울 때 유용하다.

- ex_)

  ~~~java
  class Unit {
      ...
  }
  
  class Zelot extends Unit {
      ...
  }
  
  class Marine extends Unit {
      ...
  }
  
  class Zergling extends Unit {
      ...
  }
  
  public class CastingTest {
      public static void main(String[] args) {
          Unit unit;
          unit = new Unit();
          unit = new Zealot(); // 업캐스팅
          unit = new Marine(); // 업캐스팅
          unit = new Zergling(); // 업캐스팅
          
            if(unit1 instanceof Unit) { // true
              system.out.println("Unit 타입")
          }
          
          if(unit1 instanceof Zealot) { // false
         	 	system.out.println("Zealot 타입")
          }	
          
          if(unit2 instanceof Zergling) { // false
         	 	system.out.println("Zergling 타입")
          }	
          
          if(unit3 instanceof Marine) { // true
         	 	system.out.println("Marine 타입")
          }	
          
          if(unit4 instanceof Zergling) { // true
              system.out.println("Zergling 타입")
          }
      }
  }
  ~~~

  >- 위 코드의 서브클래스들은 모두 Unit 클래스를 상속받고 있어 컴파일 오류 없이 정상적으로 수행된다.
  >- 만약 Unit 레퍼런스 변수가 어떤 객체를 가리키고 있다고 가정할 때, 가리키는 객체의 실제 타입을 구분할 때 instanceof 를 사용한다.
  >- 사용시 주의할 점
  > - instanceof 연산자는 객체에 대한 클래스 타입에만 사용할 수 있다.
  
- 다운캐스팅 사용하는 이유

   - 업캐스팅을 통한 하나의 집합에 여러 타입의 객체를 관리하는 것은 편하나 각자 고유기능에 접근할 수 없으므로, 다운캐스팅을 사용하여 고유기능을 사용하게 한다.

<br>

------

### 예상질문

>  **업캐스팅과 다운캐스팅을 하는 이유**를 설명하시오.
>
> - 수퍼 클래스에서 파생된 관련 서브 클래스들을 관리하기 용이하기 때문에 사용한다. 그러나, 업캐스팅을 할 경우 파생된 서브 클래스들 고유기능에 접근할 수 없으므로 다운 캐스팅을 한다.

> **instanceof의 사용 목적**은 무엇인가?
>
> - 업캐스팅 했을 때 레퍼런스 변수가 가르키는 객체의 타입이 어떤 것인지 구분하기 위해서 사용한다.

> 다운 캐스팅에서 명시적으로 타입을 지정해야하는 이유는?
>
> - int와 double관계와 비슷한 경우로, int에서 double은 묵시적이지만 double에서 int는 명시적으로 강제 형변환을 해주어야 한다. 다운캐스팅은 타입이 높은 쪽에서 낮은 쪽으로 변경되는 것이기 때문에 데이터가 손상되어도 괜찮은지 JVM이 판단하기 힘드므로 개발자가 직접 표시를 해줘야 한다.

-------

**<참조>**

- [자바 #24 업캐스팅과 다운캐스팅](https://sas-study.tistory.com/62)
- [업캐스팅과 다운캐스팅](https://m.blog.naver.com/PostView.nhn?blogId=goddlaek&logNo=220888538277&proxyReferer=https:%2F%2Fwww.google.com%2F)
- https://github.com/fake-developers/1st/blob/BJY-03/BJY/Upcasting%26Downcasting.md
- https://github.com/fake-developers/1st/blob/JYJ-03/JYJ/JavaCasting.md