## Singleton 패턴

<br>

### <u>Singleton 패턴</u>

전역 변수를 사용하지 않고 객체를 하나만 생성하도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 디자인 패턴

* 생성(Creational) 패턴의 하나
* 하나의 인스턴스 만을 생성하는 책임이 있으며, getInstance()를 통해 모든 클라이언트에게 동일한 인스턴스를 반환하는 작업을 수행
* 생성자가 여러번 호출되어도, 실제로 생성되는 객체는 하나
* 최초 생성 이후 호출된 생성자는 최초에 생성한 객체를 반환한다.

~~~
생성(Creational)패턴의 하나

객체 생성에 관련된 패턴
객체의 생성과 조합을 캡슐화 해 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성을 제공한다.
~~~

#### Singleton 패턴의 구현

~~~java
public class SingleObj {
    // 외부에 제공할 자기 자신의 인스턴스
    private static SingleObj singleObj = null;
    // 외부에서 직접 생성하지 못하도록 private 선언
    private SingleObj(){ }
    // 오직 1개의 객체만 생성, 자신의 인스턴스를 외부에 제공
    public static SingleObj getInstance(){
        if( singleObj == null ){
            //Singleobj 인스턴스 생성
            singleObj = new SingleObj();
        }
        return singleObj;
    }
}
~~~

* 외부에서 객체를 생성할 수 없도록 생성자를 private으로 선언
* 외부에서 SingleObj 객체를 생성할 수 없으므로, 미리 생성된 자신을 반환할 수 있도록 getInstance() 메서드를 정의
* 생서자를 private으로 선언했기 때문에 객체를 생성할 수 없으므로, getInstance() 메서드가 클래스에 정의되도록 static 제어자를 사용
* static 메서드 / static 변수
  * 구체적인 인스턴스에 속하는 영역이 아니고 클래스 자체에 속함
  * 클래스의 인스턴스를 통하지 않고서도 메서드를 실행할 수 있고 변수를 참조할 수 있음
* getInstance() 메서드 호출 시
  * singleObj 변수에 객체가 할당되지 않으면(==null) 새로운 객체를 생성
  * singleObj 변수에 객체가 이미 있으면 그것을 그대로 반환

<br/>

### <u>Singleton 패턴을 사용하는 이유</u> 

* **메모리 낭비 방지**

  고정 메모리 영역을 얻으면서 한번의 new로 인스턴스를 사용하기 때문에 메모리가 낭비되지 않는다.

* **데이터 공유**

  싱글톤으로 만들어진 클래스의 인스턴스는 전역 인스턴스이기 때문에 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다.

* **성능**

  두번째 이용 시부터 객체 로딩 시간이 현저히 줄어 성능이 좋아진다.

<br/>

### <u>Singleton 패턴의 문제점</u> 

* Singleton Instance가 너무 많은 일을 하거나 많은 데이터를 공유시킬 경우, 다른 클래스의 인스턴스들 간에 결합도가 높아져 "개방-폐쇄 원칙"을 위배하게 된다. 이는 객체 지향 설계 원칙에 어긋나다는 것을 말한다.

* 멀티 쓰레드 환경에서 인스턴스가 1개 이상 생성되는 경우가 발생할 수 있음

  * 경합 조건(Rare Condition)을 발생시키는 경우

    1. SingleObj 인스턴스가 아직 생성되지 않았을 때, 쓰레드 1이 getInstance()의 if문을 실행 해 이미 인스턴스가 생성되었는지 확인

        `singleObj 변수는 null 상태`

    2. 쓰레드 1이 생성자를 호출해 인스턴스를 만들기 전, 쓰레드 2가 if문을 실행해 singleObj 변수가 null인지 확인 

       `singleObj 변수는 null + 인스턴스를 생성하는 생성자를 호출하는 코드를 실행하게 됨`

    3. 결과적으로 SingleObj클래스의 인스턴스가 2개 생성됨

  ~~~
  경합 조건(Rare Condition)
  
  메모리와 같은 동일한 자원을 2개 이상의 쓰레드가 이용하려고 경합하는 현상
  ~~~

#### 해결책

* 멀티 쓰레드 애플리케이션이 아닌 경우 문제가 되지 않음

* 멀티 쓰레드 환경에서 발생하는 문제 해결 방법

  1. 정적 변수에 인스턴스를 만들어 바로 초기화 하는 방법

     ~~~java
     //static 변수에 외부에 제공할 자기 자신의 인스턴스를 만들어 바로 초기화
     private static SingleObj singleObj = new Singleobj();
     ~~~

  2. 인스턴스를 만드는 메서드에 동기화 처리를 하는 방법

     ~~~java
     // 인스턴스를 만드는 메서드 동기화 (임계 구역)
     public synchronized static SingleObj getInstance(){
         if( singleObj == null ){
             singleObj = new SingleObj();
         }
         return singleObj;
     }
     ~~~

  3. 인스턴스를 만드는 메서드를 임계 구역으로 변경
     * 멀티 쓰레드 환경에서 동시에 여러 쓰레드가 getInstance 메서드를 소유하는 객체에 접근하는 것을 방지
     * synchronized 특성상 비교적 큰 성능저하가 발생

<br>

<br>

<br>

### REFERENCE

* https://github.com/fake-developers/1st/blob/KJY-02/KJY/%5BSW%5D%20Singleton%20%ED%8C%A8%ED%84%B4.md
* https://github.com/fake-developers/1st/blob/JYJ-02/JYJ/Singleton.md

