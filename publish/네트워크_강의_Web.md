## DNS

인터넷을 이루고 있는 각종 서비스는 Application 계층에 존재하는 것. 이런 서비스 중 인프라에 해당하는 서비스는 [[DNS]]가 있다!

- 분산 구조형 데이터 베이스
	- DNS 네임서버의 분산 구성
	- 데이터의 영열별 구분 및 분산관리
	- 도메인의 네임서버 및 도메인 데이터는 해당 관리주체에 의해 독립적으로 관리됨. 
- 트리 구조의 도메인 네임 체계 
	- Domain : 영역, 영토를 의미
	- 도메인 네임의 자율적 생성
	- 생성된 도메인 네임은 언제나 유일하도록 네임 체계 구성

- 철수가 protocol://www.naver.com을 검색하면 
1. 컴퓨터의 (DNS 서버 주소)IP 설정을 기반으로 공유기에게 묻는다.
2. DNS 서버로 부터 IP주소와 캐싱에 사용되는 유효기간을 응답을 받는다. 
3. 받은 IP주소로 접근하면 naver에 접근 가능 

![[ISP.excalidraw.png]]

- URL 주소 = Host name과 Domain name으로 나눠져있다. 
![[도메인 이해하기.excalidraw.png]]


### 중요
1. [DNS Cache]DNS에 질의를 한 번이라도 하면PC 메모리에 질의한 URL의 IP를 가지고 있는다. (캐싱)
2. [보안] DNS가 거짓말을 하면? DNS에는 엄청나게 강력한 보안이 설정되어있다. 

###  더 알아야하는 것
1. DNS cache와 같은 역할을 할 수 있는 것이 공유기! DNS 주소와 공유기 주소와 같다는 것은 공유기가 DNS 서버에 포워딩이 돼, DNS 기능을 대신 해주는 것이라고 생각하면 된다. 
2. RootDNS는 전세계 13대 정도 있다. (iana.org) Root DNS는 DNS를 위한 DNS이다. 

Q. 도메인을 산다는 것은 어떤 의미는 ? 



## 웹 역사
HTML : hype-text-message-language (문서)
HTTP : HTML을 실어나르기 위한 프로토콜 (인프라 : TCP/IP) [[HTTP]]


인터넷 라우터를 구현은 전세계에서 우리가 두번째로 구현 1982년 
(서울대학교와 경북 구미에있는 전자 기술 연구소 )

전길남 선생님!

#암기 html은 문서다. 

## URL 과 URI 
관련 : [[WEB Moc]]
![[도메인 이해하기.excalidraw.png]]

URL : uniform resource locator (위치) : 파일이 있는 위치
URI : uniform resource identifier (식별자) :

- 개념 
URI > URL

```
Protocol://Address:PortNum/Path(or filename) ? parameter=value

http://www.test.co.kr/course.do?cmd-search&search_keywork=Test
```

htt://www.test.co.kr/ -> host 연결
course.do -> 경로 
?cmd-search
&search_keywork=Test


## HTTP 
L7 계층에 존재하는 응용 프로그램 계층 통신 프로토콜
L5 이상 이다라는 것은 소켓 통신을 하고 있는 것이고 그 말인 즉은 스트림 데이터를 가지고 통신한다는 것이다. 시작은 있지만 끝이 언제인지 해석을 해야한다. 해석하는 규정이 HTTP에 포함돼있다. 오호~ 

HTTP는 문자열로 돼있다. 그리고 stream 데이터이기에 프로토콜 해더를 통해서 끝을 규정해준다. 

### http header 잘 알아야할 것 같다.
- 해더
	- 일반
	- 요청
	- 응답
	- 엔티티

### status code 
[[statusCode]]

### method
[[http method]]
  


resource가 무엇인가? 파일(html,css,js,jpg 등등)들!
  

