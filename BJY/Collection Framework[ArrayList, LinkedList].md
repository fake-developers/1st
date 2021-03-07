## Collection Framework[ArrayList, LinkedList]

<br/>

### <u>List 컬렉션</u>

* 인덱스 순서로 저장이 되며, 중복된 데이터가 저장이 가능하다.
* 구조적으로 데이터를 일렬로 늘여놓는 구조를 갖는다. 
* 객체(데이터 등)를 저장하면 인덱스가 자동으로 부여되고 부여된 인덱스를 통해 데이터의 검색 및 삭제가 가능하다.(인덱스에는 데이터가 저장되어 있는 참조 값을 갖는다.) 
* List 컬렉션을 구현하는 대표적인 클래스들을 ArrayList, Vector, LinkedList가 있다. 
* List 인터페이스를 구현하는 클래스들이기 때문에 공통적으로 사용할 수 있는 메서드들이 많다. 

<br/>

### <u>ArrayList</u>

ArrayList는 List 인터페이스를 구현한 클래스이다. 설정된 저장 용량(capacity)보다 많은 데이터가 들어오면 자동으로 용량이 늘어난다. ArrayList를 생성하는 방법은 아래와 같다.

>  **List<E> 객체명 = new ArrayList<E>([초기 저장용량]);**

초기 저장용량을 생략하면 **본적으로 10의 저장용량**을 갖는다. **E는 제네릭 타입을 의미하는데 생략하면 Object 타입**이 된다. Object는 모든 데이터 타입을 저장 가능하지만 데이터를 추가하거나 검색할때 형 변환을 해야 한다. 자료구조에는 주로 **동일한 데이터 타입을 저장하기 때문에 제네릭 타입을 지정하고 사용하는 것이 좋다.** 기본적으로 데이터를 추가할 때는 인덱스 순으로 자동 저장된다. 이때 **중간에 데이터를 추가하거나 삭제할 경우에는 인덱스가 한 칸씩 뒤로 밀리거나 당겨진다.**

<br/>

