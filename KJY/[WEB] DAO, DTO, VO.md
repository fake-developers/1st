# [WEB] DAO, DTO, VO

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-25)* 

<br/>

## 1. DAO(Data Access Object)

* 데이터 사용 기능
* Database의 data에 접근하기 위한 객체
* 직접 DB에 접근하여 데이터를 CRUD(Create, Read, Update, Delete)하는 기능을 담당
  - 보통 DB Connection 로직까지 설정되어 있는 경우가 많음
* Database에 접근하기 위한 로직과 비즈니스 로직을 분리하기 위해 사용
* MVC 패턴의 **Model** 에서 이와 같은 일을 수행함
  - JSP 및 Servlet 페이지 내에서 로직을 기술하여 사용할 수 있음
  - 그러나 **코드의 간결화 및 모듈화, 유지보수 등의 목적** 을 위해 별도의 **DAO** 클래스를 생성하는 것이 좋음
  - 많이 쓰이는 Mybatis 등을 사용할 경우, 커넥션풀까지 제공되고 있기 때문에 DAO를 별도로 만드는 경우는 드물음

#### 1-1. 예시

* ```java
  // DB연결과 자원 해제등의 작업을 하는 클래스
  public class DBManager {
  
      static{// static 초기화 블럭
          try { //1. 드라이버 로딩
              Class.forName("oracle.jdbc.driver.OracleDriver");
              System.out.println("드라이버 로딩 성공!");
          } catch (ClassNotFoundException e) {    
              System.out.println("드라이버 로딩 실패");    
              e.printStackTrace();   
          }  
      }
      
      //db에 연결하는 메서드 
      public static Connection getConnection() throws SQLException{   
          String url="jdbc:oracle:thin:@127.0.0.1:1521:xe";   
          String user="db 아이디", pwd="db 비번";   
          
          //2. db연결하기 위한 Connection 객체 생성   
          Connection conn = DriverManager.getConnection(url, user, pwd);
          System.out.println("DB연결, conn=" + conn);   
          return conn;  
      }
    
      //DB에 연결된 것들을 닫아주는 메서드 1 
      public static void dbClose(ResultSet rs, PreparedStatement ps, Connection conn) throws SQLException{
          if(rs!=null)       
              rs.close();   
          if(ps!=null)       
              ps.close();   
          if(conn!=null)       
              conn.close();   
          System.out.println("자원반납, DB Close!!"); 
      }
      
    
      //DB에 연결된 것들을 닫아주는 메서드2 
    
      public static void dbClose(PreparedStatement ps, Connection conn) throws SQLException{   
          if(ps!=null)
              ps.close();   
          if(conn!=null)       
              conn.close();   
          System.out.println("자원반납, DB Close!!");  
      }
    
    
      //INSERT 메서드(CREATE 부분)  
      public static int insertPerson(PersonDTO personDto) throws SQLException{//DB에 Insert      
          Connection conn = null; 
          PreparedStatement ps = null; 
          int rowCount = 0;
   
          try{  
              //1,2 .드라이버 로딩,db연결  
              conn = DBManager.getConnection();   
              String sql = "insert into person(no,name,tel,age) values(person_seq.nextval,?,?,?)";    
     
              //3.sql문장을 처리하는 PreparedStatement 객체 생성  
              ps = conn.prepareStatement(sql);  
              ps.setString(1, personDto.getName());   
              ps.setString(2, personDto.getTel());  
              ps.setInt(3,personDto.getAge());
    
              //4.실행 
              rowCount = ps.executeUpdate();   
              System.out.println("person 테이블 입력 처리, rowCount = "+rowCount);  
          }finally{   
              DBManager.dbClose(ps, conn);  
          }  
          return rowCount;
      }
          
   
      //DELETE 메서드 (DELETE 부분)    
      public static int deletePerson(int no) throws SQLException{  
          Connection conn = null;  
          PreparedStatement ps = null;  
          PersonDTO dto = new PersonDTO();  
          int rowCount=0;  
    
          try{   
              //2.sb연결  
              conn = DBManager.getConnection();
     
              //3.sql문장 처리   
              String sql = "delete from person where no=?";   
              ps = conn.prepareStatement(sql);   
              ps.setInt(1,no);   
    
              //4.실행  
              rowCount = ps.executeUpdate(); 
          }finally{   
              DBManager.dbClose(ps, conn);  
          }  
          return rowCount; 
      }
   
      //SELECT 메서드 (READ 메서드 - 전체읽기) 
      public static List<PersonDTO> selectAll() throws SQLException {  
          //db - person 테이블 전체 조회 
          Connection conn = null; 
          PreparedStatement ps = null; 
          ResultSet rs = null;
   
          //여러 개의 레코드를 저장하기 위한 컬랙션 => 여러 개의 dto를 담기 위한 컬렉션 
          List<PersonDTO> list = new ArrayList<PersonDTO>();
   
          try{   
              //1,2. 드라이버 로딩 , db연결   
              conn = DBManager.getConnection();
    
              //3.preparedStatement sql을 코드와 연동하기위함  
              String sql = "select * from person order by no desc";  
              ps = conn.prepareStatement(sql);
              
              //ResultSet 읽어오기 위한 준비  
              rs = ps.executeQuery();
     
              while(rs.next()){    
                  int no = rs.getInt("no");   
                  String name = rs.getString("name");   
                  String tel = rs.getString("tel");    
                  int age = rs.getInt("age");    
                  Timestamp regdate = rs.getTimestamp("regdate");   
                  PersonDTO personDto = new PersonDTO(no, name, tel, age, regdate);    
      
                  list.add(personDto); 
              }//while   
              System.out.println("전체 조회 결과 list.size() :"+list.size()); 
          }finally{   
              DBManager.dbClose(rs, ps, conn);  
          }
          
          return list; 
      }
    
      //SELECT 메서드 (READ 메서드 - 한개 읽기) 
      public static PersonDTO selectByNo(int no) throws SQLException{  
          Connection conn = null; 
          PreparedStatement ps = null;  
          ResultSet rs = null;  
          
          //한 개의 레코드를 하나의 dto로 묶어서 리턴한다.  
          PersonDTO dto = new PersonDTO();  
          try{   
              //2.db연결   
              conn = DBManager.getConnection();
     
              //3.sql문장 처리  
              String sql = "select * from person where no=?";   
              ps = conn.prepareStatement(sql);   
              ps.setInt(1,no);
     
              //4.실행  
              rs = ps.executeQuery();   
              if(rs.next()){    
                  int age = rs.getInt("age");   
                  String name = rs.getString("name");   
                  String tel = rs.getString("tel");   
                  Timestamp regdate = rs.getTimestamp("regdate");
      
                  //하나의 레코드를 하나의 dto로 묶어준다.    
                  dto.setAge(age);   
                  dto.setName(name);   
                  dto.setNo(no);   
                  dto.setRegdate(regdate);   
                  dto.setTel(tel);   
              }  
          }finally{  
              DBManager.dbClose(rs, ps, conn);  
          } 
          return dto; 
      }
  }
  ```

