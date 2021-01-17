# Singleton Pattern

:writing_hand: *Assembled by Yunju Jang*

<!--🤝*Contributors : JiYoung Kwon*-->

<hr>

- 싱글톤 패턴이란?

  
  - 애플리케이션이 시작될 때 클래스가 <mark>최초 한번만</mark> 메모리를 할당하고(static) 그 메모리에 인스턴스를 만들어 사용하는 디자인 패턴이다.
  - 생성자가 여러 차례 호출되어도 실제로 생성되는 객체는 하나이고, 최초 생성 이후에 호출된 생성자는 최초에 생성한 객체를 반환한다.
  - 자바에서는 생성자를 private로 선언하여 생성 불가능하게 하고 getInstance()로 받아서 쓰도록 한다.
  - <b>즉, 싱글톤 패턴은 단 하나의 인스턴스를 생성해 사용하는 디자인 패턴이다. </b>
    <small>+) 인스턴스가 필요하면 똑같은 인스턴스를 만들어내는게 아니라 기존 인스턴스를 사용하는 것</small>
  
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