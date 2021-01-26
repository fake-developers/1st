# Doker

- #### 들어가기 앞서

  - **가상화란?**
    - 물리적인 하드웨어 장치를 논리적인 객체로 추상화 하는 것
    
    - 즉, 하나의 자원을 쪼개서 쓰거나, 여러개의 자원을 하나인것 처럼 묶어서 쓸수 있도록 해준다.
    

<br>

- #### Doker란?

  - **컨테이너 기반의 오픈소스 가상화 플랫폼**

  - 소프트웨어를 컨테이너라는 표준화된 유닛으로 패키징하는 기술

  - Doker에서 가장 중요한 개념 2가지

    > **<u>컨테이너(Container)</u>**
    >
    > ![container](https://user-images.githubusercontent.com/58902042/104299907-204e4880-5509-11eb-9c35-d85943f79827.PNG)
    >
    > - 격리된 공간에서 프로세스가 동작하는 기술
    >
    > - 다양한 프로그램, 실행환경을 추상화고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 해준다.
    >
    > - **장점** 
    >
    >   1. 가볍고 빠른 실행 속도
    >      - Hypervisor 엔진을 사용하지 않고 Docker Engine을 사용하여 Guest OS 없이 실행 가능하므로,  더 빠른 속도를 보장 할 수 있다.
    >   2. 높은 직접도
    >      - 여러개의 컨테이너를 만들어 실행 중이라 해도 OS는 하나이기 때문에 고밀도가 가능
    >      - 컨테이너에서는 실행되는 프로세스를 위한 메모리만 사용하기 때문에 낮은 사양에서도 동작 가능
    >   3. 낮은 오버헤드
    >      - 가상화를 위한 하드웨어 애뮬레이터 단계없이, 분리된 공간을 만들기 때문에 오버헤드가 낮다.
    >
    > - **단점**
    >   1. HOST OS에 종속적
    >      - 호스트 운영체제의 커널을 공유하여 호스트 운영체제 환경을 그대로 사용해야한다.
    >   2. 컨테이너별 커널구성이 불가능
    >      - 커널하나를 공유하므로 컨테이너마다 다른 커널 작업을 수행할 수 없다.
    > <br>
    >
    >  ~~~
    >   - 컨테이너의 개념을 도커가 처음 만든 것은 아니다.
    >   - 컨테이너, 오버레이 네트워크, 유니온 파일 시스템 등 이미 존재하는 기술을 잘 조합하고 사용하기 쉽게 만들어 도커가 유명해진 것이다.
    >  ~~~
    > 
    >

    > **<u>이미지</u>**
    >
    > ![dockerimage](https://user-images.githubusercontent.com/58902042/104299755-f137d700-5508-11eb-9059-83d1029a2a56.PNG)
    >
    > - 컨테이너 실행에 필요한 파일과 설정값등을 포함하고 있는 것
    > - 이미지를 실행한 상태 == 컨테이너
    > - **장점**
    >
    >   - 같은 이미지에서 여러개의 컨테이너를 생성할 수 있고, 컨테이너의 상태가 바뀌거나 컨테이너가 삭제되더라도 이미지는 변하지 않고 그대로 남아 있는다.
    >   - 즉, 새로운 서버가 추가되면 이리 만든 이미지를 다운받고 컨테이너를 생성하기만 하면 된다.
    >   - 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 의존성 파일을 컴파일하고 다른 것을 설치할 필요성이 사라진다.
    >
    > 	~~~
    > 	- Docker 이미지 배포 -
    > 	Docker hub에 등록하거나
    > 	Docker Registry 저장소를 직접만들어 관리 할 수 있다.
    > 	~~~

<br>

- #### Docker(컨테이너)와 가상머신(VM)의 차이

  ​	<img src ="https://user-images.githubusercontent.com/58902042/104321336-d5432e00-5526-11eb-84c9-43a26e9c6fba.PNG" align="center" height=250 weight =300>

  - OS 내부에는 물리적 자원을 관리하는 커널 공간과 사용자 프로세스를 실행하는 사용자 공간으로 나뉜다.
  - **가상머신**은 os를 자체적으로 가진다.
    - 즉, 가상머신은 독립된 커널 공간을 가지는 OS를 구성한다.
    - Hypervisor로 가상머신을 올려 가상화 한다.

  - **컨테이너**는 사용자 공간을 여러 개로 나누어 사용한다.
    - 즉, 컨테이너는 커널 공간을 공유하여 좀 더 가볍다.
    - Docker 위에 컨테이너를 올려 가상화한다.
    - 가상화 오버헤드가 거의 발생하지 않는다.



<br>

- #### 레이어 저장방식

  - 도커 이미지는 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 용량이 매우 크다.

  - 처음 이미지를 다운받으면 크게 부담되지 않지만 기존 이미지에 파일이 하나 추가되었다고 다시 다운 받는 것은 비효율적이다.

  - 따라서 **레이어**라는 개념을 도입하고 유니온 파일 시스템을 이용하여 여러개의 레이어를 하나의 파일 시스템으로 사용할 수 있게 해준다.

    ![layer](https://user-images.githubusercontent.com/58902042/104315243-023f1300-551e-11eb-8983-e4e960b05361.PNG)

    - **이미지**는 여러개의 읽기 전용 레이어로 구성되고 파일이 추가되거나 수정되면 새로운 레이어가 생성된다.
    - **컨테이너**를 생성할 때도 레이어 방식을 사용하여 기존의 이미지 레이어 위에 읽기/쓰기 레이어를 추가한다.
    - 이미지 레이어를 그대로 사용하면서 컨테이너가 실행중에 생성하는 파일이나 변경된 내용은 읽기/쓰기 레이어에 저장되므로 여러개의 컨테이너를 생성해도 최소한의 용량만 사용한다.

<br>

------------------------------

###### <참조>

- [[AWS]도커란 무엇입니끼?](https://aws.amazon.com/ko/docker/)
- [초보를 위한 도커 안내서](https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html)
- [도커에 대해 알아보기](https://judo0179.tistory.com/14)
- [도커란 무엇인가?](https://likefree.tistory.com/18)

- [가상화란 무엇인가?](https://kim-dragon.tistory.com/5)

  