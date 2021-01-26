# Context Switching

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors :  JiYoung-Kwon, Jeonghea Shin* 

<hr>


- <b>Context란?</b>

  - 사용자-사용자 간, 사용자-시스템 간, 사용자-디바이스 간의 상호작용에 영향을 미치는 사람, 장소, 개체 등의 현재 상황 및 상태를 규정하는 정보들을 뜻한다.
  
  - 운영체제에서는 CPU가 해당 <b>프로세스를 실행하기 위한</b> 해당 <b>프로세스의 정보</b>들을 말한다.

  - 대부분의 정보는 Register에 저장되며, 프로세스의 <b>PCB</b>(Process Control Block)에서 관리한다.
  
    > PCB
    >
    > <img src='resources/PCB.png' width='500px' align='center'>
    >
    > - 각 운영체제의 커널 내부에 존재한다.
    > - 각 프로세스 생성 시에 동시에 생성되어 종료 시 함께 사라진다.
    >
    > <br>
    >
    > PCB 구조
    >
    > - Process State (프로세스 사태)
    > - Program Counter : 다음에 실행할 명령어 Address
    > - Register : 프로세스 레지스터 정보
    > - Process Number : 프로세스 번호
  
    <br/>
  
  <br/>
  
- <b>Context Switching (문맥 교환)이란?</b>

  - CPU가 실행하는 프로세스가 교체되며, CPU에서 관리하는 Context가 교체되는 것을 말한다.
  - 멀티 프로세스 환경에서 CPU가 어떤 하나의 프로세스를 실행 중에 <mark>인터럽트</mark> 요청에 의해 다음 우선 순위의 프로세스가 실행되어야 할 때, 
    - 기존의 프로세스 상태 또는 레지스터 값 <b>(Context)을 저장</b>하고 다음 프로세스를 수행하도록 <b>새로운 프로세스 상태 또는 레지스터 값(Context)을 교체</b>하는 작업이다.

  <br/>

- <b>Context Switching 의 특징</b>

  - 문맥 교환을 통해 멀티 프로세싱과 <mark>멀티 스레딩</mark>을 구현할 수 있다.
    - CPU가 하나의 프로세스를 돌리다 사용자의 I/O 입력을 받아야할 때, 입력 시까지 기다리게 되면 다른 프로그램 전부 일시정지 되므로, 이러한 비효율을 막기 위해 사용된다.
  - CPU의 개수와 스레드의 개수가 같으면 문맥 교환이 발생하지 않는다.
    - 실행 중 상태 (Runnable) 의 스레드가 CPU 개수 보다 적을 경우 문제가 되지 않는다.
  - 기계어 명령어 단위로 이루어진다.
  - 프로세스 간의 문맥 교환은 운영체제의 스케쥴러가 담당한다. <small>즉, 스케쥴러가 다음 수행 프로세스를 결정한다.</small>
  - 문맥 교환을 하는 동안 해당 CPU는 아무런 일을 하지 못한다.
    - 잦은 문맥 교환은 오버헤드를 발생시켜 CPU의 성능을 저하시킬 수 있다.

  <br/>

  > 인터럽트 (Interrupt)
  >
  > - CPU가 프로그램을 실해하고 있을 때, 실행 중인 프로그램 밖에서 예외 상황이 발생하여 처리가 필요한 경우 CPU에게 알려 예외 상황을 처리할 수 있도록 한다.
  >
  > <br/>
  >
  > Context Switching이 일어나는 인터럽트의 경우
  >
  > - I/O Request (입출력 요청 시)
  > - Time slice expired (CPU 사용 시간 만료 시)
  > - Fork a child (자식 프로세스를 만들 때)
  > - Wait for an Interrupt (인터럽트 처리를 기다릴 때)

<br/>

<br/>

## 예상질문❔

Q1) Context란 무엇인가?

A1) CPU 가 실행시키려는 프로세스에 대한 정보들을 말한다.

<br/>

Q2) Context Switching이란 무엇인가?

A2) 어떤 한 프로세스가 실행 중에 인터럽트가 발생하여, 현재 작업 중인 프로세스의 정보를 저장하고 다른 프로세스를 실행하는 교체 과정을 말한다.

<br/>

Q3) 인터럽트란 무엇인가?

A3) CPU가 프로그램을 실해하고 있을 때, 입출력 요청 등 실행 중인 프로그램 밖에서 예외 상황이 발생하여 처리가 필요한 경우 CPU에게 알려 예외 상황을 처리할 수 있도록 하는 것이다.

<br/>

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/KJY/%5BWEB%5D%20PWA%EB%9E%80.md
- https://github.com/fake-developers/1st/blob/Main/SJH/Context%20Switching.md

