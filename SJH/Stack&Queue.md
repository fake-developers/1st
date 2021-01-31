# 스택(Stack), 큐(Queue)

<br>

### 스택(Stack)

<img src="https://camo.githubusercontent.com/637e093a28b8aed52379f86aabd94ba179b0b5092849b09d74a8296d00e2f8a7/68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f627931716e542f6274714245317631556c582f7a626e5864596e474158684d5962634443636136574b2f696d672e706e67" width=300> 

- 쌓아 올린다는 것을 의미
- 차곡차곡 쌓아 올린 형태의 자료구조

<br>

- #### 특징

  - **LIFO 구조** : 후입선출(Last-in First-out)
    - 마지막에 들어온 것이 먼저 나간다.
    - 입구와 출구가 같은 자료구조
  - 같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있다.
  - top으로 정한 곳을 통해서만 접근할 수 있다.
    - 자료 삭제 또한 top을 통해서만 가능하다.
  - **top** : 가장 위에 있는 자료, 가장 최근에 들어온 자료
    - 삽입되는 새 자료는 top이 가리키는 자료의 위에 쌓이게 된다.
    - 초기값 : -1
  - **push** : top을 통해 삽입하는 연산
  - **pop** : top을 통해 삭제하는 연산
  - 예외 처리
    - stack underflow : 비어있는 스택에서 원소를 추출하려는 경우
    - stack overflow : 스택이 넘치는 경우

  <br>

- #### 활용예시

  - 웹 브라우저 방문기록(뒤로 가기)  : 가장 나중에 열린 페이지부터 다시 보여준다.
  - 역순 문자열 만들기 : 가장 나중에 입력된 문자부터 출력한다.
  - 실행 취소(undo) :  가장 나중에 실행된 것부터 실행을 취소한다
  - 후위 표기법 계산
  - 수식의 괄호 검사 (연산자 우선순위 표현을 위한 괄호 검사)

<br>

- #### 오퍼레이션

  - isEmpty() : 스택이 현재 비어있는지 체크
  - push(data) : 스택에 데이터 삽입
  - pop() : 스택에서 데이터 삭제
  - peek() : 스택의 맨 위(다음에 꺼낼 데이터) 확인

<br>

- #### 구현

  ~~~java
  import java.util.EmptyStackException;
   
  public class Stack {
      
      private static class Node {
          private int data;
          private Node next;
          private Node(int data) {
              this.data = data;
          }
      }
      
      private Node top;
      
      public boolean isEmpty() {
          return top == null;
      }
      
      public int peek() {
          if(isEmpty()) throw new EmptyStackException();
   
          return top.data;
      }
      
      public void push(int data) {
          Node node = new Node(data);
          node.next = top;
          top = node;
      }
      
      public int pop() {
          if(isEmpty()) throw new EmptyStackException();
          
          int data = top.data;
          top = top.next;
          return data;
      }
  }
  ~~~

 <br>

<br>

### 큐(Queue)

<img src="https://camo.githubusercontent.com/8f80a2e2c4cb0930f125de21976ef6caef13f71cfbc54e44ebd22506e52ba4e8/68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f5a636533552f6274714244614f664755352f5263326b5233507571693351695161336f3643504c312f696d672e706e67" width=300> 

- 줄 or 줄을 서서 기다리는 것

<br>

- #### 특징

  - **FIFO 구조 ** : 선입선출(First-in First-out)

    - 먼저 들어온 것이 먼저 나간다.
    - 공연장에서 입장을 기다리는 관객
  - 한 쪽 끝에서 삽입 작업, 다른 쪽 끝에서 삭제 작업이 양쪽으로 이루어짐

    - **front** : 삭제연산만 수행되는 곳. 첫 원소
  - **rear** : 삽입연산만 수행되는 곳. 끝 원소
  - **deQueue** : 데이터의 삭제 연산. front에서 이루어짐
  - **enQueue** : 데이터의 삽입 연산. rear에서 이루어짐
  - 들어올 때 rear로 들어오지만 나올 때는 front부터 빠지는 특성

  <img src="https://camo.githubusercontent.com/4ccea346525de9879add8f0b21ad1e121bbb8c2fb3cc53c2949da5283a8b86d4/68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f64354c6f41352f62747176324a32705257492f4b70345a73734b7a626856505778634b6e48557777302f696d672e706e67">

<br>

