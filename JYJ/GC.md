# 자바 GC

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors :  JiYoung-Kwon, Jeonghea Shin* 

<hr>


- <b>GC란?</b>

  - Garbage Collection
  
  - Garbage : 정리되지 않은 메모리, 유효하지 않은 메모리 주소

    > Garbage 예시
    >
    > ``` Java
    > String[] array = new String[2];
    > 
    > array[0] = '0';
    > array[1] = '1';
    > 
    > array = new String[] {'G', 'C'};
    > ```
    >
    > - String 배열이 할당되기 전 할당된 0과 1
    > - 주소를 잃어버려 사용할 수 없는 메모리
  
  -  메모리가 부족할 때, 이런 가비지들을 메모리에서 해제시켜 다른 용도로 사용할 수 있게 한다.
  
     

<br/>

- <b>GC가 필요한 이유</b>

  - Java Runtime 시, Heap 영역에 저장되는 객체들은 따로 정리하지 않으면 계속해서 쌓이게 되어 OutOfMemory Exception이 발생할 수 있다.

  - OutOfMemory Exception을 방지하기 위해 JVM 에서 주기적으로 사용하지 않는 객체를 수집하여 정리하는 GC를 진행한다.

    > GC 2가지 작업
    >
    > - Heap 내의 객체 중 Garbage를 찾아낸다.
    > - 찾아낸 Garbage 객체를 반환하여 메모리를 회수한다.

  <br/>

<br/>

- <b>GC의 특징</b>

  <img src='resources/garbage.png' width='400px' align='center'>

  - 객체들은 Heap 영역에 생성된다.
  - Heap에 새로운 객체 생성 시, 공간이 부족하면 JVM은 OutOfMemoryGC를 뿌린다.
  - GC는 Root Set of References (유효한 최초의 참조) 가 이루어지지 않는 객체 Unreachable Objects들을 수거한다.
  - GC는 객체를 메모리에서 제거하기 전, 해당 객체의 finalize() 메서드를 호출한다.
  - GC는 사용자가 강제로 수행할 수 없고, 언제 일어나는지도 정확히 알 수 없다.

  <br/>

  > <b>GC 전 후의 메모리</b>
  >
  > <img src='resources/beforeGC.png' width='500px' align='center'>
  >
  > <img src='resources/afterGC.png' width='500px' align='center'>
  >
  > <br/>
  >
  > <br/>
  >
  > <b>GC의 대상이 되는 객체</b>
  >
  > - 모든 객체 참조가 Null 인 경우
  > - 객체가 블럭 안에서 생성되고 블럭이 종료된 경우
  > - 부모 객체가 Null 인 경우 그 자식 객체
  > - 객체가 Weak 참조만 가지고 있을 경우
  > - 객체가 Soft 참조이지만 메모리 부족이 발생한 경우

  <br/>

  <br/>

- <b>JVM 메모리 영역</b>

  - GC 작업을 진행하는 가비지 콜렉터는 GC를 위해 다음 역할을 한다.
    - 메모리 할당
    - 사용 중인 메모리를 인식
    - 사용하지 않는 메모리를 인식
  - 위 세가지 작업을 통해 앞으로 메모리를 얼마나 사용할 수 있는지 파악하고 GC를 언제 진행할지 지정할 수 있다.

  > <b>JVM 메모리 영역</b>
  >
  > <img src='resources/JVMmemory.png' width='450px' align='center'>
  >
  > - 세가지 영역으로 나뉜다. (Young, Old, Perm)
  >
  > - Young 영역 (객체 사용 시간이 짧은 객체들)
  >
  >   - Eden - Survivor 까지의 영역을 Young 영역이라고 한다.
  >   - <mark>새로 생성한 객체</mark>가 위치한다.
  >   - 대부분의 객체가 금방 접근 불가능한 상태 (unreachable)가 되기 때문에 많은 객체가 Young에서 생성되었다가 사라진다.
  >   - 이 영역에서 객체가 사라질 때, <b>Minor GC</b>가 발생한다고 한다.
  >
  >   <br/>
  >
  > - Old 영역
  >
  >   - Young 영역에서 reachable 상태를 유지해 <mark>살아남은 객체</mark>가 복사된다.
  >   - 대부분 Young 영역 보다 크게 할당되며, 크기가 큰 만큼 Young 영역 보다 GC가 적게 발생한다.
  >   - 이 영역에서 객체가 사라질 때, <b>Major GC</b>가 발생한다고 한다.
  >
  >   <br/>
  >
  > - Perm
  >
  >   - Method Area라고도 한다.
  >   - 클래스와 메소드 정보와 같이 자바 언어 레벨에서는 거의 사용되지 않는 영역이다.
  >   - 이 영역에서 GC가 발생하면 <b>Major GC</b>의 횟수에 포함된다.

  

<br/>

- <b>GC의 타입</b>

  - Major GC

    - Old, Perm 영역에서 발생하는 GC
    - 트리거 되는 시점 : Minor GC가 실패한 경우

    <br/>

  - Minor GC

    - Young 영역에서 발생하는 GC
    - 트리거 되는 시점 : Eden이 full일 경우

    <br/>

  - Full GC

    - 메모리 전체를 대상으로 하는 GC
    - 트리거 되는 시점 : Minor나 Major GC가 실패한 경우

<br/>

