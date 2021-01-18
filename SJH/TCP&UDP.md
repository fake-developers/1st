# TCP와 UDP

- ### 들어가기 앞서

  - 네트워크 계층들 중 **전송 계층**에서 사용하는 프로토콜
    - 전송계층 :  IP에 의해 전달되는 패킷의 오류를 검사하고 ㅐ전송 요구 등의 제어를 담당하는 계층
    - 그 중, **데이터를 보내기 위해 사용하는 프로토콜**이 TCP와 UDP

  <img src="https://user-images.githubusercontent.com/58902042/104872136-57e94480-5990-11eb-9d9c-a163cd84de13.PNG" height=300>

<br>

- ### TCP

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
    > 	- 3-way handshaking과정을 통해 연결을 설정
    > 	- 4-way handshaking과정을 통해 연결을 해제

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

  - User Datagram Protocol의 약자

  - 데이터를 데이터그램 단위로 처리하는 프로토콜

  - **UDP 특징**

    >**비연결형 서비스**

    >**간단한 트랜잭션**

    >**멀티캐스트/ 브로드캐스트**

    >**CheckSum필드**

<br>

- ### TCP vs UDP

  |                |      TCP       |          UDP           |
  | -------------- | :------------: | :--------------------: |
  | 연결방식       | 연결형 서비스  |   비연결혀여 서비스    |
  | 패킷 교환 방식 | 가상 회선 방식 |    데이트그램 방식     |
  | 전송 순서      | 전송 순서 보장 | 전송 순서 바뀔 수 있음 |
  | 수신 여부 확인 |     확인함     |     확인하지 않음      |
  | 통신방식       |      1:1       |   1:1 or 1:N or N:N    |
  | 신뢰성         |      높음      |          낮음          |
  | 속도           |      느림      |          빠름          |

  

<br>

------------

<참조>

- [TCP와 UDP의 특징과 차이](https://mangkyu.tistory.com/15)

- [TCP와 UDP의 차이를 자세히 알아보자](https://velog.io/@hidaehyunlee/TCP-%EC%99%80-UDP-%EC%9D%98-%EC%B0%A8%EC%9D%B4)
- [TCP란?](https://musclebear.tistory.com/2)

- [가상회선방식과 데이터그램회선 방식](https://gotwo.tistory.com/107)

- [UDP란 UDP장단점 UDP 특징](https://programming119.tistory.com/148)