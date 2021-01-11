## OSI 7계층



### <u>OSI 7계층 이란?</u>

네트워크 프로토콜이 통신하는 구조를 7개의 계층으로 분리하여 각 계층간 상호 작동하는 방식을 정해 놓은 것으로 ISO(국제표준화기구)에서 개발한 모델이다.

![OSI_7layer](https://user-images.githubusercontent.com/61674527/103727194-0a7ae800-501e-11eb-910b-01cd46098825.jpg)

<br>

### <u>OSI 7계층</u> 

#### 7계층 - 응용 계층 (Application Layer)

사용자의 명령에 따라 특정 작업을 수행하는 <strong>소프트웨어</strong>나 인터페이스를 제공하는 <strong>여러 프로토콜</strong> 등 다양한 범주에서 정보를 처리하는 역할을 수행한다.

##### 프로토콜 종류

* HTTP
* SMTP
* DNS
* POP3 ...

#### 6계층 - 표현 계층 (Presentation Layer)

<Strong>데이터의 표현방식에 관한 서비스</strong>가 이루어진다. 송/수신자가 서로 다른 문자를 사용하는 경우 <strong>번역</strong>해서 일관된 데이터 전송으로 인해 서로 이해할 수 있도록 돕는 역할을 한다.

##### 프로토콜 종류

* JPEG
* MPEG
* SMB
* AFP ...

#### 5계층 - 세션 계층 (Session Layer)

응용프로그램들 간의 통신을 관리하고 핵심 역할은 <strong>동기화</strong>이다. 응용프로그램들 사이의 접속을 설정하고 유지하며 데이터 전송 시 동기점을 제공해서 <strong>오류 발생 시 데이터를 재전송하거나 복구</strong>할 수 있다.

##### 프로토콜 종류

* SSH
* TLS ...

#### 4계층 - 전송 계층 (Transport Layer)

데이터 전송에 관한 서비스를 제공하며 <strong>송/수신 측의 실질적인 연결을 설정</strong>하고 신뢰성 있는 통신이 가능하도록 한다. 송/수신 프로세스 간의 연결을 설정한 뒤 오류 복구나 흐름 제어를 통해 안전하게 전체 메시지가 전달될 수 있도록 지원한다.

##### 프로토콜 종류

* TCP
* UDP ...

#### 3계층 - 네트워크 계층 (Network Layer)

데이터를 **패킷**단위로 분할해서 전송한다. 주된 역할은 <strong>최적의 경로를 선택</strong>하는 것이다. 데이터가 수신 호스트에 도착하기 위해 여러 시스템을 거치는데 이때 올바른 경로를 선택할 수 있도록 하는 <strong>라우팅</strong> 기능을 지원한다.

```
패킷(packet)

통신망을 통해 전송하기 쉽도록 자른 데이터의 전송 단위.
package + bucket의 합성어.
```

##### 프로토콜 종류

* IP
* ICMP
* RIP
* ARP ...

#### 2계층 - 데이터링크 계층 (Datalink Layer)

네트워크 계층에서 받은 데이터를 프레임이라는 단위로 구성한다.
디지털 장비의 고유한 물리 주소인 **MAC 주소를 사용**하며 **데이터의 정확한 송수신**을 위한 전송 제어와 오류제어, 데이터 전송시 순서 제어와 데이터 손실을 막기 위해 조절하는 흐름 제어와 같은 정보를 필요에 따라 추가한다.

##### 프로토콜 종류

* Ethernet
* ATM ..

#### 1계층 - 물리계층 (Physical Layer)

전송매체를 통해 **실제로 데이터를 전송하는 부분**이다. 데이터를 전송하기 위해 전송매체에 대한 기계, 전기적 특성에 대해 세부사항을 정의하면서 전송되는 다른 장치에 데이터의 신호변환 등을 담당한다.

##### 프로토콜 종류

* 전선, 전파
* 광섬유, 동축 케이블 ...





### REFERENCE

* <a>https://github.com/HyeminNoh/Tech-Stack/blob/master/docs/Network/OSI7Layers.md</a>
* <a>https://wiseworld.tistory.com/55</a>
* <a>http://www.hellot.net/new_hellot/magazine/magazine_read.html?code=201&idx=17723&public_date=2014-02</a>
