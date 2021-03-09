## Boxing(박싱) 과 Unboxing(언박싱)

<br/>

### <u>Wrapper 클래스</u>

* 기본 자료형(int, double, boolean 등)의 데이터를 인스턴스 (객체)로 만들기 위해 사용(포장)하는 클래스

#### 사용이유

* 제네릭, 자료구조, 매개변수 등 기본 자료형이 아닌 레퍼런스 타입을 필요로 하는 경우가 많고 메서드를 갖고 있어 다양하게 활용이 가능하기 때문이다. 
  * Map<String,Integer> → O  , Map<String,int> → X
*  인스턴스를 생성(heap 메모리에 저장) 하여 상속 및 재사용이 가능하다.
* 클래스가 제공하는 상수 사용(MIN_VALUE and MAX_VALUE)
* 문자열(String)과 기본 자료형 간 형 변환하여 사용이 가능하다.

#### 종류

우리가 사용하는 기본 자료형의 모든 wrapper 클래스를 자바에서 기본적으로 제공하여 주며, java.lang 패키지에 소속되어 있다. 대부분 기본 데이터 타입의 앞 글자를 대문자로 변경해주면 된다.

![wrapperclass](https://user-images.githubusercontent.com/61674527/110437423-b90fd780-80f8-11eb-9090-9fc7c4a647d8.png)

<br/>

### <u>Boxing(박싱)</u>

* 기본 자료형의 데이터를 래퍼(wrapper) 클래스의 객체로 만드는 과정

![String](https://user-images.githubusercontent.com/61674527/110447927-0fcede80-8104-11eb-9e8a-c384ab70bd74.png)

<br/>

~~~java
public static void main(String[] args) {
    int intData = 512;
    
    //박싱(boxing)
    Integer integerData = new Integer(intData);
    System.out.println(integerData);
    
    System.out.println(intData == integerData); //true
}
~~~

<br/>

#### 묵시적인 박싱

* 프로그래머가 임의로 박싱을 해주는 것이 아니라 자동으로 박싱이 되는 것을 말한다.

~~~java
public static void main(String[] args) {
    int intData = 512;
 
    // 묵시적인 방식
    Integer integerData = intData;
    System.out.println(integerData);
    
}
~~~

#### 명시적인 박싱

* 프로그래머가 코딩하여 명시적으로 wrapper로 변환하는 것

~~~java
public static void main(String[] args) {
    int intData = 512;
 
    // 명시적인 방식
    Integer integerData = (Integer)intData;
    System.out.println(integerData);
    
}
~~~

<br/>

### <u>Unboxing(언박싱)</u>

* 래퍼(wrapper) 클래스의 데이터를 기본 자료형으로 얻어내는 과정

~~~java
public static void main(String[] args) {
    int intData = 512;
    
    //박싱(boxing)
    Integer integerData = new Integer(intData);
    System.out.println(integerData);
    
    //언박싱(unboxing)
    int intData2 = integerData.intValue();
    System.out.println(intData2);
    
    System.out.println(intData == intData2); //true
}

~~~

<br/>

#### 묵시적인 언박싱

* 코드상 프로그래머가 임의로 언박싱을 하는 것이 아니라 자동으로 언박싱이 되는 현상을 말한다.

~~~java
public static void main(String[] args) {
    int intData = 512;
 
    // 묵시적인 방식
    Integer integerData = intData;
    System.out.println(integerData);
    
    // 묵시적인 언방식
    int sum = integerData + 100;
    System.out.println(sum);
}
~~~

<br/>

### 명시적인 언박싱

~~~java
public static void main(String[] args) {
    int intData = 512;
 
    // 명시적인 방식
    Integer integerData = (Integer)intData;
    System.out.println(integerData);
    
    // 명시적인 언방식
    int sum = (int)integerData + 100;
    System.out.println(sum);
}
~~~

<br/>

<br/>

<br/>

### REFERENCE

* [Boxing&Unboxing(1)](http://blog.naver.com/PostView.nhn?blogId=heartflow89&logNo=220975218499&redirect=Dlog&widgetTypeCall=true)
* [Boxing&Unboxing(2)](https://ktko.tistory.com/entry/%EC%9E%90%EB%B0%94-%EB%B0%95%EC%8B%B1boxing%EA%B3%BC-%EC%96%B8%EB%B0%95%EC%8B%B1unboxing)

