# HTTP와 HTTPS

:writing_hand: *Assembled by Yunju Jang*

<!--🤝*Contributors : JiYoung Kwon*-->

<hr>

- HTTP 란?

  
  - HyperText Transfer Protocol
  - 인터넷에서 웹 서버와 사용자 컴퓨터에 설치된 웹 브라우저 사이에 문서를 전송하기 위한 통신 규약 (Protocol)이다.
- 인터넷에서 Hypertext를 전송하기 위해 사용되는 통신 규약이다.
  - 클라이언트가 80번 포트에서 서버에 연결하면 80번 포트에서 기다리고 있던 서버는 요청에 응답하면서 자료를 전송한다.
- Http는 정보를 텍스트로 주고 받는다. <small>네트워크에서 전송 신호를 인터셉트 하는 경우 데이터 유출이 발생할 수 있다. --> 이러한 취약점을 보완한 것이 Https이다.</small> 
  
  <br/>


  - Https란? 

    
      - Http + S (Secure Socket)
      - 기본 골격이나 사용 목적 등은 Http 와 거의 동일하지만, 데이터를 죽 받는 과정에 보안 요소가 추가된다. (Http와의 차이점)
      - SSL(Secure Socket Layer)라는 프로토콜을 이용하여 인터넷 상에서의 정보를 암호화한다.
      - Https를 사용하면 서버와 클라이언트 사이의 모든 통신 내용이 암호화된다.
      - 사용자 마다 다른 암호를 제공해야하기 때문에 어렵다.
    
    <br/>
    
- Http와 Https 의 비교


  - Http에 비해 보안 기능이 추가된 Https가 처리 속도가 더 느리다. <small>오늘 날에는 거의 차이를 느끼지 못한다.</small>
  - 사용자 정보를 웹 서버와 주고 받아야 하는 경우 Http는 정보 유출의 위험성이 있다.
  - 정보 공유 시 SEO에 의해 Https 를 이용하는 사이트가 우선 검색될 수 있다.
  - Https는 인증서를 발급하고 유지하기 위한 추가 비용이 발생하므로, 단순 정보 조회 등만을 처리한다면 Http를 이용하는 것이 좋다.

<br/>

<br/>

## 예상질문❔

Q1) Http와 Https의 차이는 무엇인가?

A1)  Http는인터넷에서 하이퍼텍스트를 전송하기 위한 통신 프로토콜이며 보안이 되지 않기 때문에 정보 유출의 위험이 있다. Https는 이에 보안 요소가 추가된 프로토콜이다. 사용자 정보등을 주고 받을 때에 암호화를 해주며, Http에 비해 보안 기능이 추가되었기 때문에 처리 속도가 약간 느리다.

<br/>

### Reference📖

- https://post.naver.com/viewer/postView.nhn?volumeNo=16561296&memberNo=1834
- https://jeong-pro.tistory.com/89
- https://mangkyu.tistory.com/98
