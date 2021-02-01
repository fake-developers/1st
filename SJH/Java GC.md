# 자바 GC

- ### 들어가기 앞서

  - JVM에서 Heap 영역에 남아있는 더 이상 사용되지 않는 인스턴스들을 **가비지** 라고 한다.

<br>

- ### Garbage Collector(GC)

  - 메모리가 부족해 질 경우 JVM은 이 가비지들을 삭제하여 추가로 사용할 수 있는 메모리 공간을 만든다. 이 과정을 **가비지 콜렉팅** 이라고 하며, 이를 수행하는 것을 **가비지 콜렉터**라고 한다.
  
  - Java프로그래밍에서 new라는 키워드가 힙 영역에 동적으로 메모리를 할당해주고, 그 메모리를 자동으로 해제해주는 것이 GC이다.
  
  - **동작 시기**
  
    - GC도 결국 JVM에 올라가기 때문에 기본적으로 런타임에 동작
  
    1. OS로부터 할당 받은 시스템의 메모리가 부족한 경우
    2. 관리하고 있는 힙에서 사용되는 메모리가 혀용된 임계값을 초과하는 경우
    3. 프로그래머가 직접 GC를 실행하는 경우(JAVA에서 System.gc()라는 메소드가 있음, 가급적 쓰지 않는것이 좋다.)

<br>

