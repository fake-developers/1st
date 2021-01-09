## 프로세스 & 쓰레드



### <u>프로세스란?</u>

- 컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램
- 메모리에 올라와 실행되고 있는 프로그램의 인스턴스(독립적인 개체)
- 운영체제로부터 시스템 자원을 할당받는 작업의 단위
- 동적인 개념으로는 실행된 프로그램을 의미

~~~
(참고) 할당받는 시스템 자원의 예
  - CPU 시간
  - 운영되기 위해 필요한 주소공간
  - 프로그램 실행 시 Code, Data, Stack, Heap의 구조로 되어 있는 독립된 메모리 영역을 할당 받는다.
~~~

~~~
- Code 영역
  프로세스가 실행할 코드와 매크로 상수가 기계어의 형태로 저장된 공간

- Data 영역
  코드에서 선언한 전역변수 또는 static 변수 등등이 저장된 공간
  
- Stack 영역
  지역변수, 매개변수, 리턴값, 돌아올 주소 등이 저장된 공간
  함수가 지역변수를 너무 많이 가져 stack 영역 초과 시 stack overflow 발생
  
- Heap 영역
  필요에 의해 메모리를 동적 할당하고자 할 때 사용되는 공간
  메모리 주소 값에 의해서만 참조되고 사용하는 뎡역
  ex) C에서 malloc()로 Heap에 데이터 저장
~~~



### <u>프로세스의 특징</u>

![process](https://user-images.githubusercontent.com/61674527/103727119-d69fc280-501d-11eb-8d16-7318ed1a88b3.jpg)

- 프로세스는 각각 독립된 메모리 영역(Code, Data, Stack, Heap의 구조)을 할당받는다.

- 기본적으로 프로세스당 최소 1개의 쓰레드(메인 쓰레드)를 가지고 있다.

- 각 프로세스는 별도의 주소 공간에서 실행되며, 한 프로세스는 다른 프로세스의 변수나 자료구조에 접근할 수 없다.

- 한 프로세스가 다른 프로세스의 자원에 접근하려면 프로세스 간의 통신(IPC,inter-process communication)을 사용해야한다. ex) 파이프, 파일 , 소캣 등을 이용한 통신 방법 사용

  

### <u>쓰레드란?</u>

* 프로세스내에서 실행되는 여러 흐름의 단위
* 프로세스의 특정한 수행 경로
* 프로세스가 할당 받은 자원을 이용하는 실행의 단위



### <u>쓰레드의 특징</u>

![thread](https://user-images.githubusercontent.com/61674527/103727143-e8816580-501d-11eb-81de-8c04a4a50f4c.jpg)

- 쓰레드는 프로세스 내에서 각각 Stack만 따로 할당받고 Code, Data, Heap 영역은 공유한다.
- 쓰레드는 한 프로세스 내에서 동작되는 여러 실행의 흐름으로, 프로세스 내의 주소 공간이나 자원들(힙 공간 등)을 같은 프로세스 내에 쓰레드끼리 공유하면서 실행된다.
- 같은 프로세스 안에 있는 여러 쓰레드들은 같은 힙 공간을 공유한다. 반면에 프로세스는 다른 프로세스의 메모리에 직접 접근할 수 없다.
- 각각의 쓰레드는 별도의 레지스터와 스택을 갖고 있지만, 힙 메모리는 서로 읽고 쓸 수 있다.
- 한 쓰레드가 프로세스 자원을 변경하면, 다른 이웃 쓰레드도 그 변경 결과를 즉시 볼 수 있다.



### <u>멀티 프로세스와 멀티 쓰레드</u>

#### <u>멀티 프로세스</u>

하나의 응용프로그램을 여러개의 프로세스로 구성하여 각 프로세스가 하나의 작업을 처리하도록 하는 것이다.

**장점**

- 여러개의 자식 프로세스 중 하나에 문제가 발생하면 그 자식 프로세스만 죽는 것 이상으로 다른 영향이 확산되지 않는다.

**단점**

* <u>Context Switching에서의 오버헤드</u>
  Context Switching 과정에서 캐쉬 메모리 초기화 등 무거운 작업이 진행되고 많은 시간이 소모 되는 등의 오버헤드가 발생하게 된다.
* <u>프로세스 사이의 어렵고 복잡한 통신 기법 (IPC)</u>
  프로세스는 각각의 독립된 메모리 영역을 할당받았기 때문에 하나의 프로그램에 속하는 프로세스들 사이의 변수를 공유할 수 없다.

~~~
Context Switching

CPU에서 여러 프로세스를 돌아가면서 작업을 처리하는데 이 과정을 Context Switching라 한다.
~~~



#### <u>멀티 쓰레드</u>

하나의 응용프로그램을 여러개의 쓰레드로 구성하고 각 쓰레드로 하여금 하나의 작업을 처리하도록 하는 것이다.

**장점**

- 시스템 자원 소모 감소 ( 자원의 효율성 증대)
  프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리할 수 있다.
- 시스템 처리량 증가 (처리 비용 감소)
  쓰레드 간 데이터를 주고 받는 것이 간단해지고 시스템 자원 소모가 줄어들게 된다.
- 간단한 통신 방법으로 인한 프로그램 응답 시간 단축
  쓰레드는 프로세스 내의 Stack영역을 제외한 모든 메모리를 공유하기 때문에 통신의 부담이 적다.

**단점**

- 주의 깊은 설계가 필요하다.
- 디버깅이 까다롭다.
- 단일 프로세스 시스템의 경우 효과를 기대하기 어렵다.
- 다른 프로세스에서 쓰레드를 제어할 수 없다. (즉, 프로세스 밖에서 쓰레드 각각을 제어할 수 없다.)
- 멀티 쓰레드의 경우 자원 공유의 문제가 발생한다. (동기화 문제)
- 하나의 쓰레드에 문제가 발생하면 전체 프로세스가 영향을 받는다.



### <u>멀티 프로세스 대신 멀티 스레드를 사용하는 이유</u>

프로그램을 여러개 키는 것보다 하나의 프로그램 안에서 여러 작업을 해결하는 것을 의미한다.

![multi_thread](https://user-images.githubusercontent.com/61674527/103727171-fafb9f00-501d-11eb-9f31-9bcc6b4d93cd.jpg)

1. **자원의 효율성 증대**
   * 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어든다.
   * 쓰레드는 프로세스 내의 메모리를 공유하기 때문에 독립적인 프로세스와 달리 쓰레드 간 데이터를 주고 받는 것이 간단해지고 시스템 자원 소모가 줄어들게 된다. 
2. **처리 비용 감소 및 응답 시간 단축**
   * 프로세스 간의 통신(IPC)보다 쓰레드 간의 통신의 비용이 적으므로 작업들 간의 통신의 부담이 줄어든다.
   * 프로세스 간의 전환 속도보다 쓰레드 간의 전환 속도가 빠르다.

**<u>주의할 점</u>**

- 동기화 문제
- 스레드 간의 자원 공유는 전역 변수(데이터 세그먼트)를 이용하므로 함께 상용할 때 충돌이 발생할 수 있다.





### REFERENCE

* <a>https://github.com/juniza82/process-thread</a>
* <a>https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html</a>
* https://selfish-developer.com/entry/%EC%8A%A4%ED%83%9D-%ED%9E%99-%EC%BD%94%EB%93%9C-%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%98%81%EC%97%AD
* https://recorda.tistory.com/entry/20160503%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0