# String, StringBuffer, StringBuilder 차이

<br>

## 들어가기 앞서

-  Java에서 문자열을 다루는 대표적인 클래스 String, StringBuffer, StringBuilder
- 연산횟수가 많아지거나 멀티쓰레드, Race condition 등의 상황이 자주 발생 하게된다면 각 클래스의 특징을 이해하고 상황에 맞는 적절한 클래스를 사용해야 한다.

<br>

## String

  - **String 특징**

    - 불변의 성질을 가지고 있다.

    - StringBuffer, StringBuilder와 다르게 **리터럴을 통해 생성되면 그 인스턴스의 메모리 공간은 절대 변하지 않는다.**

    - 리터럴로 생성하면 String Pool 공간에 생성되며, 문자열 값은 절대 변하지 않는다.

      - '+' 연산이나, concat() 메서드를 이용하여 변화를 주어도 메모리 공간 내의 값이 변하는 것이 아니라
      - String Pool 공간 안에 메모리를 할당 받아 **새로운 String 클래스 객체를 만들어** 문자열을 나타낸다.

      - ex_)

        ~~~java
        String s = "ABC";
        s + = "DEF";
        ~~~

        - String 객체는 내부 데이터를 수정할 수 없으므로 "ABCDEF"라는 새로운 객체가 생성되고, data 변수는 이 객체를 참조한다.

        - 기존에 있던 객체는 참조되지 않게 되어 가비지 컬렉션의 메모리 해제를 기다리게 된다.

           <img src="https://user-images.githubusercontent.com/58902042/106122704-5859ba80-619c-11eb-963e-90d5947a10cc.PNG" height=200>

  - **String 장점**

      - 불변하기 때문에 단순 조회 연산에서는 타 클래스보다 빠르다.
      - 불변하기 때문에 멀티쓰레드 환경에서 동기화를 신경 쓸 필요가 없다.

  - **String 단점**

      - 언제 제거될 지 모른다.
          - 새로운 문자열이 만들어지면, 기존의 문자열은 가비지 콜렉터에 의해 제거 되어야 하기 때문이다.
      - 성능 문제
          - 문자열 연산이 많아질 경우, 계속해서 문자열 객체를 만들어 오버헤드를 발생시킨다.

- **String 클래스 사용이 적절한 경우**

  - 문자열 연산이 적고, 자주 참조하는 경우에 사용한다.

<br>

## StringBuffer, StringBuilder

- **StringBuffer, StringBuilder 공통적 특징**
  - 크기가 유연하게 변하는 가변적 특성을 가지고 있다.
    - 문자열 연산 시 클래스는 한 번만 만들고, 메모리 값을 변경시켜 문자열을 변경한다.
  - 두 클래스가 제공하는 메서드도 같고, 사용하는 방법도 동일하다.
- **StringBuffer, StringBuilder 장점**
  - 문자열 객체를 계속 만들지 않기 때문에 연산이 잦을 때 사용하면 성능이 좋다.
  - 두 클래스의 메서드들이 같아 호환이 가능하다.
- **StringBuffer, StringBuilder의 단점**
  - Buffer size를 초기에 설정해야 하는데, 이 동작으로 인해 String 객체보다 생성 속도가 느리게 된다.
  - 문자열 수정을 할 경우, 마찬가지로 버퍼의 크기를 늘리거나 줄이고, 명칭을 변경해야하는 내부적 연산이 필요하다.
    - 많은 양의 수정이 아니라면 String 객체가 나을 수 있다.
- **StringBuffer, StringBuilder가 적절한 경우**
  - 문자열 연산이 많을 때 두 클래스를 사용한다.
  - StringBuffer
    - 멀티쓰레드 환경
  - StringBuilder
    - 싱글쓰레드 환경이거나 멀티쓰레드 환경이지만 동기화가 필요 없는 경우
    - 1만번 미만의 연산인 경우
  - 연산이 많지 않은 경우 StringBuffer나 StringBuilder나 차이가 거의 없다.

<br>

## String vs (StringBuffer vs StringBuilder)

- **String과 StringBuffer, StringBuilder와의 차이**	
  - String 객체는 한번 생성되면 할당된 공간이 변하지 않지만, 다른 두 클래스의 경우 객체의 공간이 부족해지면 버퍼의 크기를 유연하게 늘려준다.
  - String : 불변 
  - StringBuffer, StringBuilder : 가변
- **StringBuffer와 StringBuilder의 차이**
  - StringBuffer는 멀티쓰레드 환경에서 synchronized 키워드를 사용할 수 있어 멀티쓰레드 상태에서 동기화를 지원한다.
    - Thread-safe하다.
  - StringBuilder는 동기화를 지원하지 않기 때문에 멀티쓰레드 환경에 적합하지 않다.
    - Thread-safe하지 않다.
    - 대신, StringBuffer에 비해 싱글쓰레드 환경에서 연산처리가 빠르다.
  - StringBuilder가 StringBuffer 보다 속도는 빠르지만, 현업에서는 언제 멀티쓰레드 환경에서 돌아갈지 알 수 없기 때문에, 안정적인 StringBuffer를 사용하기도 한다.

<br>

--------

<참조>

- [String, StringBuffer, StringBuilder 차이 및 장단점](https://ifuwanna.tistory.com/221)

- <https://github.com/fake-developers/1st/blob/JYJ-04/JYJ/String.md>