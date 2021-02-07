# 데드락

- ### 데드락(Dead lock)이란?

  - **교착상태**라고도 하며
  - 둘 이상의 프로세스가 자원을 점유한 상태에서 프로세스들이 각자 점유하고 있는 자원을 서로 기다릴 때 무한 대기에 빠지는 현상을 말한다.

<br>

- ### 데드락의 발생조건

  - 교착상태가 발생하기 위해서는 밑의 4가지 조건이 충족되어야 한다.
  - 하나라도 충족되지 않으면 교착상태는 발생하지 않는다.
  - **상호 배제**(Multual exclusion)
    - 한번에 하나의 프로세스만이 해당 자원을 사용할 수 있다.
    - 사용 중인 자원을 다른 프로세스가 사용하려면 요청한 자원이 해제될 때까지 기다려야 한다.
  - **점유 대기**(Hold and sait)
    - 자원을 최소한 하나 보유하고, 다른 프로세스에 할당된 자원을 점유하기 위해 대기하는 프로세스가 존재한다.
  - **비선점**(No preemption)
    - 다른 프로세스에 할당된 자원은 사용이 끝날 때까지 강제로 빼앗을 수 없다.
  - **순환 대기**(Circular wait)
    - 대기 프로세스의 집합이 순환 형태로 자원을 대기하고 있다.

<br>

