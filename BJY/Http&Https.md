## HTTP와 HTTPS

<br>

### <u>HTTP</u>

Hyper Text Transfer Protocol로 인터넷에서 웹 서버와 사용자 컴퓨터에 설치된 웹 브라우저 사이에 문서를 전송하기 위한 통신 규약 (Protocol)이다.

* 80번 포트

* 인터넷에서 Hypertext를 전송하기 위해 사용되는 통신규약

  클라이언트가 80번 포트에서 서버에 연결하면 80번 포트에서 기다리고 있던 서버는 요청에 응답하면서 자료를 전송

* 텍스트 전송을 주고받음. 

* **네트워크에서 전송 신호를 인터셉트 하는 경우 데이터 유출이 발생할 수 있다. **

  `이런 취약점 보완 : HTTPS`

<br/>

### <u>HTTPS</u> 

HTTP + S (Secure Socket)으로 기본 골격이나 사용 목적 등은 HTTP와 거의 동일하지만, 데이터를 받는 과정에서 보안 요소가 추가된다.

* SSL/TLS 프로토콜을 사용함으로써 HTTP의 보안 문제를 해결

* 네트워크 상에서 중간에 제 3자가 정보를 볼 수 없도록 공개키 암호화를 지원

* 실제 전송되는 데이터의 암호화에는 대칭키 암호화 방식을 사용, 키 교환에는 공개키 암호화를 사용

* 공개키 / 개인키

  * 공개키 : 모두에게 공개 가능한 키

  * 개인키 : 나만 가지고 알고 있어야 하는 키

    ![](C:\Users\jyb63\Desktop\취업스터디\1st\BJY\resource\공개키&개인키.jpg)

  * 공개키 암호화 : 개인키로만 복호화 할 수 있음

  * 개인키 암호화 : 공개키로만 복호하 할 수 있음

* 대칭키

  * 처리 속도가 빠르지만, 서버와 클라이언트가 같은 키를 사용해야 함

    키를 공유하는데 문제가 있음

#### HTTPS의 동작 과정

* 인증서 발급

  <img width="450" src="C:\Users\jyb63\Desktop\취업스터디\1st\BJY\resource\https_process.jpg">

  1. 인터넷 사이트는 자신의 정보와 공개키를 인증기관에 제출
  2. 인증기관은 제출된 데이터 검증 절차를 거쳐 개인키로 사이트에서 제출한 정보를 암호화, 인증서 발급
  3. 인증기관은 웹 브라우저에게 자신의 공개키를 제공

* 사용자의 사이트 접속

  <img width="450" src="C:\Users\jyb63\Desktop\취업스터디\1st\BJY\resource\https_process2.jpg"> <img width="450" src="C:\Users\jyb63\Desktop\취업스터디\1st\BJY\resource\https_process3.jpg"> 

  1. 사용자가 사이트에 접속하면, 자신의 인증서를 웹 브라우저에게 보낸다.

  2. 웹 브라우저는 미리 받았던 인증기관의 공개키로 인증서를 해독하여 검증한다.

     사이트의 정보와 사이트의 공개키를 알게 된다.

  3. 얻은 사이트 공개키로 대칭키를 암호화해 다시 사이트에 보낸다.

  4. 사이트는 개인키로 암호문을 해독해 대칭키를 얻게 되고, 이제 대칭키로 데이터를 주고받을 수 있다.

<br/>

### <u>HTTP VS HTTPS</u> 

* HTTP에 비해 보안 기능이 추가된 HTTPS가 처리 속도가 더 느리다. 오늘 날에는 거의 차이를 느끼지 못한다.

* 사용자 정보를 웹 서버와 주고 받아야 하는 경우 HTTP는 정보 유출의 위험성이 있다.

* 정보 공유 시 SEO에 의해 HTTPS를 이용하는 사이트가 우선 검색될 수 있다.

  (보안 문제가 중요해 짐에 따라 구글에서 가산점 부여한다고 발표 했음)

* HTTPS는 인증서를 발급하고 유지하기 위한 추가비용이 발생하므로, 단순 정보 조회 등만을 처리한다면 HTTP를 이용하는 것이 좋다.

* 가속화된 모바일 페이지(AMP, Accelerated Mobile Pages)를 만들 땐, HTTPS 프로토콜을 사용해야함

~~~
AMP

모바일 기기에서 훨씬 빠르게 콘텐츠를 로딩하기 위한 방법
HTML에서 불필요한 부분을 없앤 것이라고 볼 수 있다.
~~~

<br>

<br>

<br>

### REFERENCE

* https://github.com/fake-developers/1st/blob/KJY-02/KJY/%5BNETWORK%5D%20HTTP%EC%99%80%20HTTPS.md
* https://github.com/fake-developers/1st/blob/JYJ-02/JYJ/HttpAndHttps.md

