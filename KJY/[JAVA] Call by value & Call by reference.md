# [JAVA] Call by value & Call by reference

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-14)* 



#### :pushpin: call by value와 call by reference

- **메서드에서 인자값을 받을 때 어떤식으로 받아올 것인지에 대한 방식**
- Call by value : 값에 의한 호출
- Call by reference : 참조에 의한 호출
- JAVA의 경우, 함수에 전달되는 인자의 **데이터 타입(기본자료형/참조자료형)에 따라 메서드 호출방식이 달라짐**
  - 기본 자료형 : call by value 로 동작 (int, short, long, float, double, char, boolean)
  - 참조 자료형 : call by reference 로 동작 (Array, Class Instance)
    - 해당 객체의 주소값을 직접 넘기는 것이 아니라 객체를 가리키는 또 다른 주소값을 만들어서 넘김
- 결과적으로 **자바 내에서 메서드의 기본 형식은 Call by Value로 동작** - [3. 참고]

<br/>

#### :pushpin: 메모리 상에서의 변수

[![img](https://github.com/fake-developers/1st/raw/JYJ-07/JYJ/resources/memory.png)](https://github.com/fake-developers/1st/blob/JYJ-07/JYJ/resources/memory.png)

- 기본 타입의 경우 - 변수에 실제 값을 저장해 스택에서만 존재

- 참조 타입의 경우 - 힙 영역에 생성되고, 변수에는 힙 영역에 있는 참조 타입의 주소가 저장됨

- 참조 변수 - 비교 연산

  ```java
  int[] a = {1, 2, 3};
  int[] b = {1, 2, 3};
  
  a == b // false
  a != b // true
  ```

  - 배열은 참조 타입
    - 실제 변수에 저장된 값은 배열 객체의 주소값
    - a와 b는 실제 다른 객체가 생성이 된 주소의 값들이 저장됨

- String 타입

  - String 타입은 참조 타입 중 **주의해야 할 타입**

  - 문자열 타입의 경우 **문자열 리터럴 (값)이 동일하다면 String 객체가 공유됨**

    ```java
    String a = "nathan";
    String b = "nathan";
    String c = new String("nathan");
    
    a == b // true
    a == c // false
    a.equals(c) // true
    ```

    - a, b에 같은 값을 저장하고 비교 연산을 수행하면 기본 타입에 의한 결과가 나옴

    - new 연산자로 새로운 String 객체를 생성하여 저장하면 **참조 타입**에 의한 결과가 나옴

* **참조 타입에 대해 비교 연산을 수행할 때에는 equals 메소드를 통해 수행하는 것이 좋음**

<br/>

## 1. Call by value

- 값에 의한 호출
- **메서드 호출 시, 사용되는 인자의 메모리에 저장되어 있는 값(value)을 복사**하여 보냄
  - 복사된 인자는 함수 안에서 **지역적** 으로 사용됨

#### 1-1. 예시

- 1) 기본 자료형 call by value

  ```java
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
  ```

  ```
  <실행결과>
  swap() 호출 전 : a = 10, b = 20
  swap() 호출 후 : a = 10, b = 20
  ```

  - 결과 값 : swap 되기 전의 값으로 그대로 출력 됨

    ![img](https://user-images.githubusercontent.com/58902042/110285270-55b57500-8026-11eb-9e26-a97feeb34b8b.png)

    - swap() 메서드 호출 시에 사용한 인자 a,b와 swap() 메서드 내의 매개변수 x,y는 서로 다르기 때문

<br/>

- 2) 참조 자료형 call by value

  ```java
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
  ```

  ```
  <실행결과>
  1,2
  1,2
  ```

  - 결과 값 : swap 되기 전의 값으로 그대로 출력 됨

    ![img](https://user-images.githubusercontent.com/58902042/111024805-01decd80-8424-11eb-9d80-d148bd080001.png)

    - Call by reference는 맞지만 메서드 호출을 할 때 **새로운 reference를 만들어 복사해 호출하기 때문**

    ![img](https://user-images.githubusercontent.com/58902042/111024804-01463700-8424-11eb-85aa-c898ddbaa37a.png)

    - 객체를 호출하지만, **객체의 자체를 복사해서 리턴** 하므로 객체의 값을 swap하는 것으로 **안의 원본 값을 바꿀 수 없음**

<br/>

- 즉, **Call of Value** 는 값을 직접 전달 받기 때문에 실제 swap을 해 값을 변경했다 하더라도 **원본 데이터는 바뀌지 않고, 단순히 복사된 값을 바꾸는 것에 불과함**

<br/>

## 2. Call by reference

- 주소에 의한 호출
- **메서드 호출 시 사용되는 인자의 메모리에 저장되어있는 주소값(address)을 복사**하여 보냄
  - 즉, 주소값을 통해 해당 변수를 가리킴

#### 2-1. 예시

- ```java
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
  ```

  - 결과 값 : 실제 swap이 이루어짐

    ![img](https://user-images.githubusercontent.com/58902042/110288792-df1b7600-802b-11eb-8220-eb3ccd95889d.png)

    - one과 two는 값의 주소를 복사(Call by value)받아 같은 인스턴스를 참조하지만

    ![img](https://user-images.githubusercontent.com/58902042/110289119-505b2900-802c-11eb-89e0-832180142707.png)

    - **참조되어지는 값을 바꾸어서** 해당 객체의 멤버변수에 접근하여 값을 바꿔 연산이 수행되는 것을 알 수 있음

<br/>

## 3. Call by value 와 Call by reference 를 통한 중요한 자바의 특징

![javaMemory.png](https://github.com/fake-developers/1st/blob/JYJ-07/JYJ/resources/javaMemory.png?raw=true)

- 자바는 해당 지역변수가 가리키고 있는 힙 영역의 객체를 가리키는 새로운 지역변수를 생성하고 그 것을 통해 **같은 객체를 가리키도록 하는 방식**
  - 객체(참조 타입)를 메서드로 넘길 때 참조하는 지역 변수의 실제 주소를 넘기는 것이 아님

* 기본 타입을 매개변수로 받아 값을 바꾼 경우, 참조타입을 매개변수로 받아 값을 변경한 경우 **모두 스택에서 변경이 이루어지기 때문에 아무런 의미가 없음**

- 결국, 기본적으로 **자바에서의 메소드 호출은 참조, 기본형 모두 Call By Value를 따르고 있음**
  - 객체의 경우, 객체를 가리키는 주소 값을 넘겨 새로운 지역변수를 통해 Call By Value로 객체를 참조해 모든 메소드와 필드를 호출해 실행이 됨

<br/>

## :page_with_curl: Reference

[[자바[java] Call by value Call by reference](https://sleepyeyes.tistory.com/11)

[[Java] Call By Value와 Call By Reference](https://nathanh.tistory.com/119)

[[JAVA]Call by Value 와 Call by reference 란 ?](https://devlog-wjdrbs96.tistory.com/44)

[[Java] Call by value와 Call by reference](https://re-build.tistory.com/3)

https://sleepyeyes.tistory.com/11

https://devlog-wjdrbs96.tistory.com/44

https://nathanh.tistory.com/119

https://siyoon210.tistory.com/104

https://re-build.tistory.com/3
