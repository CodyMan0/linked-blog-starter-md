# 공식 문서를 통한 지식 정리 
HTML과 같은 하이퍼미디어 문서를 전송하기 위한 [[application layer]] 프로토콜.

정리 : 인터넷 상에서 클라이언트와 서버가 자원을 주고 받을때 쓰는 통신 규약 . HTTP는 텍스트 교환이므로 보안에 취약하다. 이 보안 문제를 해결해주는게 [[HTTPS]]

특징
1. application layer의 최상위에 있다. 
2. [[proxy]]란 application layer에서 동작하는 것들을 말한다. 
3. 클라이언트와 서버가 http의 요청과 응답으로 교환하기 전에 신뢰할만한 인터넷 전송 프로토콜인 [[TCP]]에 연결을 설정해야한다. 
	여기서 http/1.0 그리고 http/2.0 그리고 http/3.0에 차이가 있는거구나? 
	http/1.0 : 각 요청/응답에 별도의 TCP 연결
	http./1.1은 파이프라이닝 개념괴 지속적인 연결의 개념 도입 
	http/2.0은 연결이 지속적이고 효율적으로 유지되는데 도움이 되도록 메시지를 다중 전송하는 특징

흐름 
1. TCP 연결을 엽니다. TCP 연결은 요청을 보내거나 응답을 받는데 사용됩니다.
2. HTTP 메세지를 전송합니다.  (HTTP/1은 text 그대로 오지만 HTTP/2는 캡슐화되어있다. 그러면 HTTP/2는 https인가?)
```html
GET / HTTP/1.1
Host: developer.mozilla.org
Accept-Language: fr
```
3. 서버에 의해 전송된 응답을 읽어들입니다
```
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2010 14:28:02 GMT
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: "51142bc1-7449-479b075b2891b"
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html

<!DOCTYPE html... (here comes the 29769 bytes of the requested web page)
```


HTTP는 hyperText Transfer Protocol의 
- hyperText -> html과 동일 (문서와 문서가 링크 로 연결되도록 하는 태그로 구성된 언어)
- Transfer -> 우리는 우리가 만든 웹사이트를 널리 알리고 다른 사람들과 공유하기 위해서 다른 컴퓨터에게 **전송**해야 합니다. 그리고 전송은 **보내는 주체**와 **받는 주체**가 있다는 것이 큰 특징입니다.
- Protocol -> 물리적으로 떨어진 컴퓨터 끼리 어떻게 HTML파일(HyperText)을 주고 받을지에 대한 **약속**입니다. 인터넷 상에서 일어나는 소통은 **대부분 HTTP 규약**을 따릅니다.

#한마디정리 그런데 그 약속에 핵심은 요청과 응답이다 요청의 특징 3가지가 있다
## Request and Response
**소통의 핵심은 요청과 응답**
- 가는말이 고와야 오는말이 곱다!!! x100

#### [[request message structure]]
#### [[respone message structure]]


## http method
[[http method]]


## Stateless #stateless
독립적인 HTTP 그래서 이전 정보를 알지 못하고 매 통신마다 필요한 정보를 보내야한다. 
state(기억력)
자기소개 #비유 가 너무 와닿는다. 
> 8명의 셀원들이 있는 셀모임이 있는데  시작하는 주 한명의 셀원이 왔다. 리더와 셀원 한명이 자기소개를 했는데 다음주에는 새로운 셀원이 오게 되었으니 또 자기소개를 해야하고 매 셀원이 새로 올때마다 자기소개는 계속 이루어진다. 

따라서, **기술의 탄생 배경** => 

만일 여러번의 통신(요청/응답)의 진행과정에서 연속된 데이터 처리가 필요한 경우(ex. 온라인 쇼핑몰에서 로그인 후 장바구니 기능)를 위해 로그인_토큰 또는 브라우저의 쿠키 , 세션_스토리지, 로컬_스토리지 같은 기술이 필요에 의해 만들어졌습니다.

stateful : stateless의 반대 개념 ! 요청이 저장되는 것을 말한다. 

stateful / stateless 차이 및 사용 정리

## 나만의 언어로 정리
HTTP 는 컴퓨터들끼리의 약속이다. HTTP 소통의 핵심은 요청과 응답이다. HTTP 통신은 독립적이다. 그래서 이전의 상태를 전혀 알지 못한다. 그렇기 때문에 매 통신마다 필요한 모든 정보를 담아서 요청을 보내야한다. 



## HTTP 기반 API
1. [[XMLHttpRequest]]
2. [[Fetch API]]

### 출처(참고문헌)

### 연결문서
- [[HTTPS]] 
