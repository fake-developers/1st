## POJO

<br/>

### <u>POJO란?</u>

* **Plain Old Java Object**의 약자로, 오래된 방식의 간단한 [자바](https://ko.wikipedia.org/wiki/자바_(프로그래밍_언어)) 오브젝트라는 말

*  [Java EE](https://ko.wikipedia.org/wiki/Java_EE) 등의 중량 [프레임워크](https://ko.wikipedia.org/wiki/프레임워크)들을 사용하게 되면서 해당 프레임워크에 종속된 "무거운" 객체를 만들게 된 것에 반발해서 사용되게 된 용어

* 특별한 제한에 종속되지 않고, 클래스 패스(class path)를 필요로 하지 않는 일반적인 Java Object를 의미한다.

* 주요 Java 오브젝트 모델, 컨벤션 또는 프레임워크를 따르지 않는 Java 오브젝트를 나타낸다.

* 2000년 9월 마틴 파울러, 레베카 파슨스, 조시 맥켄지에 의해 만들어졌다.

  > *"We wondered why people were so against using regular objects in their systems and concluded that it was because simple objects lacked a fancy name. So we gave them one, and it's caught on very nicely."*
  >
  > *우리는 왜 사람들이 자기들 시스템에 일반적인 오브젝트를 사용하는 것에 반대하는지 궁금했고, 그 이유는 단순한 오브젝트에 멋진 이름이 없기 때문이라고 결론을 지었습니다. 그래서 우리는 멋진 이름을 지었고, 매우 인기를 얻었습니다.*

<br/>

#### 조건

1. **특정 규약에 종속되지 않는다.**

   * 단일 상속 제한 때문에 객체지향적인 설계기법 적용하기 어려워짐

   * 다른 환경으로의 이전이 어려움

2. **특정 환경에 종속되지 않는다.**

   * 예를 들어 웹환경에 종속되는 HttpServletRequest나 HttpSession와 관련된 API를 직접 이용해서는 안된다.

3. **단일 책임 원칙을 지키는 클래스**

   * 단순히 1,2번을 지켰다고 POJO라 할 수 없다. 책임과 역할이 각기 다른 코드를 하나의 클래스에 넣는 경우 진정한 POJO라 할 수 없다.



즉, **POJO란** **객체지향적**인 원리에 충실하면서, **특정 환경과 규약에 종속되지 않아** 필요에 따라 재사용될 수 있는 방식으로 설계된 오브젝트라 할 수 있다.

<br/>

#### ORM과 POJO

> ORM (Object Relationship Mapping)
>
> - 객체-관계 매핑, 즉 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑해주는 것을 말함
>   - 자바 ORM의 기술 표준 JPA, 대표적인 오픈 소스에는 Hibernate가 해당됨
> - 만약 자바 객체가 ORM 기술을 사용하기 위해 Hibernate 프레임워크를 직접 의존하는 순간 POJO라고 할 수 없음
>   - 특정 '기술'에 종속되었기 때문
>
> +) Mybatis는 ORM이 아닌, **SQL 매퍼**임
>
> - ORM 프레임워크는 데이터베이스 객체를 자바 객체로 매핑함으로써 객체 간의 관계를 바탕으로 **SQL을 자동으로 생성**해주지만,
> - Mybatis는 **SQL을 명시**해 주어야 함

<br/>

### <u>POJO는 다음과 같은 것을 해선 안된다. (특징)</u>

1. 미리 지정된 클래스를 extends 하는 것.

   -> 클래스 상속을 강제하지 않는다.

   ```java
   public class Foo extends javax.servlet.http.HttpServlet { ... }
   ```

2. 미리 정의된 인터페이스를 implement 하는 것.

   -> 인터페이스 구현을 강제하지 않는다.

   ```java
   public class Bar implements javax.ejb.EntityBean { ... }
   ```

3. 미리 정의된 Annotation을 포함하는 것.

   -> 애노테이션 사용을 강제하지 않는다.

   ```java
   @javax.persistence.Entity
   public class Baz { ... }
   ```

그러나 기술적 어려움과 다른 이유로 인해, POJO-compliant라고 기술된 많은 소프트웨어 제품이나 프레임워크들(persistence와 같은)은 실제로 미리 정의된 Annotation을 제대로 동작하는 기능을 구현하기 위해 필요로 한다.

이와같은 것들의 특징은 Annotation을 추가하기 전에 POJO이고 Annotation을 제거했을 때, POJO 상태로 되돌아간다면 POJO로 간주할 수 있다는 것이다.

<br/>

### <u> 예시</u>

#### 사용하지 않은 예시(특정 환경에 결합도가 높은 코드) 

**JMS로부터 메시지를 받는 경우**

>JMS를 사용하기 위해 **MessageListener** 인터페이스를 상속받아야 한다. 
>
>하지만, 다음과 같이 구현하면 JMS라는 **특정 환경에 종속**되게 되고 다른 메시징 솔루션을 적용하기 어려워 진다. 
>
>단순한 예제와 달리 Listener가 많은 경우, AMQP나 다른 솔루션으로 교체할 경우 더더욱 어려울 것이다.

~~~java
public class ExampleListener implements MessageListener {

  public void onMessage(Message message) {
    if (message instanceof TextMessage) {
      try {
        System.out.println(((TextMessage) message).getText());
      }
      catch (JMSException ex) {
        throw new RuntimeException(ex);
      }
    }
    else {
      throw new IllegalArgumentException("Message must be of type TextMessage");
    }
  }

}
~~~

<br/>

#### 사용한 예시(특정 환경에 결합도가 낮은 코드)

```java
@Component
public class ExampleListener {

  @JmsListener(destination = "myDestination")
  public void processOrder(String message) {
    System.out.println(message);
  }
}
```

> 위의 코드는 어떠한 인터페이스에 종속되지 않는다. @JmsListenr라는 어노테이션을 이용하여 JMS 서비스와 연동한다. 다른 솔루션을 사용하고 싶은 경우, @RabbitListener 로 바꿔주기만 하면 된다. 

<br/>

### <u>장점</u>

- 특정 규약에 종속되지 않아 객체지향 설계를 할 수 있다.
- 특정 환경에 종속되지 않아 테스트하기 좋다.
- 특정 규약에 종속되지 않아 로우 레벨 코드와 비즈니스 코드가 분리되어 깔끔한 코드 작성이 가능하다.

<br/>

### <u>POJO 프레임워크</u>

#### Spring

스프링은 POJO를 이용한 엔터프라이즈 애플리케이션 개발을 목적으로 하는 프레임워크라 한다. 

* 엔터프라이즈 애플리케이션 개발 중 하나의 예를 들면 DB 이용 기술이 있다.

* DB 이용 기술에 관련된 코드를 객체지향적인 POJO를 기반으로 깔끔하게 구현할 수 있다.

<img src="https://user-images.githubusercontent.com/61674527/120220168-4b96c180-c277-11eb-9a72-158083614d7e.JPG" alt="스프링 POJO" style="zoom:70%;" />

* POJO를 이용해서 만든 애플리케이션 로직 + POJO가 어떻게 관계를 맺고 동작하는지 정의해 놓은 설계정보
* IoC(Inversion of Control, 제어의 역전) 컨테이너 안에서 POJO를 구성 및 관리하는 것이 가장 핵심
* Java EE 등을 사용할 때에 비해서 특정 인터페이스를 구현하거나 상속 할 필요 없고 라이브러리를 지원하기에 용이하며 객체 또한 가벼운 것이 특징이다.

<br/>

### <u>JavaBeans와 POJO</u>



* JavaBeans : 데이터를 표현하기 위한 Java 클래스를 만들 때의 규약
* JavaBeans 규칙
  - 모든 클래스의 프로퍼티는 private이며 getter, setter 메소드로 제어한다.
  - 인자가 없는 public 생성자가 있어야 한다.
  - Serializable 인터페이스를 구현해야 한다.
* Java beans는 POJO이다.
* POJO는 Java beans가 아니다.
* JavaBeans는 특별한 POJO의 변형이라고 볼 수 있다.
  * 바로 `Serializable` 마커 인터페이스(실제 구현이 없고 단순히 확인을 할 수 있는)를 implement하기 때문이다. 
  * 더 세부적인 규약이 정해져있고, 이를 지켜야한다.

<br/>

<br/>

<br/>

### REFERENCE

* [POJO - (Plain Old Java Object)란 뭘까?](https://siyoon210.tistory.com/120)
* [POJO 정리](https://velog.io/@dion/what-is-POJO)
* [[Spring] POJO 란 무엇인가?](https://withseungryu.tistory.com/62)
* [POJO(plain old java object)란?](https://happyer16.tistory.com/entry/POJOplain-old-java-object%EB%9E%80)
* [포조(Plain Old Java Object, POJO) 이해하기](https://needjarvis.tistory.com/585)
* https://github.com/fake-developers/1st/blob/KJY-11/KJY/%5BJAVA%5D%20POJO.md

