## 2022-07-26 13:24  

## 주제 :
----
## 공부한 포인트
목차 
1. 인터넷
2. TCP/IP 계층
3. TCP/IP 흐름
4. 신뢰할 만한 TCP/IP

#### TCP/IP의 계층
**TCP/IP** 란 인터넷에서 컴퓨터들이 서로 정보를 주고 받는데 쓰이는 프로토콜의 집합


1. #application_layer : 특정 서비스 제공위해 어플리케이션 끼리 정보를 주고 받는 것 (FTP,HTTP,SSH,Telnet,DNS)
2. #transport_layer: 송신된 데이터를 수신측 어플에 확실하게 전달 (TCP,UDP,RTP,RTCP, HTTPS)
3. #internet_layer : 수신 측까지 데이터를 전달하기 위해 사용된다,
4. #network_access_layer : 네트워크에 직접 연결된 기기 간 전송을 할 수 있도록 한다.(이더넷, PPP,Tocken ring)



#### 면접 질문을 가지고 TCP/IP 이해하기
Q. www.google.com(:80) 치면 일하는 일은?
위와 같이 입력하면 80포트로 어떤 HTTP 요청 메세지를 보내는 것이고 해당 요청을 인터넷을 통해 구글 서버로 전달하기 위해 #패킷 을 만든다.  패킷에는 각 계층에 필요한 정보들이 담겨야한다. 


TCP 패킷의 해더 : SP 와 DP  
IP의 해더 : SA , DA (목적지 주소는 오직 도메인으로만 알고 있다, 하지만 DNS 프로토콜을 통해 알 수 있다.)


TCP/IP 의 흐름(DNS )
브라우저는 도메인에게 domain에 대한 ip주소를 요청 -> OS에서 DNS 서버로 요청을 보내고

Domain 프로토콜을 통해 ip 주소를 받아왔다 -> 마지막으로 ethernet 프로토콜에 대한 해더를 만들어야한다. #맥주소 (게이트 웨이)
#ARP_프로토콜 ip 주소를 MAC 주소로 바꾸어주는 주소해석 프로토콜 





* TCP 는 연결지향형 프로토콜 

## 나만의 언어로 정리


### 출처(참고문헌)

### 연결문서
- [[internet]]