- ### 데드락 해결법

  - **교착 상태 예방** 및 **회피**
    
    - 교착 상태가 되지 않도록 보장하기 위하여 교착 상태를 예방하거나 회피하는 프로토콜을 이용하는 방법
    
  - **교착 상태 탐지** 및 **회복**
    
    - 교착 상태가 되도록 허용한 후 회복시키는 방법
    
  - **교착 상태 무시**

    - 대부분의 시스템은 교착 상태가 잘 발생하지 않으며, 교착 상태 예방, 회피, 탐지, 복구하는 것은 많은 비용이 든다.

    > #### 교착 상태 예방<small>(Prevention)</small>
    >
    > - 교착 상태 발생 조건 중 하나를 제거함으로써 해결하는 방법
    >
    >   - 시스템의 처리량이나 효율성을 떨어트리는 단점이 발생할 수 있다.
    >
    >  > **상호 배제 부정**
    >  >
    >  > - 한번에 여러 프로세스가 공유 자원을 사용할 수 있게 한다.
    >   >
    >   > - but, 추후 동기화 관련 문제가 발생할 수 있다.
    >   >
    >
    >   >**점유 대기 부정**
    >   >
    >   >- 프로세스가 실행에 필요한 모든 자원을 한꺼번에 요구하고 허용할 때까지 작업을 보류해서, 나중에 또 다른 자원을 점유하기 위한 대기 조건을 성립하지 않도록 한다.
    >   >- 즉, 프로세스가 실행되기 전 필요한 모든 자원을 할당한다.
    >   >
    >
    >   > **비선점 부정**
    >   >
    >   >- 이미 다른 프로세스에게 할당된 자원이 선점권이 없다고 가정할 때, 높은 우선순위의 프로세스가 해당 자원을 선점할 수 있도록 한다.
    >   >- 프로세스가 어떤 다른 자원을 요구 할 때 요청한 자원을 사용 가능 한지 검사하여, 사용 가능하다면 점유하고 있는 자원을 반납하고 요구한 자원을 사용하기 위해 대기한다.
    >
    >   >**순환 대기 부정**
    >   >
    >   >- 자원을 순환 형태로 대기하지 않도록 일정한 한 쪽 방향으로만 자원을 요구할 수 있도록 한다.

    

    > #### 교착 상태 회피<small>(Avoidance)</small>
    >
    > - 교착 상태 예방보다 조금 덜 제한적으로 예방법의 단점을 일부 해결가능
    >
    > - 교착 상태가 빠질 가능성이 있는지를 검사하여, **가능성이 없을 때**만 자원을 할당함으로써 문제를 피하는 방법
    >
    >   - **안정 상태(safe state)** 
    >
    >     : 시스템의 프로세스들이 요청하는 모든 자원을, 교착 상태를 발생시키지 않으면서도 차례로 모두에게 할당해줄 수 있는 상태
    >
    >   - **안전 순서(safe sequence)**
    >
    >     : 특정한 순서로 프로세스들에게 자원을 할당, 실행 및 종료 등의 작업을 할 때 교착상태가 발생하지 않는 순서
    >
    > - **불안정 상태**는 교착상태가 발생할 가능성이 있는 상태(교착 상태가 불안정 상태의 부분 집합)
    >
    > - **회피 알고리즘**은 자원을 할당한 후에도 시스템이 항상 **안정 상태(safe state)**에 있을 수 있도록 할당을 허용하자는 것이 기본 특징이다.(은행원 알고리즘)
    >
    >   > **은행원 알고리즘**(Banker's Algorithm)
    >   >
    >   > - 다익스트라가 제안한 기법, 은행에서 모든 고객의 요구가 충족되도록 현금을 할당하는데서 유래한 기법
    >   >
    >   > - 안정상태(safe state)에 있으면 자원을 할당하고, 그렇지 않으면 다른 프로세스들이 자원을 해지 할 때까지 대기한다.
    >   >
    >   > - ex.
    >   >
    >   >   <img src="https://user-images.githubusercontent.com/58902042/105373259-d6244000-5c49-11eb-893b-68e9e059814a.png" height=280>
    >   >
    >   >   - 은행이 빌려줄 수 있는 총 금액 100달러
    >   >
    >   >   - 고객 1, 2, 3에게 각각 20, 30, 30 달러씩 빌려줌
    >   >
    >   >   - 은행에 남은 금액은 20달러
    >   >
    >   >     - 10달러를 더 빌려야하는 고객 2이나, 20달러를 더 빌려야하는 고객 3에게 빌려줄 수 있음
    >   >
    >   >       1. 고객 2에게 10달러를 빌려주고 갚을 때까지 기다린다.
    >   >       2. 고객 2로 부터 40달러를 돌려받아 50달러가 생긴다.
    >   >       3. 고객 1이나 고객 3을 도울 수 있다.
    >   >
    >   >     - 이러한 메커니즘으로 상황을 해결해줄 수 있는 순서열에는
    >   >
    >   >       > 고객2 - 고객1- 고객3
    >   >       >
    >   >       > 고객2 - 고객3 - 고객1
    >   >       >
    >   >       > 고객3 - 고객1 - 고객2
    >   >       >
    >   >       > 고객3 - 고객2 - 고객1
    >   >
    >   >       이 있고, 안전 순서열이 존재한다고 말한다.
    >   >
    >   >     - 이 상태를 안전 상태라고 한다.
    >   >
    >   >     <br>
    >   >
    >   >   - 반면, 고객1이 최소 35달러가 당장 필요하다고 해서 35달러를 빌려줬다고 가정했을 때,
    >   >
    >   >   <img src="https://user-images.githubusercontent.com/58902042/105373902-7f6b3600-5c4a-11eb-8e04-9e8f4cc459ce.png" height=280>
    >   >
    >   >   - 은행에 남은 돈이 5달러 밖에 남지 않아 아무도 해결해줄 수 없다.
    >   >   - 이 상태를 불안전 상태, 또는 교착상태(Dead lock)라고 한다.
    >   >   - 즉, 은행원 알고리즘의 조건은 최소한 한명에게 대출해줄 금액은 항상 은행이 보유하고 있어야한다.
    >   >
    >   > - 은행원 알고리즘 **단점**
    >   >   1. 할당할 수 있는 자원의 수가 일정해야 한다.
    >   >   2. 사용자 수가 일정해야 한다.
    >   >   3. 항상 불안전 상태를 방지해야하므로 자원 이용도가 낮다.
    >   >   4. 최대 자원 요구량을 미리 알아야한다.
    >   >   5. 프로세스들은 유한한 시간 안에 자원을 반납해야 한다.
    >   >   6. 즉, 굉장히 복잡하고 오버헤드가 크다.
    >

    

    > #### 교착 상태 탐지<small>(Detection)</small>
    >
    > - 시스템에 교착상태가 발생했는지 점검하여 교착상태에 있는 프로세스와 자원을 발견하는 기법
    >
    > - 교착상태 발견 알고리즘과 자원 할당 그래프 등을 사용할 수 있다.
    >
    >   > **자원 할당 그래프**
    >   >
    >   > - 프로세스와 자원간의 관계를 나타내는 그래프
    >   >
    >   > - 원 : 프로세스 / 사각형 : 자원 / 사각형 안의 점 : 자원의 수
    >   >
    >   >   - 자원 → 프로세스 (해당 프로세스가 자원을 가지고 있음)	
    >   >   - 프로세스 → 자원 (해당 프로세스가 자원을 요청, 대기 중)
    >   >
    >   > - 그래프에 cycle이 없으면 교착상태 아님
    >   >
    >   > - 그래프에 cycle이 있을 경우,
    >   >
    >   >   - 자원당 자원의 개수가 하나 밖에 없으면, 교착상태
    >   >
    >   >     - R(2) 자원을 p(1),p(2)가 갖고 있으면서, p(3)가 요청하는 상황이기에 교착상태
    >   >
    >   >     <img src="https://user-images.githubusercontent.com/58902042/105376688-59936080-5c4d-11eb-8e7d-56c7c3a6707a.png" height=300>
    >   >
    >   >   - 자원당 자원의 개수가 여러개면 교착상태 일수도 있고, 아닐수도 있다.
    >   >
    >   >     - p(4)가 R(2)를 반납하거나, p(2)가 R(1)을 반납할 수 있기에 교착상태 아님
    >   >
    >   >     <img src="https://user-images.githubusercontent.com/58902042/105376710-61eb9b80-5c4d-11eb-93e1-1c9e9beaafe0.png" height=300>

    

    > #### 교착 상태 회복<small>(Recovery)</small>
    >
    > - 교착상태를 일으킨 프로세스를 **종료**하거나, 교착상태의 프로세스에 할당된 **자원을 선점**하여 프로세스나 자원을 회복하는 것을 의미한다.
    >
    >   > **프로세스 종료**
    >   >
    >   > - 교착상태에 있는 프로세스를 종료하는 방법
    >   > - 종료 방법
    >   >   1. 교착상태에 있는 모든 프로세스를 종료하는 방법
    >   >   2. 교착상태에 있는 프로세스를 하나씩 종료해가며 교착상태를 해결하는 방법
    >
    >   > **자원 선점**
    >   >
    >   > - 교착상태의 프로세스가 점유하고 있는 자원을 선점하여 다른 프로세스에게 할당하여, 해당 프로세스를 일시 정지 시키는 방법
    >   > - 우선순위가 낮은 프로세스, 수행된 정도가 적은 프로세스, 사용되는 자원이 적은 프로세스 등을 위주로 해당 프로세스의 자원을 선점한다.
    >   >
    >   > \* 자원 선점 시 고려할 사항
    >   >
    >   > 1. 자원을 선점할 프로세스 **선택** 문제
    >   >    - 최소한의 피해를 줄 수 있는 프로세스를 선택한다.
    >   > 2. 자원을 선점한 프로세스의 **복귀** 문제
    >   >    - 자원이 부족한 상태이므로 **대부분 일시 중지** 시키고 **다시 시작**하는 방법을 사용한다.
    >   > 3. **기아 현상** 문제
    >   >    - 한 프로세스가 계속하여 자원 선점 대상이 되지 못하도록 고려해야 한다.

<br>

--------

- ### 예상질문

  > **교착상태란 무엇**인가?
  >
  > - 둘 이상의 프로세스가 각각 하나씩 자원을 점유하면서 다른 서로 점유하고 있는 다른 자원을 요청하는 무한 대기 상태

  > **교착상태 발생조건** 4가지
  >
  > - 상호배제, 비선점, 점유 및 대기, 환형 대기가 있다.

  > **교착상태를 해결하기 위한 기법**에는 어떤 것이 있는가?
  >
  > - 교착상태가 발생하기전 발생조건을 제거하는 예방 기법, 교착상태의 가능성을 미리 파악하여 회피하는 회피기법, 교착상태가 발생했는지 발견하는 발견 기법, 교착상태를 일으킨 프로세스를 종료시키거나 선점하는 회복 기법이 있다.

  > **회피기법에서 대표적인 알고리즘**은 무엇인가?
  >
  > - 은행원 알고리즘

<br>


------

<참조>

- [교착상태의 해결 정리](https://heavenly-appear.tistory.com/332)
- [Ch7. Deadlock](https://velog.io/@suuhyeony/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-Ch7.-Deadlock)
- [Deadlock 개념이란? 그에 대한 해결책/회피책](https://jwprogramming.tistory.com/12)
- <https://github.com/fake-developers/1st/blob/BJY-03/BJY/Deadlock.md>
- <https://github.com/fake-developers/1st/blob/JYJ-03/JYJ/DeadLock.md>
