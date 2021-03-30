## DAO(Data Access Object) & DTO(Data Transfer Object) & VO(Value Object)

<br/>

### <u>DAO(Data Access Object)</u>

* Data Access Object의 약자
* DAO는 DB의 data에 접근하기 위한 객체로 직접 DB에 접근하여 데이터를 삽입, 삭제, 조회 등 조작할 수 있는 기능을 수행한다.
* MVC 패턴의 Model에서 이과 같은 일을 수행한다.
  - JSP 및 Servlet 페이지 내에서 로직을 기술하여 사용할 수 있지만,
  - 코드의 간결화 및 모듈화, 유지보수 등의 목적을 위해 별도의 DAO 클래스를 생성하는 것이 좋다.
* DAO의 경우는 DB와 연결할 Connection 까지 설정되어 있는 경우가 많다.
* 재 많이 쓰이는 Mybatis 등을 사용할 경우 커넥션풀까지 제공되고 있기 때문에 DAO를 별도로 만드는 경우는 드물다.

<br/>

~~~java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class TestDao {

    public void add(TestDto dto) throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.jdbc.Driver");
        Connection connection = DriverManager.getConnection("jdbc:mysql://localhost/test", "root", "root");

        PreparedStatement preparedStatement = connection.prepareStatement("insert into users(id,name,password) value(?,?,?)");


        preparedStatement.setString(1, dto.getName());
        preparedStatement.setInt(2, dto.getValue());
        preparedStatement.setString(3, dto.getData());
        preparedStatement.executeUpdate();
        preparedStatement.close();
        
        connection.close();

    }
}
~~~

<br/>

### <u>DTO(Data Transfer Object)</u>

- Data Transfer Object의 약자
- 데이터 저장 담당 클래스
- 메소드 호출 횟수를 줄이기 위해 만든 데이터 객체
-  계층간(Controller, View, Business Layer) 데이터 교환을 위한 자바 빈즈(Java Beans)를 의미한다.
- 로직을 가지지 않는 데이터 객체이고 getter/setter메소드만 가진 클래스를 의미한다.
  * setter를 가져서 가변적 성격을 가진다.

>**자바 빈즈(Java Beans)**
>
>- Java로 작성된 소프트웨어 컴포넌트를 지칭하는 단어
>- 비즈니스 로직 부분을 담당하는 Java 프로그램 단위
>- 장점
>  * JSP페이지가 복잡한 자바 코드로 구성되는 것을 피할 수 있음
>  * 재사용 가능한 컴포넌트를 만들 수 있음

<br/>

~~~java
public class PersonDTO {
 //DTO(Data Transfer Object),VO(Value Object), Bean
 
 //1. 멤버변수
 private int no;
 private String name;
 private String tel;
 private int age;
 private Timestamp regdate;
 
 //2. 생성자
 public PersonDTO() {
  super();
 }

 public PersonDTO(int no, String name, String tel, int age, Timestamp regdate) {
  super();
  this.no = no;
  this.name = name;
  this.tel = tel;
  this.age = age;
  this.regdate = regdate;
 }

 //3. getter/setter
 public int getNo() {
  return no;
 }

 public void setNo(int no) {
  this.no = no;
 }

 public String getName() {
  return name;
 }

 public void setName(String name) {
  this.name = name;
 }

 public String getTel() {
  return tel;
 }

 public void setTel(String tel) {
  this.tel = tel;
 }

 public int getAge() {
  return age;
 }

 public void setAge(int age) {
  this.age = age;
 }

 public Timestamp getRegdate() {
  return regdate;
 }

 public void setRegdate(Timestamp regdate) {
  this.regdate = regdate;
 }
 //4. toString
 @Override
 public String toString() {
  return "PersonDTO [no=" + no + ", name=" + name + ", tel=" + tel
    + ", age=" + age + ", regdate=" + regdate + "]";
 }  
}
~~~

<br/>

### <u>VO(Value Object)</u>

* Value Object의 약자
* 데이터 저장 담당 클래스
* 자바에서 단순히 값 타입을 표현하기 위해 불변 클래스를 만든다.
  * 불변 클래스는 Read-Only 속성을 가진다. (DTO와의 차이점)
* 예를 들면 빨강은 Color.RED, 초록은 Color.GREEN 이렇게 단순히 값만 표현하기 위해 getter기능만 존재한다.

<br/>

~~~java
class Color {
    private int R,G,B,A;
    public Color(int r,int g, int b, int a){…}
    //getters and setters
    public final static Color RED = new Color(255,0,0);
    public final static Color GREEN = new Color(0,255,0,0);
}
~~~

<br/>

### <u>DTO VS VO</u>

* VO

  - 데이터 그 자체를 담는 객체
    - DB와 연동된 Data를 받아올 때 사용
  - 불변의 성격을 가진 클래스
    - ex _) 지역번호 02
  - 값이 같으면 동일 오브젝트라고 본다
    - like 리터럴

  ```java
  VO a = VO(1);
  VO b = VO(1);
  //a==b
  ```

* DTO

  * 데이터의 전송을 위한 객체
    - 받아온 VO를 통신하여 매핑/처리가 필요할 경우 변환하여 사용
  * 가변의 성격을 가진 클래스
  * 사람의 핸드폰 번호
  * 비지니스 로직이 들어가기도 한다.
  * 같은 값이 들어가도 다르게 본다
    - like 인스턴스

  ```java
  DTO a = new DTO(1);
  DTO b = new DTO(1);
  //a!=b
  ```

<br/>

<br/>

<br/>

### REFERENCE

* [DAO&DTO&VO()](https://github.com/fake-developers/1st/blob/SJH-09/SJH/DAOvsDTOvsVO.md)
* [DAO&DTO&VO(2)](https://lemontia.tistory.com/591)
* [DAO&DTO&VO(3)](https://rninche01.tistory.com/entry/web-DAO-DTO-VO-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)
* [DAO&DTO&VO(4)](https://berrrrr.github.io/programming/2019/11/03/dao-vo-do-dto/)