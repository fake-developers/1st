# TCP와 UDP

- ### 들어가기 앞서

  - 네트워크 계층들 중 **전송 계층**에서 사용하는 프로토콜
    - 전송계층 :  IP에 의해 전달되는 패킷의 오류를 검사하고 재전송 요구 등의 제어를 담당하는 계층
    - 그 중, **데이터를 보내기 위해 사용하는 프로토콜**이 TCP와 UDP

  <img src="https://user-images.githubusercontent.com/58902042/104872136-57e94480-5990-11eb-9d9c-a163cd84de13.PNG" height=300>

<br>

- ### TCP

  <img src="https://user-images.githubusercontent.com/58902042/105079218-77888600-5ad2-11eb-9ba6-e0610c76a690.png" width=400>

  - Transmission Control Protocol의 약자
  - 서버와 클라이언트간에 데이터를 신뢰성 있게 전달하기 위해 만들어진 프로토콜
  - 데이터는 네트워크선로를 통해 전달되는 과정에서 손실되거나 순서가 되바뀔수 있는데, TCP가 손실을 검색해내서 이를 교정하고 순서를 재조합할 수 있도록 해준다.
  - **TCP 특징**

    > **흐름제어 및 혼잡 제어**
    >
    > - 흐름제어 : 데이터 처리 속도를 조절하여 수신자의 버퍼 오버플로우를 방지
    > - 혼잡제어 : 네트워크 내의 패킷 수 가 넘지게 증가하지 않도록 방지

    > **연결형 서비스로 가상 회선 방식 제공**
    >
    > <img src="https://user-images.githubusercontent.com/58902042/105078577-8cb0e500-5ad1-11eb-88b0-9199f3843a6f.png" width=500>
    >
    > - **3-way handshaking**과정을 통해 연결을 설정
    >
    >   1. 먼저 open()을 실행한 클라이언트가 SYN을 보내고 SYN_SENT 상태로 대기한다.
    >
    >   2. 서버는 SYN_RCVD 상태로 바꾸고  SYN과 응답 ACK를 보낸다.
    >
    >   3. SYN과 응답 ACK을 받은 클라이언트는 ESTABLISHED 상태로 변경하고 서버에게 응답 ACK를 보낸다.
    >   4. 응답 ACK를 받은 서버는 ESTABLISHED 상태로 변경한다.
    >
    > - **4-way handshaking**과정을 통해 연결을 해제
    >
    >   1. 먼저 close()를 실행한 클라이언트가 FIN을 보내고 FIN_WAIT1 상태로 대기한다.
    >
    >   2. 서버는 CLOSE_WAIT으로 바꾸고 응답 ACK를 전달한다. 동시에 해당 포트에 연결되어 있는 어플리케이션에게 close()를 요청한다.
    >
    >   3. ACK를 받은 클라이언트는 상태를 FIN_WAIT2로 변경한다.
    >
    >   4. close() 요청을 받은 서버 어플리케이션은 종료 프로세스를 진행하고 FIN을 클라이언트에 보내 LAST_ACK 상태로 바꾼다.
    >
    >   5. FIN을 받은 클라이언트는 ACK를 서버에 다시 전송하고 TIME_WAIT으로 상태를 바꾼다. TIME_WAIT엥서 일정 시간이 지나면 CLOSED된다. ACK를 받은 서버도 포트를 CLOSED로 닫는다.

    > **신뢰성 높은 전송**
    >
    > - Dupack-based retransmission
    >
    >   \- 정상적인 상황에서는 ACK 값이 연속적으로 전송되어야 한다.
    >
    >   \- 그러나, ACK값이 중복으로 올 경우 패킷 이상을 감지하고 재전송을 요청한다.
    >
    > - Timeout-based retransmission
    >
    >   \- 일정시간 동안 ACK 값이 수신을 못할 경우 재전송을 요청한다.

    > **전이중(Full-Duplex), 점대점(Point to Point) 방식**
    >
    > - 전이중 : 전송이 양방향으로 동시에 일어날 수 있다.
    > - 점대점 : 각 연결이 정확히 2개의 종단점을 가지고 있다.

<br>

- ### UDP

  <img src="https://user-images.githubusercontent.com/58902042/105079223-78b9b300-5ad2-11eb-99f6-89d14d552405.png" width=400>

  - User Datagram Protocol의 약자

  - 데이터를 데이터그램 단위로 처리하는 프로토콜

  - 신뢰성보다 연속성이 중요한 서비스에서 많이 사용

  - **UDP 특징**

    >**비연결형 서비스로 데이터그램 방식 제공**

    >**간단한 트랜잭션**
  
    >**멀티캐스트/ 브로드캐스트**
  >
    >- point-to-point 방식으로 TCP와 달리 UDP는 멀티캐스트/브로드 캐스트가 가능
  
    >**선택적 CheckSum**

<br>

- ### TCP vs UDP

  |                |            TCP             |          UDP           |
  | -------------- | :------------------------: | :--------------------: |
  | 연결방식       |       연결형 서비스        |    비연결형 서비스     |
  | 패킷 교환 방식 |       가상 회선 방식       |    데이트그램 방식     |
  | 전송 순서      |       전송 순서 보장       | 전송 순서 바뀔 수 있음 |
  | 수신 여부 확인 |           확인함           |     확인하지 않음      |
  | 통신방식       |            1:1             |   1:1 or 1:N or N:N    |
  | 신뢰성         |            높음            |          낮음          |
  | 속도           |            느림            |          빠름          |
| 사용           | HTTP, Email, File transfer |   DNS, Broadcasting    |
  
  >**가상 회선 방식**
  >
  >- 데이터를 전송하기 전 논리적 연결 설정
  >- 경로 설정을 한번만 수행
  >
  ><img width="400" src="https://user-images.githubusercontent.com/58902042/105077355-c385fb80-5acf-11eb-9d93-b26b9413b49d.png">
  >
  >**데이터그램 방식**
  >
  >- 패킷이 독립적으로 전송
  >- 매번 라우터가 최적의 경로를 선택하여 패킷 전송
  >
  ><img  src="https://user-images.githubusercontent.com/58902042/105077354-c2ed6500-5acf-11eb-891a-c469a2ac7cd0.png" width="400">

<br>

------------

- ### 예상질문

  > **전송 순서를 보장할 수 있는 프로토콜**은 무엇이며, 그 **이유**는 무엇인지 쓰시오.
  >
  > - TCP, 패킷 전달을 가상 회선 방식을 쓰기 때문이다.
  > - 데이터를 전송하기 전 논리적 연결을 설정하므로, 전송순서가 변하지 않는다.

  > TCP와 UDP가 사용되는 **계층**은 어디인가?
  >
  > - IP에 의해 전달되는 패킷의 오류를 검사하고 재전송 요구 등의 제어를 담당하는 계층인 전송계층이다

<br>

--------

<참조>

- [TCP와 UDP의 특징과 차이](https://mangkyu.tistory.com/15)

- [TCP와 UDP의 차이를 자세히 알아보자](https://velog.io/@hidaehyunlee/TCP-%EC%99%80-UDP-%EC%9D%98-%EC%B0%A8%EC%9D%B4)
- [TCP란?](https://musclebear.tistory.com/2)

- [가상회선방식과 데이터그램회선 방식](https://gotwo.tistory.com/107)

- [UDP란 UDP장단점 UDP 특징](https://programming119.tistory.com/148)