<br/>

## 2. DTO(Data Transfer Object)

* 데이터 저장 기능
* 매소드 호출 횟수를 줄이기 위해 만든 데이터 객체
* 로직을 가지지 않은 데이터 객체
  - getter/setter 메서드만을 포함함
  - **가변적 성격** 을 가짐 (setter를 가지기 때문)
* 계층(Controller, Service, View layer)간 데이터 교환을 위한 *자바 빈즈(Java Beans)* 를 의미
  * 자바빈즈(Java Beans)
    * java로 작성된 소프트웨어 컴포넌트를 지칭하는 단어
    * 비즈니스 로직 부분을 담당하는 java 프로그램 단위
    * 장점
      * JSP 페이지가 복잡한 자바 코드로 구성되는 것을 피할 수 있음
      * 재사용 가능한 컴포넌트를 만들 수 있음

#### 2-1. 예시

* ```java
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
          return "PersonDTO [no=" + no + ", name=" + name + ", tel=" + tel + ", age=" + age + ", regdate=" + regdate + "]";
      }  
  }
  ```

<br/>

## 3. VO(Value Object)

* 데이터 저장 기능
* DTO와 혼용해서 사용하지만, 미묘한 차이가 있음
  - 값을 위해 쓰이는 객체
    - 보통 getter의 기능만 포함함
      - setter를 이용하여 값을 수정하면 안된다는 것
    - **불변(read-only)** 의 속성을 가짐
* 관계 데이터베이스의 레코드에 대응되는 자바 클래스
  - Database 레코드를 구성하는 필드들을 VO의 Attribute로 구성
  - 해당 변수에 접근 할 수 있는 Getter/Setter 메서드의 조합으로 형성
  - equals()로 비교할 때 객체의 모든 값을 비교해야 함

#### 3-1. 예시

* ```java
  class Color {
      private int R,G,B,A;
      public Color(int r,int g, int b, int a){…}
      //getters and setters
      public final static Color RED = new Color(255,0,0);
      public final static Color GREEN = new Color(0,255,0,0);
  }
  ```

<br/>

 ## 4. VO VS DTO

- **VO**

  - 데이터 그 자체를 담는 객체

    - DB와 연동된 Data를 받아올 때 사용

  - 불변의 성격을 가진 클래스

    - ex) 지역번호 02

  - 값이 같으면 동일 오브젝트라고 봄

    - like 리터럴
    
```java
    VO a = VO(1);
    VO b = VO(1);
    // a == b
    ```
  
- **DTO**

  - 데이터의 전송을 위한 객체

    - 받아온 VO를 통신하여 매핑/처리가 필요할 경우 변환하여 사용

  - 가변의 성격을 가진 클래스

    - ex) 사람의 핸드폰 번호

  - 비지니스 로직이 들어가기도 함

  - 같은 값이 들어가도 다르게 봄

    - like 인스턴스
    
```java
    DTO a = new DTO(1);
    DTO b = new DTO(1);
    // a != b
    ```

<br/>

## :page_with_curl: Reference

- [DAO vs DTO vs VO vs BO 차이](https://berrrrr.github.io/programming/2019/11/03/dao-vo-do-dto/)
- [[web] DAO, DTO, VO 개념 정리](https://rninche01.tistory.com/entry/web-DAO-DTO-VO-개념-정리)
- [VO vs DTO](https://ijbgo.tistory.com/9)
- [DAO vs DTO vs VO](https://thefif19wlsvy.tistory.com/21)
- [Java - DAO, DTO 간단정리](https://m.blog.naver.com/PostView.nhn?blogId=khm900402&logNo=220303769941&proxyReferer=https:%2F%2Fwww.google.com%2F)
- [[스프링 부트 개념] VO(Value Object)와 DTO(Data Transfer Object의 차이](https://namubada.net/376)

- [DAO&DTO&VO(2)](https://lemontia.tistory.com/591)