- ### JVM 메모리 영역 

  ![a](https://user-images.githubusercontent.com/58902042/104981357-cb9c5780-5a4b-11eb-8af3-361d4a789770.PNG)

  - Young Generation(객체 사용 시간이 짧은 객체들)
    - Eden + Survivor(2개)
    - 새롭게 생성된 객체가 위치한다.
    - 이 영역에서 발생하는 GC를 Minor GC라고 한다.
  - Old Generation
    - Young 영역에서 살아남은 객체가 여기로 복사된다.
    - Young 영역보다 메모리가 크게 할당되어 Young영역보다 GC가 적게 발생한다.
    - 이 영역에서 발생하는 GC를 Major GC라고 한다.
  - Perm Generation
    - Heap 영역이 아니다.
    - JVM에 의해 사용하는 클래스와 메서드 객체 정보를 담고 있다.
    - JDK8부터는 PermGen은 Metaspace로 교체된다.

<br>

- ### GC 타입

  - Minor GC
    -  대상 : Young 영역
    - 트리거 되는 시점 : Eden이 full일 경우
  - Major GC
    - 대상 : Old 영역
    - 트리거 되는 시점 : Minor GC가 실패하는 경우
  - Full GC
    - 대상 : 전체 Heap + Permanent 영역
    - 트리거 되는 시점 : Minor나 Major GC가 실패하는 경우

<br>

- ### GC 종류

  - **stop the world**  키워드
    
    - JVM이 GC를 실행하는 동안 GC를 실행하는 메소드를 제외한 모든 쓰레드를 일시적으로 정지시킨다는 것을 의미
  1. **Serial GC**
     - 순차적 GC라고도 불리며, 가장 오래된 GC이다.

     - Mark-Sweep-Compaction 알고리즘이 한번에 하나씩만 동작한다(단일 스레드)
     - Stop-The-World 시간이 너무 길어 사용하지 않는다.

       > **Young 영역** (single thread)
       >
       >  - mark and copy
       >
       >      1. 처음 생성된 객체가 Eden 영역에 올라간다.
       >
       >         <img src="https://user-images.githubusercontent.com/58902042/104958038-a9d2ae80-5a12-11eb-900f-4f611eac9717.png">
       >
       >      2. Eden 영역이 꽉 차면 Minor GC가 발생하게 되며, 이 영역에 위치하는 객체 중 참조되지 않는 객체는 메모리에서 제거되며, 살아남은 객체들은 Servior영역 두 군데 중 한 군데로 이동한다. 단  Servior 영역중 하나는 반드시 비어있어야 한다.
       >
       >         <img src="https://user-images.githubusercontent.com/58902042/104958154-d981b680-5a12-11eb-9675-18e748e69833.png">
       >
       >         2-1. 객체의 크기가 Servior영역의 크기보다 큰 경우 Old영역으로 이동한다.
       >
       >         <img src="https://user-images.githubusercontent.com/58902042/104958155-da1a4d00-5a12-11eb-81fa-54ed613f02ed.png">	
       >
       >      3. 각 객체는 Minor GC에서 살아남은 횟수를 기록하는 age bit를 가지고 있으며, age bit 값이 MaxTenuring Threshold라는 설정값을 초과할 경우, Old영역으로 이동한다.
       >
       >         <img src="https://user-images.githubusercontent.com/58902042/104958160-db4b7a00-5a12-11eb-823f-1242163224e9.png">
       >
       > **Old 영역** (single thread)
       >
       > - mark-sweep-compact
       >   1. mark : 살아남을 객체를 표시한다.
       >
       >   2. sweep : 마킹이 없는 객체를 모두 삭제한다.
       >
       >   3. compact : sweep 단계 후 살아남은 객체들 사이의 빈공간을 합친다.

  2. **Parallel GC**

     - 여러개의 스레드로 Young 영역에서 GC를 수행한다.
     - Stop-The-World 시간을 줄일 수 있다.

       > **Young 영역**(multi thread)
       >
       > - mark and copy
       >
       > **Old 영역 **(single thread)
       >
       > - mark-sweep-compact

  3. **Parallel Old GC**
     - Parallel GC와 비슷하나, Mark-Sweep-Compaction 알고리즘 대신 Mark-Summary-Compaction 알고리즘을 사용한다.

       > **Young 영역**(multi thread)
       >
       > - mark and copy
       >
       > **Old 영역**(multi thread)
       >
       > - mark-summary-compact
       >
       >   1. mark : 살아남을 객체를 표시한다.
       >
       >   2. summary : 이전에 GC를 수행하여 컴팩션된 영역에 살아 있는 객체의 위치를 조사한다.
       >
       >   3. compact : summary 단계 후 살아남은 객체들 사이의 빈공간을 합친다.
     
  4. **CMS GC**

     -  힙 메모리의 크기가 클 때 적합하다.
     - Low Latency GC라고도 부른다.

       > **Young 영역**(multi thread)
       >
       > - mark and copy
       >
       > **Old 영역**(multi thread)
       >
       > - mark-sweep-remark
       >   1. Initial Mark (stop-the-world) : 애플리케이스 코드에서 직접/바로 접근 가능한 객체를 판단하고 initial set을 만든다.
       >
       >   2. Concurrent Mark : initial 단계에서 만든 set의 객체들을 따라가며 GC 대상인지 추가로 체크한다.
       >
       >   3. Remark (stop-the-world) : concurrent mark 단계에서 변경된 객체를 다시 체크한다.
       >
       >   4. Concurrent sweep : 표시한 객체들 삭제한다.
       >
       > - CMS 방식은 compaction하지 않아 메모리를 몰아놓지 않으므로 다른 옵션을 사용하여 메모리를 모아준다.
     
  5. **G1 GC**
  
     <img src="https://user-images.githubusercontent.com/58902042/105059384-8e22e300-5aba-11eb-8f79-373ce57e3dc4.png" height=250>
     
     - 큰 용량의 메모리에서 짧은 GC 시간을 보장하는데 목적을 둔다.
     - Eden, Survivor, Old 영역이 존재하지만 고정된 크기로 위치에 존재하지않는다.
     - 전체 Heap 영역을 Region이라는 특정한 크기로 나누어, 각 Region의 상태에 따라 동적으로 역할을 부여한다.
     
       > **Young 영역**(multi thread)
       >
       > - -XX:ParallelGCThreads로 thread 갯수를 조정할 수 있다
       > - 살아 남은 객체들은 Survivor Region으로 이동(evacuation/compacting)한다
       > - 정의된 aging threhold 값을 넘으면, survivor region의 오래된 객체는 Old 영역 region으로 이동한다.
       >
       > **Old 영역**(multi thread)
       >
       > - -XX:ConcGCThreads로 marking 단계에 사용되는 GC 쓰레드 갯수 조정 가능하다.
       > - 전체 heap에 대해서 G하지 않고 일부 region에서만 GC를 수행한다.
       > - Old region 영역의 GC 선택 기준은 사용하는 객체(liveness)를 기준으로 판단한다.
       > - GC 효율을 높이기위해 liveness가 높은 것은 재사용 될 가능성이 높다고 ㅏㄴ단하여 liveness가 적은 것을 GC하도록 한다.
       > - 과정
       >   - Initial Mark(stop-the-world) : Old Region에 존재하는 객체들이 참조하는 Survivor Region을 찾는다. 이 과정에서 Stop-The-World가 발생하게 된다.
       >   - Root Region Scan : Initial Mark 에서 찾은 Survivor Region에서 GC 대상 객체를 탐색한다.
       >   - Concurrent Mark : 전체 Region에 대해 스캔하여, GC 대상 객체가 존재하지 않는 Region은 이후 단계에서 제외된다.
       >   - Remark(stop-the-world) : Stop-The-World 후, GC 대상에서 제외할 객체를 식별한다.
       >   - Cleanup(stop-the-world) : Stop-The-World 후, 살아있는 객체가 가장 적은 Region에 대해서 참조되지 않는 객체를 제거한다. Stop-The-World 끝내고 완전히 비워진 Region을 Freelist에 추가하여 재사용한다.
       >   - Copy(stop-the-world) : Root Region Scan 단계에서 찾은 GC 대상 Region이었지만 Cleanup 단계에서 살아남은 객체들을 Available/Unused Region에 복사하여 Compaction 작업을 수행한다.

<br>

-----

- ### 예상질문

  > **GC란 무엇**인가?
  >
  > - JVM에서 Heap 영역에 남아있는 더 이상 사용되지 않는 인스턴스를 삭제하여 추가로 사용할 수 있는 메모리 공간을 만드는 과정을 수행하는 것

  > GC는 **데이터 영역 중 어디서** 사용되는가
  >
  > - 메모리를 동적으로 할당받는 Heap영역에서 사용된다.

  > **GC의 타입** 3가지에 대해 설명하라.
  >
  > - Young영역에서 사용되는 Minor GC
  > - Old영역에서 사용되는 Major GC
  > - 전체 힙(Young+Old)영역과 Perm에서 사용되는 Full GC가 있다.

<br>

-----

<참조>

- [자바 Garbage Collector에 대해서](https://velog.io/@hygoogi/%EC%9E%90%EB%B0%94-GC%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)

- [Java 가비지 컬렉터 이해하기](https://readystory.tistory.com/48)

- [가비지 컬렉터에 대하여](https://velog.io/@litien/%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%ED%84%B0GC)

- [자바 Garbage Collector이란](https://advenoh.tistory.com/14)

- https://deveric.tistory.com/64
