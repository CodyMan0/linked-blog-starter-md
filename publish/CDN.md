---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 : 대규모 시스템 설계 기초 , 유튜브
저자 : 알렉스 쉬 지음

URL :
1. https://www.youtube.com/watch?v=YJGz7F9pLQE,
2. bytebytego : https://www.youtube.com/watch?v=RI9np1LWzqw
3. akamai 영상 : https://www.youtube.com/watch?v=9Sq9y4ljmPI


https://www.youtube.com/watch?v=RLJ6tPzXB5Q&t=301s
공부하기 
인용 : 

CDN은 정적 콘텐츠를 전송하는데 쓰인다. [[caching]]과 연관


그렇다면 동적 콘텐츠 캐싱은 무엇이지? 
-> request path , query string, cookie, request header 등의 정보에 기반하여 html 페이지를 캐싱하는 것을 말한다. (http 요청)

# 강의 (인터넷 전반에 대한 이해와 CDN의 개념


아카마이의 핵심 고민 
> 어떻게 하면 인터넷을 빠르고 안정적으로 사용할 수 있을까? 

## internet
![[스크린샷 2023-03-01 오후 3.16.45.png]]

점들이 의미하는 것은 [[ISP]]

- 네트워크 간에 연결 : kt와 skt 간 연결이 되는 것은 자원을 아끼기 위해 
- 단일한 윤영/ 통제 주최가 없다는 의미는 누구에게나 열려있다는 의미! 통제하려는 나라는 중국과 북한 정도. 즉 누구에게나 열려있지만 어느 누가 책임지지 않는다는 의미

### internet은 네트워크들의 집합
![[스크린샷 2023-03-01 오후 3.22.05.png]]


### 인터넷의 구조 
![[스크린샷 2023-03-01 오후 3.28.11.png]]

middle Mile : ISP간의 연결 (해저 테이블로 연결)
last Mile : user와 ISP와의 연결

인터넷 사용량의 변화(텍스트 -> 이미지,텍스트 -> 동영상)으로 인한 컨텐츠의 평균적인 크기가 증가하였습니다. 유튜브를 통해 검색량이 증가하면서 유튜브 서버(해외)까지 가는데 시간이 걸리는 문제가 발생되었다. 


### 인터넷 컨텐츠의 전달 과정 

찾아보기 


### 인터넷을 느리게 하는 것 
1. 물리적 거리 (가장 큰 이유)
2. 최단 경로로 가지 않는다. (자원 이슈 )


### 역사적 관점으로 본 해결책
#### 1.  캐싱 ( CDN 1.0) 텍스트 -> 이미지 
이미지가 텍스트 보다 용량이 크다 보니 이미지 콘텐츠가 느리게 업로드가 된다. 웹사이트에 들어갈때 이미지는 캐시 서버에서 주는 것. 캐시 서버는 어디에 놓을까? user와 연결된 [[ISP]]와 연결 되어있나? (찾아보기)

적용 분야 
- 이미지 플래쉬 캐싱
- 웹사이트 캐싱
- 멀티 미디어 스트리밍
- 대용량 파일

효과
- 사용자 속도 개선
- Origin 서버 (본 서버) 및 네트워크 부하 감소
- 대규모 동시접속시 사이트 다운 방지


#### 2. 가속 (CDN 2.0) 이미지 -> 동적 콘텐츠  2005  

로그인 이후 사용자에게 맞는 정보를 주어야하는 상황으로 바뀌었다. 그래서 CDN서버는 Origin 서버로 다시 가야하는 상황이 생김. 그래서 user와 Origin 서버간에 거리가 멀면 과거의 문제가 다시 발생하는 상황.


적용 분야 
- 웹 동적 컨텐츠 가속
- Socket 통신 가속
- VDI 가속
- VPN 가속
- 이메일
효과
- 해외 사용자 속도개선 (한국일 경우)


#### 3. 모바일 환경 최적화 (CDN 3.0) 이미지 -> 모바일 퍼스트 2015  
다른 디바이스 환경에 따라  CDN에서 해상도를 조절해주고 내려주는 기능 

적용 분야 
- 글로벌 웹사이트
- 모바일 사이트
- 모바일 앱
효과
- 웹사이트 성능 최적화 
- 모바일 환경에 성능 최적화 


# CDN
1998년에 등장 
1. 가장 기본적인 역할 
 ![[스크린샷 2023-03-01 오후 4.12.37.png]]
 유저로부터 가장 가까운 곳(ISP)에 CDN 서버를 캐시해놓아 문제를 해결
CDN 서비스를 제공하는 업체 : AWS cloudfront , CLOUDFLARE, Akamai, Azure CDN

 4개의 업체의 공통점 
 1. DNS

2. Anycast





# 웹 프론트엔드 최적화를 위한 성능개선 및 CDN 

## 이미지 최적화 
![[스크린샷 2023-03-01 오후 4.36.08.png]]
모든 경우의 이미지를 준비하려면 너무 복잡하다. 이런 문제를 해결 하기 위한 방법
1. 로직으로 해결하려면 복잡도나 확장성이 나빠진다. 클라우드 서비스로 해결 
2. HTTP 해더의 활용 
	1. cache-control: max-age=600 // 10분간은 브라우저에서 캐시하여 데이터를 가지고 있겠다.
	2. content-encoding: gzip // html,css,js를 내려줄때 gzip으로 압축해주겠다는 의미.
	3. content-length: 34735
	4. content-type:text/html
3. 캐싱
	1. 인터넷 캐싱 (프록시 서버 캐싱, CDN 캐싱)
	2. 브라우저 캐싱 
4. CDN
	1. 사용자의 주변 CDN 서버로 부터 정적 콘텐츠를 내려받아 빠르게 이용 가능하다
![[스크린샷 2023-03-01 오후 4.45.57.png]]
		-> 원본 서버 부하 분산 성능개선, 비용 개선의 효과 




# CDN 필요성
 결국 하나의 요청당 하나의 응답을 받게 되는데 서비스가 커지면 문제가 발생 

응답 속도의 

지역마다 둔 서버를 EDGE라고 부른다.

## DNS와 GSLB

**DNS** : domain name system 
**GSLB** : global server load balancing  -> 서버의 상태를 파악해서 적절한 서버로 연결해준다. 
DDos : 요청이 몰리면 CDN으로 연결해두렁ㅆ따면 그 지역 CDN만 공격 당하고 이후 같은 지역으 ㅣ요청은 다른 서버로 자동을 ㅗ요청하게 연결해줘서 장애대응에 장점


## 캐싱과 TTL 
데이터를 얼마나 오래 존재하도록 할지에 대한 용어 TTL로 서버에 캐싱할 데이터의 유효시간을 정하는 것은 react-query에서 캐시 타입을 정하고 시간이 지나면 새롭게 요청을 보내서 데이터를 가지고 오는 것과 같다. 
-> Edge computing 




### 생각의 연결고리
분야 :

키워드 : [[caching]]

관련있는 메모 :
[[edge]]