- <b>GC의 종류와 객체 GC 과정</b>

  > <b>Stop-the-world</b>
  >
  > - GC를 발생하기 위해 JVM이 애플리케이션 실행을 멈추는 것이다.
  > - 발생 시, GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춘다.
  > - GC 작업을 완료한 이후에야 중단했던 작원을 다시 시작한다.
  >
  > <br/>
  >
  > - GC 과정
  >
  >   1. Marking
  >
  >      <img src='resources/Marking.jpg' width='400px' align='center'>
  >
  >      - 프로세스는 마킹을 호출한다.
  >        - 메모리가 사용되는지 안되는지를 찾아낸다.
  >      - 참조되는 객체는 파란색, 참조되지 않는 객체는 주황색으로 보여진다.
  >      - 모든 오브젝트는 마킹 단계에서 결정을 위해 스캔된다. <small>(매우 많은 시간 소모)</small>
  >
  >      <br/>
  >
  >   2. Normal Deletion
  >
  >      <img src='resources/Deletion.png' width='400px' align='center'>
  >
  >      - 참조되지 않는 객체를 제거하고, 메모리를 반환한다.
  >      - 메모리 Allocator는 반환되어 비어진 블럭의 참조 위치를 저장해두고, 새로운 오브젝트가 선언되면 할당되도록 한다.
  >
  >      <br/>
  >
  >   3. Compacting
  >
  >      <img src='resources/Compacting.png' width='400px' align='center'>
  >
  >      - 참조되지 않는 객체를 제거하고 남은, 참조되는 객체들을 묶는다.
  >      - 묶으면 공간이 생기므로, 새로운 메모리 할당 시 더 쉽고 빠르게 진행된다.
  >
  > \* 모든 객체를 Mark & Compact 하는 JVM은 비효율적이다.

  <br/>

  > <b>General GC</b>
  >
  > - 두 가정 하에 만들어진다.
  >
  >   - 대부분의 객체는 금방 접근 불가능 상태 (unreachable)가 된다.
  >   - 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다.
  >
  >   <br/>
  >
  > - 과정
  >
  >   1. 객체가 생성되어 Eden 영역에 올라간다.
  >
  >      
  >
  >      <img src='resources/General1.png' width='450px' align='center'>
  >
  >      - 처음 생성된 객체는 Eden 영역에 할당된다.
  >
  >      - 이후 Eden 영역이 꽉 차면 할당이 해제되지 않은 객체를 Survivor 영역으로 이동시킨다.
  >
  >        <small>(Minor GC가 시작된다. 비참조 객체는 Eden space가 Clear될 때 반환된다.)
  >
  >      <br/>
  >
  >   2. Eden 영역이 꽉 차면 Survivor 영역으로 넘어간다. <small>(단, Survivor 영역 중 하나는 반드시 비어있어야 한다.)</small>
  >
  >      <img src='resources/General2.png' width='450px' align='center'>
  >
  >      - Survivor 영역에 있는 객체는 올라가 있는 Survivor 영역이 꽉 찰 때 다시 GC 심사를 받는다.
  >
  >      - 할당이 되어있고 아직 사용 중이라는 판단이 되면, 다른 Survivor 영역으로 이동한다.
  >
  >        - S1 이동 시, S0과 Eden 영역은 Clear 된다.
  >        - Minor GC 시, 이 과정을 반복한다.
  >
  >      - 객체의 크기가 Survivor 영역의 크기보다 큰 경우, Survivor 영역을 거치지 않고 바로 Old 영역으로 이동할 수 있다.
  >
  >        > <img src='resources/General3.png' width='450px' aling='center'>
  >
  >      <br/>
  >
  >   3. 이 과정에서 오랫동안 살아남은 객체는 Old 영역으로 이동한다.
  >
  >      <img src='resources/General4.png' width='450px' align='center'>
  >
  >      - Old 영역에 들어간 객체는 풀 GC, 메이저 GC가 발생하지 않는 한 GC되지 않는다.

<br/>

<br/>

## 예상질문❔

Q1) 가비지 컬렉션이란 무엇인가?

A1) 참조되지 않는 객체, 즉 가비지를 메모리에서 해제시켜 해당 메모리를 다른 용도로 사용할 수 있도록 하는 것이다.

<br/>

Q2) 자바에서 가비지 컬렉션은 어떻게 진행되는가?

A2) JVM의 가비지 컬렉터가 Heap 영역의 메모리에 공간이 부족하면 Out Of Memory GC를 뿌린다. GC에서 참조가 이루어지지 않는 가바지 객체를 찾아낸다. 찾아낸 가비지 객체를 반환하여 메모리를 회수한다. 

<br/>

Q3) Minor GC와 Major GC의 차이점은 무엇인가?

A3) 마이너 GC는 Young 영역에서 발생하는 GC이고, 메이저 GC는 Old, Perm 영역에서 발생하는 GC이다.

<br/>

Q4) 사용자가 강제로 GC를 사용하지 않는 이유는 무엇인가?

A4) 강제로 GC를 호출할 경우, 모든 백그라운드 쓰레드를 다 정지시키기 때문에 프로그램이 꺼진다. 즉 모든 프로세스에 지장을 주기 때문에 사용하지 않는다.

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/KJY/%5BWEB%5D%20PWA%EB%9E%80.md
- https://github.com/fake-developers/1st/blob/Main/SJH/Java%20GC.md

