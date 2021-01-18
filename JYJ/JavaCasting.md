# Java - Upcasting 과 Downcasting

:writing_hand: *Assembled by Yunju Jang*

<!-- 🤝*Contributors : JiYe Bae* -->

<hr>


-  <b>캐스팅이란?</b>
- 타입을 변환하는 것을 말한다. (형변환)
  - 자바의 상속 관계에 있는 부모와 자식 클래스 간에는 서로 간의 형변환이 가능하다.
- 자식 클래스가 부모 클래스 타입으로 캐스팅 되는 업캐스팅과, 부모가 자식 클래스 타입으로 캐스팅되는 다운 캐스팅이 있다.
  

<br/>

### 업 캐스팅

- <b>업캐스팅이란?</b>

  - 서브 클래스의 객체가 수퍼 클래스의 타입으로 형변환 되는 것을 말한다.
  - 자바에서 서브 클래스는 수퍼 클래스의 속성을 상속 받기 때문에
    - 서브 클래스의 객체는 슈퍼 클래스의 멤버를 모두 가진다.
    - 따라서, 서브 클래스는 슈퍼 클래스로 취급될 수 있다.
  - 즉, 수퍼 클래스 레퍼런스 변수가 서브 클래스로 객체화된 인스턴스를 가리킬 수 있게 된다.

  > 예시
  >
  > ``` Java
  > class Person { // 슈퍼 클래스
  >     String name;
  >     Person(String name){
  >         this.name = name;
  >     }
  > }
  > 
  > class Student extends Person { // Person을 상속 받은 서브 클래스
  > 	String check;
  >     Student(String name) {
  >         super(name);
  >     }
  > }
  > 
  > public class Practice {
  >     public static void main(String[] args){
  >         // 레퍼런스 student를 이용하면 name과 check에 접근이 가능하다.
  >         Student student = new Student("홍길동");
  >         
  >         // 레퍼런스 person을 이용하면 Student 객체의 멤버 중
  >         // 오직 Person 클래스의 멤버(name)만 접근이 가능하다.
  >         Person person = student;
  >         person.name = "이름입니다.";
  >         
  >          // check는 Person 클래스의 멤버가 아니어서 컴파일 오류
  >         person.check = "이름입니다.";
  >     }
  > }
  > ```
  >
  > - 위 코드와 같이 업캐스팅을 하게 되면 객체 내에 있는 모든 멤버를 접근할 수 없다.
  > - 오직 수퍼 클래스의 멤버에만 접근이 가능하고, 이는 멤버 필드와 멤버 메서드에도 동일하게 적용된다.

  - 업캐스팅 시에는 명시적인 타입 캐스팅을 선언하지 않아도 된다. 

    <small>ex) <code>Person person = (Person) student</code></small>

  <br/>

- <b>업캐스팅을 사용하는 이유</b>

<br/>

<br/>

### 다운 캐스팅

- <b>다운캐스팅이란?</b>

  - 자신의 고유한 특성을 잃은 서브 클래스의 객체를 다시 복구 시켜주는 것을 말한다.
  - 업캐스팅 된 것을 다시 원상태로 돌리는 것이다.

  > 예시
  >
  > ``` Java
  > class Person {
  >     String name;
  >     
  >     public Person(String name){
  >         this.name = name;
  >     }
  > }
  > 
  > class Student extends Person {
  >     String check;
  >     
  >     public Student(String name) {
  >         super(name);
  >     }
  > }
  > 
  > public class CastingTest {
  >     public static void main(String[] args){
  >         // 업캐스팅을 먼저 진행
  >         Person person = new Student("홍길동");
  >         
  >         // 다운캐스팅
  >         // 위에 선언한 person을 명시적으로 강제 형변환
  >         Student student = (Student)person; 
  >         
  >         student.name = "이름입니다.";
  >         student.check = "이름입니다."; // 둘 다 컴파일 에러가 발생하지 않음
  >     }
  > }
  > ```
  >
  > - 위 코드에서 업캐스팅과 다른점은, <b>명시적으로 타입을 지정</b>해야 한다는 점이다.
  >
  > - 또한, 업캐스팅이 <b>선행</b>되어야 한다.
  >
  > - 형변환할 타입을 명시함으로서 컴파일 오류는 사라졌지만, 실제 코드를 수행하면서 ClassCastException이 발생할 수 있다. 
  >
  >   <small>* ClassCastException : 어느 객체를 상속 관계에 없는 클래스에 캐스트하려고 할 때 발생</small>
  >
  > - 즉, 어떤 레퍼런스가 가리키는 객체의 타입인지를 구분하기 어렵다.

  <br/>

