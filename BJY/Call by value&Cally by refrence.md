## Call by value & Call by reference

<br/>

* **메서드에서 인자값을 받을 때 어떤식으로 받아올 것인지에 대한 방식**을 나타낸다.
* JAVA의 경우, 함수에 전달되는 인자의 데이터 타입(기본자료형/참조자료형)에 따라 메서드 호출방식이 달라진다.
  * 기본 자료형 : call by value 로 동작 (int, short, long, float, double, char, boolean)
  * 참조 자료형 : call by reference 로 동작(Array, Class Instance)
    - 해당 객체의 주소값을 직접 넘기는 것이 아니라 객체를 가리키는 또 다른 주소값을 만들어서 넘긴다.

### <u>**Call by value**</u>

**메소드 호출 시에 사용되는 인자의 메모리에 저장되어 있는 값(value)을 복사하여 보낸다.**

→  int a =3 이라는 문구가 있으면 메소드에서 인자값을 받을 때 a라는 자체에 주소를 받는게 아니라 a의 값인 3을 받아 처리하는 방식이다. 

<br/>

![call_by_value(1)](https://user-images.githubusercontent.com/61674527/111074812-3b98fc80-8528-11eb-9622-5806bd45e153.jpg)

~~~java
//결과 값

비포
안녕잘가
에프터
안녕잘가
~~~

> 스왑 메소드가 받는 두 인자는 인자값에 주소 즉 인자 그자체를 받는 것이 아니라 인자의 값을 복사해서 받는다. 
>
> 즉 String one 에는 a에 값인 "안녕" 에 값이 (String 은 참조 변수 이므로 "안녕" 에 주소 값이 복사), 마찬가지로 two 에도 b의 주소가아닌 b값에 주소가 복사 되어진다.

![call_by_value(2)](https://user-images.githubusercontent.com/61674527/111074822-4784be80-8528-11eb-84a4-1e0d4453f46c.jpg)

이렇게 메인 메소드의 a, b와 swapS 메소드의 one two는 서로 같은 값을 참조할 뿐 이다.

<br/>

![call_by_value(3)](https://user-images.githubusercontent.com/61674527/111074832-510e2680-8528-11eb-81a3-67f5a1756d4e.jpg)

이렇게 메소드 내에서는 변화가 이루어 지지만 메소드가 닫히면 swapS에 있던 정보는 다 사라지므로 메인 메소드에 영향을 주지 못한다.

**만약 call by Reference 방식 이였으면 메소드내에서 one two가 a, b의 주소값을 받아 곧 a=one b=two 이고 메소드 수행으로 서로값이 바뀌니 메소드 수행을 하고 나서도 a, b가 바뀌어 있을 것이다.** 

### <u>Call by reference</u>

**메소드 호출 시 사용되는 인자 값의 메모리에 저장되어있는 주소(Address)를 복사하여 보낸다.** 

→ 값이 아니라 인자 그자체에 주소 값을 보낸다. 



![call_by_ref(1)](https://user-images.githubusercontent.com/61674527/111075193-2624d200-852a-11eb-94f4-7d795f3a38fb.jpg)

> 객체를 참조하는 주소를 매개변수로 넘겨줘 수행한 결과 값은 실제 swap이 이루어짐을 볼 수 있다.

![call_by_ref(2)](https://user-images.githubusercontent.com/61674527/111075202-2fae3a00-852a-11eb-9da2-c39a30b4a1ee.jpg)

one과 two는 값의 주소를 복사(Call by value)받아 같은 인스턴스를 참조하지만,

![call_by_ref(3)](https://user-images.githubusercontent.com/61674527/111075211-3a68cf00-852a-11eb-84b6-e609b3a527b4.jpg)

참조되어지는 값을 바꾸어서 해당 객체의 멤버변수에 접근하여 값을 바꿔 연산이 수행되는 것을 알 수 있다.

<br/>

***

**자바는 본형 타입 변수와 참조형 타입 변수가 있는데 ,둘 다 상관없이 call by value 방식으로 메소드에서 받아진다.** 

**대신 기본형 타입은 그 값을 복사 해서 주지만, 참조형 타입은 값의 래퍼런스(주소)가 저장되는 것이므로 그 값의  래퍼런스가 복사 되어진다.**

<br/>

<br/>

<br/>

### REFERENCE

* [call by value & call by reference(1)](https://sleepyeyes.tistory.com/11)
* [call by value & call by reference(2)](https://github.com/fake-developers/1st/blob/JYJ-07/JYJ/CallByValueAndReference.md)
* [call by value & call by reference(3)](https://github.com/fake-developers/1st/blob/SJH-07/SJH/Call%20by%20value%20vs%20Call%20by%20reference.md)

