# Singleton Pattern

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYoung Kwon*

<hr>

- 싱글톤 패턴이란?

  
  - 애플리케이션이 시작될 때 클래스가 <mark>최초 한번만</mark> 메모리를 할당하고(static) 그 메모리에 인스턴스를 만들어 사용하는 디자인 패턴이다.
  - 생성자가 여러 차례 호출되어도 실제로 생성되는 객체는 하나이고, 최초 생성 이후에 호출된 생성자는 최초에 생성한 객체를 반환한다.
  - 자바에서는 생성자를 private로 선언하여 생성 불가능하게 하고 getInstance()로 받아서 쓰도록 한다.
  - <b>즉, 싱글톤 패턴은 단 하나의 인스턴스를 생성해 사용하는 디자인 패턴이다. </b>
    <small>+) 인스턴스가 필요하면 똑같은 인스턴스를 만들어내는게 아니라 기존 인스턴스를 사용하는 것</small>
  
  <br/>
  
- 싱글톤 패턴의 구현

  ```Java
  public class SingleObj {
      // 외부에 제공할 자기 자신의 인스턴스
      private static SingleObj singleObj = null;
      // 외부에서 직접 생성하지 못하도록 private로 생성자 선언
      private SingleObj(){}
      // 오직 1개의 객체만 생성하여 자신의 인스턴스를 외부에 제공
      public static SingleObj getInstance(){
          if(singleObj == null) {
              // SingleObj 인스턴스 생성
              singleObj = new SingleObj();
          }
          return singleObj;
      }
  }
  ```

  - 외부에서 객체를 생성할 수 없도록 생성자는 private으로 선언한다.
  - 외부에서 미리 생성된 자신의 인스턴스를 반환할 수 있도록 getInstance() 메서드를 정의한다.
  - getInstance() 메서드에서 클래스가 정의될 수 있도록 static 제어자를 사용한다.
  - static 메서드 / static 변수
    - 구체적인 인스턴스에 속하는 영역이 아니고 클래스 자체에 속한다.
    - 클래스의 인스턴스를 통하지 않아도 메서드를 실행할 수 있고, 변수를 참조할 수 있다.

    - getInstance() 메서드 호출 시
      - singleObj 변수에 객체가 할당되어있지 않으면 새로운 객체를 생성한다.
      - 이미 존재하면 그것을 반환한다.

<br/>


- 싱글톤 패턴을 사용하는 이유
  
  - 메모리 낭비 방지
    - 고정 메모리 영역을 얻으면서 한번의 new로 인스턴스를 사용하기 때문에 메모리가 낭비되지 않는다.
  - 데이터 공유
    - 싱글톤으로 만들어진 클래스의 인스턴스는 전역 인스턴스이기 때문에 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다.
  - 성능
    - 두 번째 이용 시부터 객체 로딩 시간이 현저히 출어 성능이 좋아진다.
  
  <br/>
  
- 싱글톤 패턴의 문제점
  
  
  - 프로그램 전체에서 하나의 객체만 공통으로 사용하기 때문에, 각 객체 간의 결합도가 높아질 수 있다.
  
  - 결합도가 높아지면 참조하는 모든 값들이 변경되어야 하기 때문에 수정과 테스트가 어려워진다.
  
  - 멀티 쓰레드 환경에서 동기화 처리를 하지 않으면 인스턴스가 중복 생성되는 경우도 발생할 수 있다.
  
  
    - 경합 조건 (Rare Condition)
  
      > 메모리와 같은 동일한 자원을 2개 이상의 쓰레드가 이용하려고 경합하는 현상
  
    - 경합 조건을 발생시키는 경우
  
      1. SingleObj 인스턴스가 아직 생성되지 않았을 떄, 쓰레드 1이 getInstance 메서드의 if 문을 실행해 이미 인스턴스가 생성되었는지 확인한다.
      2. 쓰레드 1이 생성자를 호출해 인스턴스를 만들기 전, 쓰레드 2가 if문을 실행해 singleObj 변수가 null인지 확인한다.
         - 현재 singleObj 변수는 null이고, 인스턴스를 생성하는 생성자를 호출하는 코드를 실행하게 된다.
      3. 결과적으로 SingleObj 클래스의 인스턴스가 2개 생성된다.
  
  <br/>
  
- 멀티 쓰레드 환경에서 발생하는 문제를 해결하는 방법

  1. 정적 변수에 인스턴스를 만들어 바로 초기화하는 방법 (Eager Initialization)

     ``` Java
     // static 변수에 외부에 제공할 자기 자신의 인스턴스를 만들어 바로 초기화
     private static SingleObj singleObj = new SingleObj();
     ```

       <br/>

  2. 인스턴스를 만드는 메서드에 동기화 처리를 하는 방법 (Thread-Safe Lazy Initailization)

     ``` java
     // 인스턴스를 만드는 메서드 동기화 (임계 구역)
       public synchronized static SingleObj getInstance() {
            if(singleObj == null) {
                singleObj = new SingleObj();
            }
            return singleObj;
       }
     ```

     - 인스턴스를 만드는 메서드를 임계 구역으로 변경하면
       - 멀티 쓰레드 환경에서 동시에 여러 쓰레드가 getInstance 메서드를 소유하는 객체에 접근하는 것을 방지한다.
     - synchronized 특성상 비교적 큰 성능 저하가 발생한다.

<br/>

<br/>

## 예상질문❔

Q1) 싱글톤 패턴이란 무엇인가?

A1) 생성자가 여러 차례 호출 되어도 최초로 호출된 생성자가 생성한 객체를 리턴하여 그 객체만 사용하도록 하는 디자인 패턴이다. 

<br/>

### Reference📖

- https://gmlwjd9405.github.io/2018/07/06/singleton-pattern.html
- https://jeong-pro.tistory.com/86
- https://velog.io/@kyle/%EC%9E%90%EB%B0%94-%EC%8B%B1%EA%B8%80%ED%86%A4-%ED%8C%A8%ED%84%B4-Singleton-Pattern
