## CSR과 SSR의 차이



~~~
Rendering(랜더링)

어떠한 웹 페이지 접속 시, 그 페이지를 화면에 그려주는 것.
~~~



### <u>SPA & MPA</u>

#### SPA(Single Page Application)

서버로부터 처음에만 페이지를 받아오고 이후에는 동적으로 페이지를 구성해서 새로운 페이지를 받아오지 않는 웹 애플리케이션.

- 페이지가 한번 로딩 된 이후 데이터를 수정하거나 조회할 때, 페이지가 새로고침되지 않고 다른 페이지로 넘어가지 않음.
- 사용자 친화적
- 상대적으로 서버 요청이 작음
- 개발이 상대적으로 효율적
- Front-End 와 Back-End 분리로 개발 업무 분업화 및 협업 용이
- SPA에서 기본적으로 CSR 방식을 사용한 것. (둘은 같은 것이 아니다.)

#### MPA(Multi Page Application)

서버로부터 완전한 페이지를 받아오고 이후에 데이터를 수정하거나 조회할 때, 다른 완전한 페이지로 이동한다. 

* URL이 바뀔 수 있음.
* MPA에서 SSR 방식을 사용한 것.



### <u>CSR</u>

최초에 서버에서 한 번 관련파일을 모두 로딩 한 후, 사용자의 요청이 올 때마다 리소스를 서버에 제공하여 클라이언트가 해석하고 랜더링 하는 방식

![csr1](https://user-images.githubusercontent.com/61674527/104108645-c0d61a00-5309-11eb-9ca9-7f843daddaf2.jpg)

![csr2](https://user-images.githubusercontent.com/61674527/104108650-cd5a7280-5309-11eb-86ed-c005c48e1113.jpg)

* #### 장점

  * 첫 로딩에 HTML과 같은 static 파일들만 다 받으면, 동적으로 빠르게 랜더링 
  * 서버와 클라이언트 간의 데이터 양과 트래픽 현저히 감소

* #### 단점

  * <u>SEO 문제가 발생</u>
  * 모든 HTML과 static 파일이 로드될 때까지 기다려야하기 때문에 초기 랜더링이 느림



### <u>SSR</u>

서버에서 랜더링을 마치고, data가 결합된 (완성된) HTML 파일을 내려주는 방식
요청시마다 새로고침이 일어나며 서버에 새로운 페이지에 대한 요청을 하는 방식

![ssr](https://user-images.githubusercontent.com/61674527/104108660-dd725200-5309-11eb-9d56-c765f9166b2e.jpg)

* #### 장점

  * 초기 로딩 속도가 빨라 사용자가 콘텐츠를 빨리 볼 수 있음
  * 모든 검색엔진에 대한 <u>SEO가 가능함</u>.

* #### 단점

  * 매번 페이지를 요청할 때마다 새로고침 됨
  * 서버에 매번 요청을 하기에 트래픽, 서버 부하가 커짐



### <u>CRS VS SSR</u>

![csr_ssr](https://user-images.githubusercontent.com/61674527/104108676-eb27d780-5309-11eb-9e3e-2c752a7bffdb.jpg)

|                    |                   CSR                   |       SSR        |
| :----------------: | :-------------------------------------: | :--------------: |
| **초기 로딩 속도** |                오래걸림                 |   속도가 빠름    |
|   **서버 부담**    |               부담이 적음               |    부담이 큼     |
|      **SEO**       | 데이터 수집 불가능<br />(단, 구글 제외) | 데이터 수집 가능 |



### <u>SEO(Search Engine Optimization)</u>

Naver, Daum, Google 과 같은 검색엔진이 퍼블리싱한 웹사이트를 잘 읽도록 검색엔진에 최적화 하는 기술을 말한다.  CSR에서는 불가능 하고 SSR에서는 가능하다.

공식 홈페이지와 같이 일반 사용자에게 검색되어야 하는 사이트라면 SEO를 고려해야한다.
따라서 SSR과 CSR을 적절히 활용해야한다.





### REFERENCE

* https://github.com/fake-developers/1st/blob/KJY-01/KJY/%5BWEB%5D%20CSR%EA%B3%BC%20SSR%20%EC%B0%A8%EC%9D%B4.md
* https://github.com/fake-developers/1st/blob/SJH-01/SJH/CSR%26SSR%20Difference.md
* https://velog.io/@ru_bryunak/SPA-%EC%82%AC%EC%9A%A9%EC%97%90%EC%84%9C%EC%9D%98-SSR%EA%B3%BC-CSR
* https://medium.com/%EC%95%84%EB%AA%BD%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4/csr-ssr-spa-mpa-ede7b55c5f6f
* https://kim-mj.tistory.com/275