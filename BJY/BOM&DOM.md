## BOM



### <u>BOM이란?</u>

웹 서비스 개발은 브라우저와 밀접한 관련이 있다. 모든 서비스(뒤로가기, 북마크, 즐겨찾기, 히스토리 등...)는 사실 브라우저를 바탕으로 실행되기 때문이다. 이때 브라우저와 관련된 객체들의 집합을 **Browser Object Model** 이라고 부른다.



### <u>BOM을 구성하는 객체</u>

* **[window object]** : 최상위 객체로, 각 프레임별로 하나씩 존재한다.
* **[navigator object]** : 브라우저명과 버전정보를 속성으로 가진다.
* **[screen object]** : 브라우저의 외부환경에 대한 정보를 제공한다.
* **[history]** : 현재의 브라우저가 접근했던 URL history.
* **[location object]** : 현재 URL에 대한 정보. 브라우저에서 사용자가 요청하는 URL.
* **[document object]** : 브라우저 윈도우에 로드된 웹페이지나 document의 method, propertioes 조작하기 위해 사용되는 객체. BOM의 중요한 부분을 구성한다.



## DOM



### <u>DOM이란?</u>

**Document Object Model** 의 약자이다. 문서에 대한 모든 내용을 담고있는 객체이다. 도큐먼트에 관련 된 내용 모두 문서, 즉 열려진 페이지에 대한 정보를 따로 객체화 시켜서 관리한다.



### <u>DOM의 종류</u>

W3C DOM 표준은 세가지 모델로 구문된다.

* **Core DOM** : 모든 문서 타입을 위한 DOM 모델
* **HTML DOM** : HTML 문서 타입을 위한 DOM 모델
* **XML DOM **: XML 문서 타입을 위한 DOM 모델

### <u>DOM tree</u>

DOM은 웹 문서의 요소를 부모 요소와 자식 요소로 구분하여 계층적 구조로 인식한다. DOM의 트리 구조는 노드와 가지로 표현한다. 노드는 웹 문서의 HTML 태그 요소만 표현 하는 것이 아니다. 모든 텍스트와 이미지, 태그의 속성들 까지 객체화 하여 DOM tree에 표현한다.

![dom_tree](C:\Users\jyb63\Desktop\취업스터디\1st\BJY\resource\dom_tree.jpg)

#### - 문서 노드 (Document Node)

트리의 최상위에 존재하며, 하위 자식 노드에 접근하기 위해서는 Document Node를 통해야 한다. Dom tree의 접근하기 위한 시작점이다.

#### - 요소 노드 (Element Node)

웹 문서의 태그는 Element Node로 표현된다. 모든 Element Node는 Attribute Node와 Text Node를 자식으로 가질 수 있는데, 자식 노드를 변경하여 웹 페이지를 동적으로 조작할 수 있다. 쉽게 말하면 태그이다.

~~~
<p>,<div>,<span> 등...
~~~

#### - 속성 노드 (Attribute Node)

태그의 모든 속성은 Attribute Node로 표현하며 해당 태그의 자식 노드로 인식된다. 

~~~
<input>태그 안에서 name, value 등의 속성을 사용할 수 있음.
이러한 속성들을 가리키는 노드이다.
~~~

#### - 텍스트 노드 (Text Node)

태그 내 텍스트를 표현한다. Text Node는 자신의 자식 노드를 가질 수 없기 때문에 Dom tree의 최종단이다. 

~~~
<span>안녕</span>일 경우 텍스트 노드는 '안녕'이다.
~~~