![ArrayList 주요 메소드](https://user-images.githubusercontent.com/61674527/109425235-b3483100-7a2a-11eb-8bd6-e7741ca48845.png)

<br/>

#### 예제

~~~~java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class ArrayListEx01 {

	public static void main(String[] args) {
		List<String> list = new ArrayList<String>();
		list.add("리스트1"); // 0번 index에 데이터 추가
		list.add("리스트2"); // 1번 index에 데이터 추가
		list.add("리스트3"); // 2번 index
		list.add("리스트4"); // 3번 index
		list.add(1, "리스트5"); // 1번 index에 데이터 추가(기존의 1번 이후의 인덱스들이 하나씩 뒤로 밀림)
		list.add("리스트6"); // 5번 index

		System.out.println(list.size()); // 저장된 데이터 용량 출력 : 6

		System.out.println(list.get(0)); // 0번 index 값 출력
		System.out.println(list.get(1)); // 1번 index 값 출력

		System.out.println();

		for (int i = 0; i < list.size(); i++) { // 반복문 이용 데이터 출력
			System.out.println(i + "번 인덱스 데이터 : " + list.get(i));
		}

		System.out.println();

		list.remove(0); // 0번 index 삭제(하나씩 앞으로 당겨짐)
		list.remove("리스트5"); // 리스트5를 갖는 데이터 삭제(이후의 데이터들은 하나씩 앞으로 당겨짐)

		for (String value : list) { // for each 반복문 이용 데이터 출력
			System.out.println(value);
		}

		System.out.println();

		Iterator<String> elements = list.iterator(); // Iterator (반복자)
		while (elements.hasNext()) { // Iterator 이용 데이터 출력 / hasNext : 데이터가 있으면 true 없으면 false 리턴
			System.out.println(elements.next()); // next() 다음 데이터 리턴
		}
	}
}
~~~~

<br/>

### <u>LinkedList</u>

List의 구현 클래스이므로 ArrayList와 **사용 방법은 동일**하다. 하지만 **구조는 다르게 구성**되어있다. **LinkedList는 인접합 곳을 링크하여 체인처럼 관리**한다. LinkedList는 중간의 데이터를 삭제할 때 인접한 곳의 링크만을 변경하면 되기 때문에 **중간에 데이터를 추가/삭제하는 경우 처리 속도가 빠르다. ** LinkedList를 생성하는 방법은 아래와 같다.

> **List<E> list = new LinkedList<E>();**

<br/>

![LinkedList 주요 메소드](https://user-images.githubusercontent.com/61674527/109425247-be9b5c80-7a2a-11eb-8c0b-5428516b1d12.png)

#### 종류

* **단일 연결리스트(Singly LinkedList)**

  각 노드에 자료 공간과 한 개의 포인터 공간이 있고, 각 노드의 포인터는 다음 노드를 가리킨다.

* **이중 연결리스트(Doubly LinkedList)**

  구조는 단일 연결리스트와 비슷하지만, 포인터 공간이 두 대가 있고 각각의 포인터는 앞의 노드와 뒤의 노드를 가리킨다.

* **원형(환형) 연결리스트(Circular LinkedList)**

  일반적인 연결리스트에 마지막 노드와 처음 노드를 연결시켜 원형으로 만든 구조이다.

* **이중 원형(환형) 연결리스트(Doubly Circular LinkedList)**

  이중 연결리스트의 마지막 노드와 처음 노드를 연결시켜 원형으로 만든 구조이다.

<br/>

#### 예제

~~~java
class A {
    // 필드
    int n;
    String s;
    // 생성자
    public A(int n, String s) {
        this.n = n;
        this.s = s;
    }
    // 메서드
    void output() {
        System.out.println("num : " + n + ", s : " + s);
    }
}
// Main
public static void main(String[] args) {
    LinkedList<A> list = new LinkedList<A>();
        
    list.add(new A((int)(Math.random()*100) % 100, "호랑이"));
    list.add(new A((int)(Math.random()*100) % 100, "코끼리"));
    list.add(new A((int)(Math.random()*100) % 100, "독수리"));
    list.add(new A((int)(Math.random()*100) % 100, "맘모스"));
    list.add(new A((int)(Math.random()*100) % 100, "코뿔소"));
        
    System.out.println("정렬 전");
    for (A item : list) {
        item.output();
    }
    
    System.out.println("----------------------------------");
}
Collections.sort(list, new Comparator<A>() {
            // compare 함수를 사용하여 정렬을 어떻게 할 것인지 정의한다.
            @Override
            public int compare(A o1, A o2) {
                // 순차 정렬을 해주는 코드(역방향은 부등호를 변경하거나 return 값을 바꿔주면 됨)
                // if-else 동등의 개념을 포함 , -1이 있기 때문에 +1로 적어서 동등하게 맞춰준다.
                if(o1.n > o2.n) // if(o1.n < o2.n) : 역순
                    return +1;    // 양수의 대명사를 +1이라고 본다.
                else
                    return -1;
 
            }
        });


~~~





### <u>ArrayList와 LinkedList의 성능 비교</u>

|                           비교항목                           |                  ArrayList                  |     LinkedList     |
| :----------------------------------------------------------: | :-----------------------------------------: | :----------------: |
| Element(Object)를 이용한 검색<br />[contains()]/삭제[remove()] |                    O(n)                     |        O(n)        |
|               index를 통한 Random 접근(get())                |                    O(1)                     |        O(n)        |
|             index를 통한 삽입/삭제 - List의 중간             |                    O(n)                     |        O(n)        |
|                Iterator를 통한 반복 중 1스탭                 |                    O(1)                     |        O(1)        |
|           Iterator를 통한 삽입/삭제 - List의 중간            |                    O(n)                     |        O(1)        |
|                             개요                             | Dynamic (a.k.a. growable & resizable) array | Doubly-linked list |
|                  삽입/삭제 - 마지막 Element                  |           amortized O(1) [대부분]           |        O(1)        |
|                   삽입/삭제 - 최초 Element                   |                    O(n)                     |        O(1)        |

<br/>

<br/>

<br/>

### REFERENCE

* [List 컬렉션](https://oper6210.tistory.com/35)
* [List 컬렉션2](https://hwan1001.tistory.com/5)
* [LinkedList](https://hwan1001.tistory.com/11)

