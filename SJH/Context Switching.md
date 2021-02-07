# Context Switching

#### 들어가기 앞서

- Context란?
  - CPU가 다루는 Task에 대한 정보
  
  - 대부분의 정보는 Register에 저장되며 PCB로 관리된다.
  
    ~~~
    <Register>
    - CPU가 요청을 처리하는데 필요한 데이터를 일시적으로 저장하는 기억장치
    ~~~


<br>

## Context Switching이란?

  - CPU가 한 개의 Task(Process/Thread)를 실행하고 있는 상태에서 **Interrupt 요청**에 의해 다른 Task로 실행이 전환되는 과정에서 기존의 Task 상태 및 Context를 저장하고 새로운 Task의 Context정보로 교체하는 작업.
    >Interrupt 요청
    >
    >- 입출력 요청이 왔을 때(I/O interrupt)
    >- CPU사용시간이 만료되었을 때
    >- 자식 프로세스를 만들 때

  - 즉, CPU가 실행하는 프로세스가 교체될 때 CPU에서 관리하는 Context가 교체되는 작업

  - Context Switching일 때 해당 CPU는 아무 일도 할 수 없어서 성능저하가 발생할 수 있다.

  - Process 와 Thread 를 처리하는 Context Switching 은 조금 다른데 Process는 PCB, Thread는 TCB에서 Context Switching한다.

    >**PCB**
    >
    >​	![PCB](https://user-images.githubusercontent.com/58902042/105075111-aac81680-5acc-11eb-8219-3af324d3ae5e.PNG)
    >
    >- OS에 의해 스케줄링되는 Process Control Block
    >- 구조
    >  - Process State : 프로세스 상태
    >  -  Program Counter : 다음에 실행할 명령어 Address
    >  -  Register : 프로세스 레지스터 정보
    >  -  Process number : 프로세스 번호
    >
    >**TCB**
    >
    >![TCB)](https://user-images.githubusercontent.com/58902042/105075114-ab60ad00-5acc-11eb-903e-04f75786880b.PNG)
    >
    >- 프로세스에 있는 스레드 라이브러리에 의해 스케쥴링되는 Thread Control Block
    >
    >**Process Switching vs Thread Switching**
    >
    ><img src="https://user-images.githubusercontent.com/58902042/105075259-dcd97880-5acc-11eb-9105-7b72a9338b3a.PNG" height=250>
    >
    >:bulb:  스레드는 컨텍스트 스위칭 될때 code, data, heap 영역은 프로세스 것이기에 Context 발생시 Stack 영역만 변경을 진행하면 되므로,
    >
    >:bulb:  멀티 프로세스를 통해 PCB를 Context Switching하는 것보다 멀티 스레드를 통해 TCB를 Context Switching하는 비용이 더 적다.

<br>

## 스케쥴러

- Context-Switching을 하는 주체
- 인터럽트가 발생할 때 수행할 다음 프로세스를 결정한다.


<br>

## Context Swithcing을 하는 이유

  - 멀티 프로그래밍을 하기 위해서이다.
    - CPU가 하나의 프로세스를 돌리다가 사용자의 I/O입력을 받아야할 때 입력을 받을 때까지 기다리게 된다면 다른 프로그램은 다 일시정지 상태가 되므로, 이러한 비효율을 막기 위해 사용한다.

<br>

------

<참조>

- [컨텍스트 스위치에 대한 정리](https://jins-dev.tistory.com/entry/%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8-%EC%8A%A4%EC%9C%84%EC%B9%98Context-Switching-%EC%97%90-%EB%8C%80%ED%95%9C-%EC%A0%95%EB%A6%AC)
- [컨택스트 스위칭 개념 정리](https://pearlluck.tistory.com/m/150?category=830586)

- [PCB와 TCB](https://zin0-0.tistory.com/225)
- [Thread와 Process의 Context Switching](https://hwan-shell.tistory.com/197)
- [컨택스트 스위칭](https://www.crocus.co.kr/1364?category=268776)
