# Call by value와 Call by reference

- Call by value와 Call by reference는 **메서드에서 인자값을 받을 때 어떤식으로 받아올 것인지에 대한 방식**을 나타낸다.
- Call by value는 값에 의한 호출, Call by reference는 참조에 의한 호출을 뜻한다.
- JAVA의 경우, 함수에 전달되는 인자의 **데이터 타입(기본자료형/참조자료형)에 따라 메서드 호출방식이 달라짐 **
  - 기본 자료형 : call by value 로 동작 (int, short, long, float, double, char, boolean)
  - 참조 자료형 : call by reference 로 동작(Array, Class Instance) 
    - 해당 객체의 주소값을 직접 넘기는 것이 아니라 객체를 가리키는 또 다른 주소값을 만들어서 넘긴다.
  - 데이터 타입에 대한 더 자세한 내용은 [여기](Java%20Primitive%20type%20&%20Reference%20type.md)를 클릭.
- 결과적으로 **자바 내에서 메서드의 기본 형식은 Call by Value로 동작**한다.

<br>

## Call by value

- 값에 의한 호출

- **메서드 호출 시에 사용되는 인자의 메모리에 저장되어 있는 값(value)을 복사**하여 보낸다.

  - 복사된 인자는 함수 안에서 지역적으로 사용된다.

- ex_) 1. 기본 자료형 call by value

  ~~~java
  Class CallByValue{
      public static void swap(int x, int y){
  		int temp = x;
          x = y;
          y = temp;
      }
      
      public static void main(String[] args) {
          int a = 10;
  		int b = 20;
          
          System.out.println("swap() 호출 전 : a = " + a + ", b = " + b);
          swap(a, b);
          System.out.println("swap() 호출 후 : a = " + a + ", b = " + b);
      }
  }
  ~~~

  ~~~
  <실행결과>
  swap() 호출 전 : a = 10, b = 20
  swap() 호출 후 : a = 10, b = 20
  ~~~

  - 위와 같이 int 기본 타입의 값을 매개변수로 받아 두 매개 변수의 값을 swap 한 후 출력하는 코드를 보면 결과 값은 swap 되기 전의 값으로 그대로 출력이 된다.

    <img src="https://user-images.githubusercontent.com/58902042/110285270-55b57500-8026-11eb-9e26-a97feeb34b8b.png" height=280> 

    - swap()메서드 호출시에 사용한 인자 a,b와 swap() 메서드내의 매개변수 x,y는 서로 다르기 때문이다.

- ex_) 2. 참조 자료형 call by value

  ~~~java
  public class SwapTest {
      public static void swap(Integer one, Integer two) {
          Integer tmp = one;
          one = two;
          two = tmp;
      }
   
      public static void main(String[] args) {
          Integer a = new Integer(1);
          Integer b = new Integer(2);
   
          System.out.println(a.intValue() + " " + b.intValue());
          swap(a, b);
          System.out.println(a.intValue() + " " + b.intValue());
      }
  }
  ~~~

  ~~~
  <실행결과>
  1,2
  1,2
  ~~~

  - 위와 같이 참조형 타입인 Integer을 이용해 객체를 매개변수로 받아 두 매개 변수의 값을 swap 한 후 에도 결과 값은 swap 되기 전의 값으로 그대로 출력이 된다.

    <img src="https://user-images.githubusercontent.com/58902042/111024805-01decd80-8424-11eb-9d80-d148bd080001.png" height=210> 

    - Call by reference는 맞지만 메서드 호출을 할 때 새로운 reference를 만들어 복사해 호출하기 때문이다. 

    <img src="https://user-images.githubusercontent.com/58902042/111024804-01463700-8424-11eb-85aa-c898ddbaa37a.png" height=210> 

    - 위의 그림에서 볼 수 있듯이 객체를 호출하지만, 객체의 자체를 복사해서 리턴하므로 객체의 값을 swap하는 것으로 안의 원본 값을 바꿀 수 없다.

- 즉, Call of Value는 값을 직접 전달 받기 때문에 실제 swap을 해 값을 변경했다 하더라도 **원본 데이터는 바뀌지 않고, 단순히 복사된 값을 바꾸는 것에 불과하다**

<br>

## Call by reference

- 주소에 의한 호출

- **메서드 호출 시 사용되는 인자의 메모리에 저장되어있는 주소값(address)을 복사**하여 보낸다.

  - 즉,  주소값을 통해 해당 변수를 가리킨다.

- ex_)

  ~~~java
  Class CallByReference{
      int value;
      
      CallByReference(int value) {
          this.value = value;
      }
  
      public static void swap(CallByReference one, CallByReference two) {
          int temp = one.value;
          one.value = two.value;
          two.value = temp;
      }
  
      public static void main(String[] args) {
          CallByReference a = new CallByReference(10);
          CallByReference b = new CallByReference(20);
  
          System.out.println("swap() 호출 전 : a = " + a.value + ", b = " + b.value);
  		swap(a, b);
          System.out.println("swap() 호출 전 : a = " + a.value + ", b = " + b.value);
      }
  }
  ~~~

  - 객체를 참조하는 주소를 매개변수로 넘겨줘 수행한 결과 값은 실제 swap이 이루어짐을 볼 수 있는데, 

     <img src="https://user-images.githubusercontent.com/58902042/110288792-df1b7600-802b-11eb-8220-eb3ccd95889d.png" height=200> 

    - one과 two는 값의 주소를 복사(Call by value)받아 같은 인스턴스를 참조하지만,

    <img src="https://user-images.githubusercontent.com/58902042/110289119-505b2900-802c-11eb-89e0-832180142707.png" height=200> 

    - 참조되어지는 값을 바꾸어서 해당 객체의 멤버변수에 접근하여 값을 바꿔 연산이 수행되는 것을 알 수 있다.

--------

**<참조>**

- [[자바[java] Call by value Call by reference](https://sleepyeyes.tistory.com/11)]
- [[Java] Call By Value와 Call By Reference](https://nathanh.tistory.com/119)
- [[JAVA]Call by Value 와 Call by reference 란 ?](https://devlog-wjdrbs96.tistory.com/44)
- [[Java] Call by value와 Call by reference](https://re-build.tistory.com/3)