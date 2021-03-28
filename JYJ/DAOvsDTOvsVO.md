# DAO vs DTO  vs VO

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JeongHea Shin*

<hr>




## DAO (Data Access Object)

- <b>DAO 란?</b>

  - 데이터 사용 기능
  - Database의 data에 접근하기 위한 객체이다.
  - 직접 DB에 접근하여 데이터를 CRUD (생성, 조회, 수정, 삭제) 하는 기능을 담당한다.
    - 보통 DB connection 로직까지 설정되어 있는 경우가 많다.
  - DB에 접근하기 위한 로직과 비즈니스 로직을 분리하기 위해 사용한다.
  - MVC 패턴의 Model에서 이와 같은 일을 수행한다.
    - JSP 및 Servlet 페이지 내에서 로직을 기술하여 사용할 수 있지만, 코드의 간결화 및 모듈화, 유지보수 등을 위해 별도의 DAO 클래스를 생성하는 것이 좋다.
  
  <br/>
  
  <br/>
  
- <b>DAO 예시</b>

  ``` java
public class DBManager {
    // DB연결과 자원 해제등의 작업을 하는 클래스
   
    // static 초기화 블럭 - static 변수의 복잡한 초기화에 사용됨
    // 해당클래스가 메모리에 로드될 때 최초로 한번만 실행됨
    static{
     try {
  	//1. 드라이버 로딩
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
     System.out.println("DB연결, conn="+conn);
     return conn;
    }
    
    //DB에 연결된 것들을 닫아주는 메서드1
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
    public static void dbClose( PreparedStatement ps, Connection conn) throws SQLException{
     if(ps!=null)
         ps.close();
     if(conn!=null)
         conn.close();
     System.out.println("자원반납, DB Close!!");
    }
    
    //INSERT 메서드(CREATE 부분)
    public static int insertPerson(PersonDTO personDto) throws SQLException {//DB에 Insert
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
   }//deletePerson
  
   //SELECT 메서드 (READ 메서드 - 전체읽기)
   public static List<PersonDTO> selectAll() throws SQLException {
  
    //db - person 테이블 전체 조회
    Connection conn = null;
    PreparedStatement ps = null;
    ResultSet rs = null;
    //여러 개의 레코드를 저장하기 위한 컬랙션
    // => 여러 개의 dto를 담기 위한 컬렉션
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
  
      //한 개의 레코드를 dto에 저장한다
      //한 개의 레코드는 하나의 dto
      //각 레코드(dto)를 컬렉션에 저장
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
     //System.out.println("번호로 조회, dto ="+dto);//toString의 값이 찍힌다.
    }finally{
     DBManager.dbClose(rs, ps, conn);
    }
    return dto;
   }
   
  }
  ```
  
  

<br/>

<br/>

<br/>

## DTO (Data Transfer Object)

- <b>DTO 란?</b>

  - 데이터 저장 기능

  - 메소드 호출 횟수를 줄이기 위해 만든 데이터 객체이다.

  - 로직을 가지지 않는다.
  
  - getter/setter 메서드만을 포함한다.
    - 가변적 성격을 가진다. (setter로 인하여)

  - 계층 (Controller - Service - View layer) 간 데이터 교환을 위한 자바 빈즈가 이에 해당된다.

    > 자바 빈즈 (Java Beans) 란?
    >
    > - java로 작성된 소프트웨어 컴포넌트를 지칭하는 단어이다.
    > - 비즈니스 로직 부분을 담당하는 java 프로그램 단위
    >
    > <br/>
    >
    > 자바 빈즈 사용 이점
    >
    > - JSP 페이지가 복잡한 자바 코드로 구성되는 것을 피할 수 있다.
    > - 재사용 가능한 컴포넌트를 만들 수 있다.

<br/>

<br/>

- <b>DTO 예시</b>
  
  ``` java
  ublic class PersonDTO {
   // DTO (Data Transfer Object), VO (Value Object), Bean
   
   // 1. 멤버 변수
   private int no;
   private String name;
   private String tel;
   private int age;
   private Timestamp regdate;
   
   // 2. 생성자
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
  
   // 3. getter/setter
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
   // 4. toString
   @Override
   public String toString() {
    return "PersonDTO [no=" + no + ", name=" + name + ", tel=" + tel
      + ", age=" + age + ", regdate=" + regdate + "]";
   }  
  ```
  
  

<br/>

<br/>

<br/>

## VO (Value Object)

- <b>VO 란?</b>

  - 데이터 저장 기능
- DTO와 혼용해서 사용하지만 미묘한 차이가 있다.
  - 값을 위해 쓰이는 객체
  - 보통 getter 기능만 포함한다.
      - setter를 이용하여 값을 수정하면 안된다.
      - 따라서, 불변 (read-only) 의 속성을 가진다.
  - 관계 데이터베이스의 레코드에 대응되는 자바 클래스
    - Database 레코드를 구성하는 필드들을 VO의 Attribute로 구성한다.
    - 해당 변수에 접근할 수 있는 Getter/Setter 메서드의 조합으로 형성한다.
    - equals()로 비교할 때 객체의 모든 값을 비교해야 한다.
  
  <br/>
  
  <br/>
  
- <b>VO 예시</b>

  ``` java
  class Color {
      private int R, G, B, A;
      public Color(int r, int g, int b, int a){...}
     	// getters and setters
      public final static Color RED = new Color(255, 0, 0);
      public final static Color GREEN = new Color(0, 255, 0, 0);
  }
  ```

<br/>

<br/>

<br/>

## VO와 DTO 비교

- <b>VO</b>

  - 데이터 그 자체를 담는 객체이다.

    - DB와 연동된 데이터를 받아올 때 사용한다.

  - 불변의 성격을 가진 클래스이다.

    - ex) 지역 번호 (02, 031 ...)

  - 값이 같으면 동일 오프젝트라고 본다. (리터럴)

    - ex) 

    - ``` java
      VO a = VO(1);
      VO b = VO(1);
      // a == b
      ```

<br/>

- <b>DTO</b>

  - 데이터의 전송을 위한 객체이다.

    - 받아온 VO를 통신하여 매핑/처리가 필요한 경우 변환하여 사용한다.

  - 가변의 성격을 가진 클래스이다.

    - ex) 핸드폰 번호

  - 비즈니스 로직이 들어가기도 한다.

  - 같은 값이 들어가도 다르게 본다. (인스턴스)

    - ex)

    - ``` java
      DTO a = new DTO(1);
      DTO b = new DTO(1);
      // a != b
      ```

<br/>

<br/>

<br/>

## 예상질문❔

Q1) DAO란 무엇인가?

A1) DB를 이용해 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 오브젝트이다.

<br/>

Q2) DTO란 무엇인가?

A2) 데이터를 전달하는 객체이다. 계층간 데이터 교환을 위한 자바빈즈가 해당된다.

<br/>

Q3) VO란 무엇인가?

A3) 도메인에서 한 개 또는 그 이상의 속성들을 묶어서 특정 값을 나타내는 객체를 의미한다.

<br/>

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/SJH/DAOvsDTOvsVO.md
- https://genesis8.tistory.com/214
- https://mommoo.tistory.com/61
- https://woowacourse.github.io/javable/post/2020-06-11-value-object/
