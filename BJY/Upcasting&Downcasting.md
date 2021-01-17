## 업캐스팅(Upcasting) & 다운캐스팅(Downcasting)



### <u>캐스팅이란?</u>

타입을 변환하는 것을 말하며 **형변환**이라고도 한다.

* 데이터 손실을 막기 위해 다형성을 지켜주는 것
* 자바의 상속 관계에 있는 부모와 자식 클래스 간에는 서로간의 형변환이 가능하다.

<br/>

### <u>업캐스팅(Upcasting)</u>

**서브 클래스의 객체가 수퍼 클래스 타입으로 형변환 되는 것**

수퍼 클래스의 레퍼런스 변수가 서브 클래스로 객체화 된 인스턴스를 가리킬 수 있게 된다.

* 업캐스팅 시에는 명시적인 타입 캐스팅을 선언하지 않아도 된다.

~~~
ex) 사람은 생물이다.
사람 -> 서브 클래스
생물 -> 수퍼 클래스
~~~

![upcasting](https://user-images.githubusercontent.com/61674527/104850375-1629b100-5932-11eb-9b74-91422ffb3713.jpg)

> grade는 Person의 멤버가 아니므로 컴파일 오류

<br/>

### <u>다운캐스팅(Downcasting)</u>

**자신의 고유한 특성을 잃은 서브 클래스의 객체를 다시 복구 시켜주는 것**

* 업캐스팅 된 것을 다시 원상태로 돌리는 것
* 업캐스팅과 달리 명시적으로 타입을 지정해야 한다.
* 업캐스팅이 선행되어야 한다.

<img src="https://user-images.githubusercontent.com/61674527/104850397-29d51780-5932-11eb-8265-d6e14f0596e2.jpg" style="zoom: 67%;" />

![downcasting2](https://user-images.githubusercontent.com/61674527/104850405-36597000-5932-11eb-9b48-e6f8cc0e6c5a.jpg)

>  무분별한 다운캐스팅은 컴파일 시점에는 오류가 발생하지 않아도 런타임 오류를 발생시킬 가능성이 있다.  

<br/>

### <u>instanceof</u>

혼동되는 객체의 타입을 구분하기 위해 사용되는 연산자

* 결과 타입은 boolean이며 이항연산자처럼 사용한다.

~~~java
class Unit{
    //생략
}
class Zealot extends Unit{
    //생략
}
class Marine extends Unit{
    //생략
}
class Zergling extends Unit{
    //생략
}

public class CastingTest{
    public static void main(String[] args){
        Unit unit1 = new Unit();
        Unit unit2 = new Zealot(); //업캐스팅
        Unit unit3 = new Marine(); //업캐스팅
        Unit unit4 = new Zergling(); //업캐스팅
        
        if(unit1 instanceof Unit){ //true
            System.out.println("unit1은 Unit 타입이다.");
        }
        if(unit1 instanceof Zealot){ //false
            System.out.println("unit1은 Zealot 타입이다.");
        }
        if(unit2 instanceof Zealot){ //true
            System.out.println("unit2는 Zealot 타입이다.");
        }
        if(unit2 instanceof Zergling){ //false
            System.out.println("unit2는 Zergling 타입이다.");
        }
        if(unit3 instanceof Unit){ //true
            System.out.println("unit3은 Unit 타입이다.");
        }
        if(unit4 instanceof Zergling){ //false
            System.out.println("unit4는 Zergling 타입이다.");
        }
        
    }
}
~~~

<br/>

<br/>

<br/>

### REFERENCE

* [캐스팅](https://m.blog.naver.com/PostView.nhn?blogId=dlaxodud2388&logNo=221642221204&proxyReferer=https:%2F%2Fwww.google.com%2F)
* [캐스팅(2)](https://mommoo.tistory.com/40)
* [instanceof](https://woochan-autobiography.tistory.com/201)
* [명품Jjava](https://slidesplayer.org/slide/14701469/)