- #### 활용예시

  - 주로 데이터가 입력된 시간 순서대로 처리해야 할 필요가 있는 상황에 이용
    - 우선순위가 같은 작업 예약 (프린터의 인쇄 대기열)
    - 은행 업무
    - 콜센터 고객 대기시간
    - 프로세스 관리
    - 너비 우선 탐색(BFS, Breadth-First Search) 구현
    - 캐시(Cache) 구현

  <br>

- #### 문제점

  - 일반적으로 배열을 [1] [2] [3] [4] 이런 직선 형태로 보았을 때, 가장 오래 기다린 처음 들어온 [1]이라는 데이터가 Dequeue 되면 다른 데이터들을 차례대로 땡겨주어야 한다.

  - \[ ] [2] [3] [4]

    - Dequeue가 되면 Dequeue가 된 자리를 채우기 위해 rear에서 front까지 자리이동을 해주어야 한다.
    - 소수의 자료의 경우는 상광이 없지만 많은 데이터의 경우 연산에 많은 시간이 걸린다.

    ---------

    이러한 문제점을 해결하기 위해 나온 것이 **원형 큐, 순환 큐, 환영 큐** 라고 불리는 방법이다.

    ---------

    <img src="https://camo.githubusercontent.com/be30b302ee5bef0a0c06a268e6eb3e6ea8c79ec8baf2d11c78c423e97fd73925/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f313935323538343634453745434231433044" height =150> 

    - 배열을 직선으로 보는 것이 아니라 원형으로 보는 방법
    
    <br>

- #### 오퍼레이션

  - isEmpty() : 큐가 현재 비어있는지 체크
  - enqueue() : 큐에 데이터 삽입
  - dequeue() : 큐에서 데이터 삭제
  - peek() : 큐의 맨 앞(다음에 꺼낼 데이터) 확인

<br>

- #### 구현

  ~~~java
  import java.util.EmptyStackException;
   
  public class Queue {
      
      private static class Node{
          private int data;
          private Node next;
          private Node(int data) {
              this.data = data;
          }
      }
      
      private Node front;
      private Node rear;
      
      public boolean isEmpty() {
          return front == null;
      }
      
      public int peek() {
          return front.data;
      }
      
      public void enqueue(int data) {
          Node node = new Node(data);
          if(rear != null) {
              rear.next = node;
          }
          rear = node;
          if(front == null) {
              front = node;
          }
      }
      
      public int dequeue() {
          if(isEmpty()) throw new EmptyStackException();
          
          int data = front.data;
          front = front.next;
          if(front == null) {
              rear = null;
          }
          return data;
      }
  }
  ~~~

<br>

<br>

### 스택 vs 큐

<img src="https://camo.githubusercontent.com/21d71b702146591e4ec9b8db11414ee62dec16f78bdeeb727d01f2c781ba97b1/68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f626b74444b782f62747176305756747052382f33627634647278314a52784d554c4b76516b6a49744b2f696d672e706e67">

- 스택, 큐 java 코드 및 실행 결과

  <img src="https://camo.githubusercontent.com/607b94b1694165b282fb9f26d2c18ff0bf4227550f9821ce8e4faa8fed5c4e59/68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f6355474771432f62747142464d4c5747536f2f6c3650576345744253626165544d685a45423171314b2f696d672e706e67"> 

  <img src="https://camo.githubusercontent.com/4739bb0a016f0df28d623823ef37796a5b069355e2d71c58988ae18ce36eaeaf/68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f636c70426e7a2f627471424530343470306b2f7a673763626c764b5342576b6b6f4b3033324e56336b2f696d672e706e67"> 



<br>

-------------

 ### 예상질문 :bulb:

 	1. **스택과 큐의 구조**에 대해 설명하시오
     - 스택은 LIFO(후입선출의 구조), 큐는 FIFO(선입선출의 구조)를 가진다.



2. 큐의 문제점과 해결방안에 대해 설명하시오.
   - 일반적으로 만들어진 큐의 경우, 배열로 만들어지기 때문에 Dequeue가 되면 뒤에 있는 데이터를 앞으로 땡겨주어야 한다. 따라서 연산에 많은 시간이 걸리게 된다.
   - 이를 해결하기 위해 원형 큐, 순환 큐, 환영 큐라고 불리는 배열을 원형으로 보는 큐가 나왔다.

<br>

----------

**<참조>**

- <https://github.com/fake-developers/1st/blob/KJY-04/KJY/%5BDATA%20STRUCTURE%5D%20%EC%8A%A4%ED%83%9D(Stack),%20%ED%81%90(Queue).md>