- instanceof

  - 다운캐스팅을 할 때, 어떤 객체의 타입인지 구분하기 위해 사용하는 연산자

  > instanceof 연산자의 형태
  >
  > <img src='resources/instanceof.png' width='300px' align='center'>
  >
  > - instanceof 연산자의 결과 값은 boolean 타입으로 true, false를 반환 값으로 가진다.
  >
  > - 업캐스팅 했을 때 레퍼런스 변수가 가리키는 객체의 타입이 어떤 것인지 구분하기 어려울 때 유용하다.
  >
  > - 예시
  >
  >   ``` Java
  >   class Unit {
  >       ...
  >   }
  >   
  >   class Zelot extends Unit {
  >       ...
  >   }
  >   
  >   class Marine extends Unit {
  >       ...
  >   }
  >   
  >   class Zergling extends Unit {
  >       ...
  >   }
  >   
  >   public class CastingTest {
  >       public static void main(String[] args) {
  >           Unit unit;
  >           unit = new Unit();
  >           unit = new Zealot(); // 업캐스팅
  >           unit = new Marine(); // 업캐스팅
  >           unit = new Zergling(); // 업캐스팅
  >       }
  >   }
  >   ```
  >
  >   - 위 코드의 서브클래스 들은 모드 Unit 클래스를 상속받고 있어 컴파일 오류 없이 정상적으로 수행된다.
  >   - 만약, unit 레퍼런스 변수가 어떤 객체를 가리키고 있다고 가정할 때, 가리키는 객체의 실제 타입을 구분할 때 instanceof 를 사용한다.
  >
  >   ```Java
  >   class Unit {
  >       ...
  >   }
  >   
  >   class Zelot extends Unit {
  >       ...
  >   }
  >   
  >   class Marine extends Unit {
  >       ...
  >   }
  >   
  >   class Zergling extends Unit {
  >       ...
  >   }
  >   
  >   public class CastingTest {
  >       public static void main(String[] args) {
  >          	Unit unit1 = new Unit();
  >           Unit unit2 = new Zealot(); // 업캐스팅
  >           Unit unit3 = new Marine(); // 업캐스팅
  >           Unit unit4 = new Zergling(); // 업캐스팅
  >           
  >           if(unit1 instanceof Unit) { // true
  >               system.out.println("Unit 타입")
  >           }
  >           
  >           if(unit1 instanceof Zealot) { // false
  >          	 	system.out.println("Zealot 타입")
  >           }	
  >           
  >           if(unit2 instanceof Zergling) { // false
  >          	 	system.out.println("Zergling 타입")
  >           }	
  >           
  >           if(unit3 instanceof Marine) { // true
  >          	 	system.out.println("Marine 타입")
  >           }	
  >           
  >           if(unit4 instanceof Zergling) { // true
  >               system.out.println("Zergling 타입")
  >           }
  >       }
  >   }
  >   ```
  >
  >   - 사용 시 주의할 점은 instanceof 연산자는 객체에 대한 클래스 타입에만 사용할 수 있다.

<br/>

<br/>

## 예상질문❔

Q1) 업캐스팅이란 무엇인가?

A1) 서브 클래스가 슈퍼 클래스의 타입으로 형 변환된 것으로, 슈퍼클래스의 멤버에만 접근이 가능하다.

<br/>

Q2) 다운캐스팅이란 무엇인가?

A2) 업캐스팅 되었던 슈퍼클래스가 다시 본래의 서브클래스 형으로 돌아오는 것으로, 업캐스팅과 다르게 명시적 형변환이 필요하다.

<br/>

### Reference📖

- https://m.blog.naver.com/PostView.nhn?blogId=dlaxodud2388&logNo=221642221204&proxyReferer=https:%2F%2Fwww.google.com%2F
- https://madplay.github.io/post/java-upcasting-and-downcasting
- https://lbmmbl.tistory.com/29
- https://diaryofgreen.tistory.com/97
