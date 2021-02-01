# Web Server와 WAS

<br>

### 들어가기 앞서

- 

<br>

### Web Server

- 소프트웨어와 하드웨어로 구분된다.
  - 하드웨어 : Web 서버가 설치되어 있는 컴퓨터
  - 소프트웨어 : 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 **정적인 컨텐츠(.html .jpeg .css 등)를 제공**하는 서버
  
- **Web Server의 기능**
  - HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저)의 요청을 서비스하는 기능을 담당한다.
  - 요청에 따라 두가지 기능 중 적절하게 선택하여 수행한다.
    1. 정적인 컨텐츠 제공
       - WAS를 거치지 낳고 바로 자원을 제공한다.
    2. 동적인 컨텐츠 제공을 위한 요청 전달
       - 클라이언트(웹 브라우저)의 요청(Request)을 WAS에 보내고, WAS가 처리한 결과를 클라이언트(웹 브라우저)에게 전달한다.

- **Web Server의 예**
  - Apache Server(대표적), Niginx, IIS(Window 전용 Web 서버) 등

<br>

### WAS(Web Application Server)

- DB 조회나 다양한 로직 처릴르 요구하는 **동적인 컨텐츠를 제공**하기 위해 만들어진 Application Server
- HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 <u>*미들웨어*</u>  이다.
- '웹 컨테이너' or '서블릿 컨테이너'라고도 불린다.

  - 즉, JSP, Servlet 구동 환경을 제공한다.
- **WAS의 역할 **
-  WAS = Web Server + Web Container
  -  Web Server의 기능들을 구조적으로 분리하여 처리하고자는 목적으로 제시되었다.
     -  분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용된다.
     -  주로 DB 서버와 같이 수행된다.
  -  현재는 WAS가 가지고 있는 Web Server도 정적인 컨텐츠를 처리하는데 있어서 성능상 큰 차이가 없다.
- **WAS의 기능**
  1. 프로그램 실행 환경과 DB 접속 기능 제공
  2. 여러 개의 트랜잭션(논리적 작업 단위) 관리 기능
  3. 업무를 처리하는 비즈니스 로직 수행
- **WAS의 예**
  - Tomcat(대표적), JBoss, Jeus, Web Sphere 등

<br>

-----------

*즉, WAS의 경우 웹 서버 + 웹 컨테이너의 개념으로 웹서버의 역할을 동시에 할 수 있다는 것이다. 그렇다면 웹서버를 사용하지 않고 WAS만 쓰면 되는 것 아닌가?*

---------------

<br>

### Web Server와 WAS를 나눠야 하는이유

#### 1. 서버 부하 방지

- WAS는 DB조회나 다양한 로직을 처리하느라 바쁘기 때문에 단수한 정적 컨텐츠는 Web Server에서 빠르게 클라이언트에게 제공하여 처리하는 것이 좋다.
- WAS는 기본적으로 동적 컨텐츠를 제공하기 위해 존재하는 서버이다.
- 만약, WAS가 정적 컨텐츠 요청까지 처리하게 된다면 부하가 커지고 동적 컨텐츠 처리가 지연되면서 수행속도가 느려져 이로 인해 페이지 **노출 시간이 늘어나는 문제가 발생**하여 **효율성이 크게 떨어진다.**

#### 2. 물리적 분리로 보안 강화

- WAS의 경우 DB서버에 대한 접속 정보가 있기 때문에 외부로 노출될 경우 보안상 문제가 될 수있다.
- SSL에 대한 암복호화 처리에 Web Server를 사용

#### 3. 여러대의 WAS 연결 가능

- <u>*Load Balancing*</u>을 위해 Web Server 사용
- fail over(장애 극복), fail back 처리에 유리
- 특히 대용량 웹 어플리케이션의 경우 여러개의 서버를 사용, Web Server와 WAS를 분리하여 무중단 운영을 위한 장애 극복에 쉽게 대응할 수 있다.
  - ex_) 앞단의 Web Server에서 오류가 발생한 WAS를 이용하지 못하도록 한 후 WAS를 재시작하여 사용자는 오률르 느끼지 못하고 이용할 수 있다.

#### 4. 여러 웹 어플리케이션 서비스 가능

- 하나의 서버에서 PHP Application과 Java Application을 함께 사용할 수 있다.

#### 5. 기타**

- 접근 허용 IP 관리, 2대 이상의 서버에서의 세션 관리 등도 Web Server에서 처리하면 효율적이다.

<br>

즉, **자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성**을 위해 Web Server와 WAS를 분리한다.

--------

***Web Server를 WAS 앞에 두고 필요한 WAS들을 Web Server에 플러그인 형태로 설정하면 더욱 효율적인 분산 처리가 가능하다.***

----

<br>

### Web Service Architeture

- Client -> Web Server -> DB

- Client -> WAS -> DB

- Client -> Web Server -> WAS -> DB

  - 이 구조의 동작 과정

    <img src="https://user-images.githubusercontent.com/58902042/106428922-0fac4500-64ad-11eb-884a-c9f135111000.png" height=200>

-------

**<참조>**

- https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html

- https://goldsony.tistory.com/37

- https://jeong-pro.tistory.com/84

- https://codechasseur.tistory.com/25

- [로드밸런싱이란 무엇인가](https://oriyong.tistory.com/94)