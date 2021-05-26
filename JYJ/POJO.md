# POJO

:writing_hand: *Assembled by Yunju Jang*

<!--🤝*Contributors : JeongHea Shin, JiYe Bae*-->

<hr>



## POJO

- <b>POJO 란?</b>

  - Plain Old Java Object

  - 오래된 방식의 간단한 자바 오브젝트라는 뜻이다.

  - Java EE 등의 중량 프레임워크들을 사용하게되면서 무거운 객체를 만들게 된 것에 대한 반발로 사용하게된 용어이다.

    - 한마디로 자바로 가볍게 개발하자는 뜻

  - 2000년 9월 마틴 파울러 등이 사용하기 시작한 용어이다.

    ``` 
    "우리는 사람들이 자기네 시스템에 보통의 객체를 사용하는 것을 왜 그렇게 반대하는지 궁금하였는데, 간단한 객체는 폼 나는 명칭이 없기 때문에 그랬던 것으로 결론 지었다. 그래서 적당한 이름을 하나 만들어 붙였더니, 아 글쎄, 다들 좋아하더라고" - 마틴 파울러
    ```

<br/>

<br/>

- <b>그렇다면, '오래된 방식의 간단한 오브젝트'가 뭘까?</b>

  - 특정 '기술'에 종속되어 동작하는 것이 아닌, 순수한 자바 객체를 말한다.

  - ex) ORM과 POJO

    > ORM (Object Relationship Mapping)
    >
    > - 객체-관계 매핑, 즉 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑해주는 것을 말한다.
    >   - 자바 ORM의 기술 표준 JPA, 대표적인 오픈 소스에는 Hibernate가 해당한다.
    > - 만약 자바 객체가 ORM 기술을 사용하기 위해 Hibernate 프레임워크를 직접 의존하는 순간 <mark>POJO라고 할 수 없다.</mark>
    >   - 특정 <mark>'기술'에 종속</mark>되었기 때문이다.
    >
    > <br/>
    >
    > +) Mybatis는 ORM이 아닌, <b>SQL 매퍼</b>이다.
    >
    >  - ORM 프레임워크는 데이터베이스 객체를 자바 객체로 매핑함으로써 객체 간의 관계를 바탕으로 <b>SQL을 자동으로 생성</b>해주지만,
    >  - Mybatis는 <b>SQL을 명시</b>해 주어야 한다.

<br/>

<br/>

- <b>POJO의 조건</b>

  - 특정 규약에 종속되지 않는다.

    - 어떠한 상속도 받지 않는다.
    - 단일 상속 제한 때문에 객체지향적인 설계기법을 적용하기 어려워진다.
    - 다른 환경으로의 이전이 어렵다.

    <br/>

  - 특정 환경에 종속되지 않는다.

    - API를 직접 이용하지 않는다.
    - 다른 환경에서 사용하기 어렵다.
    - 비즈니스 로직과 기술적인 내용을 담은 웹정보 코드가 섞여 이해하기 어려워진다.
    - 웹 서버에 올리지 않고 독립적으로 테스트하기 어려워진다.

    <br/>

  - 단일 책임 원칙을 지키는 클래스

    - 책임과 역할이 각기 다른 코드를 하나의 클래스에 넣으면 안된다.

  ##### 즉, POJO란 객체지향적인 원리에 충실하면서, 특정 환경과 규약에 종속되지 않아 필요에 따라 재사용될 수 잇는 방식으로 설계된 오브젝트라 할 수 있다.

<br/>

<br/>

- <b>예시</b>

  - POJO를 사용하지 않은 경우

    ``` java
    // 특정 환경에 결합도가 높은 코드
    // JMS로 부터 메시지를 받는 경우 --> JMS를 사용하기 위해 MessageListener 인터페이스를 상속받아야 한다.
    
    public class ExampleListener implements MessageListener {
        public void onMessage(Message message){
            if(message instanceof TextMessage){
                try{
                    System.out.println((TextMessage) message).getText());
                } catch(JMSException ex){
                    throw new RuntimeException(ex);
                }
            } else {
                throw new OllegalArgumentException("Message must be o type Text Message");
            }
        }
    }
    ```

    <br/>

  - POJO를 사용한 경우

    ``` java
    @Component
    public class ExampleListener{
        @JmsListener(destination = "myDestination")
        public void processOrder(String message){
            System.out.println(message);
        }
    }
    ```

    - 위의 코드는 어떠한 인터페이스에 종속되지 않는다.
    - @JmsListener라는 어노테이션을 이용하여 JMS 서비스와 연동한다.
      - 어노테이션의 사용은 어노테이션을 뺐을 때 POJO로 간주되는 경우, POJO로 인정한다.
    - 다른 솔루션을 사용하고 싶은 경우 어노테이션만 바꿔주면 된다.
    - 스프링 프레임워크는 위의 예제처럼 우리의 코드와 라이브러리와의 결합성을 줄이도록 도와준다.

<br/>

<br/>

- <b>POJO의 장점</b>
  - 특정 규약에 종속되지 않아 객체지향 설계를 할 수 있다.
  - 특정 환경에 종속되지 않아 테스트하기 좋다.
  - 특정 규약에 종속되지 않아 로우 레벨 코드와 비즈니스 코드가 분리되어 깔끔한 코드 작성이 가능하다.

<br/>

<br/>

- <b>POJO 프레임워크</b>

  - Spring은 POJO를 이용한 엔터프라이즈 애플리케이션 개발을 목적으로 하는 프레임워크이다.
  - 엔터프라이즈 애플리케이션 개발 중 하나의 예를 들면 DB 이용 기술이 있따.
  - DB 이용 기술에 관련된 코드를 객체지향적인 POJO를 기반으로 깔끔하게 구현할 수 있다.

  <img src="C:\Users\rlo3o\Desktop\장윤주\취업준비\Git\1st\JYJ\resources\pojo.png" width='400px' align='center'>

<br/>

<br/>

<br/>

## 예상질문❔

Q1) POJO란 무엇인가?

A1) 특정 규약과 환경에 종속되지 않는 자바 객체를 말한다.

<br/>

<br/>

### Reference📖

- https://siyoon210.tistory.com/120
- https://dreaming-soohyun.tistory.com/entry/JPA%EC%99%80-MyBatis%EC%9D%98-%EC%B0%A8%EC%9D%B4-ORM%EA%B3%BC-SQL-Mapper
- https://gmlwjd9405.github.io/2019/02/01/orm.html
- https://mangkyu.tistory.com/20
- https://okky.kr/article/336882
- https://happyer16.tistory.com/entry/POJOplain-old-java-object%EB%9E%80

