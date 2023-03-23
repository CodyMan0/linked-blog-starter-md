# 인증 과정 중 2가지 sesion과 token Based Authentication


# 1. Introduction

---

웹 환경에서 사용자와 시스템 간에 데이터를 교환하기 위해 HTTP 방식을 사용합니다. HTTP 통신은 요청과 응답에 의해 동작하며, HTTP의 특징 중 가장 중요한 특징은 바로 ==Stateless== 입니다. 문자 그대로 번역하면 State(상태) + less(없음) 을 의미합니다 -> ==(상태를 기억하지 않음)==
  

각각의 HTTP 통신(요청/응답)은 독립적 이기 때문에 과거의 통신(요청/응답)에 대한 내용을 전혀 알지 못 합니다. 이전의 상태를 전혀 알지 못 한다는 것은 무엇을 의미할까요?  
  

**매 통신마다 필요한 모든 정보를 담아서 요청을 보내야 합니다.** 비유를 하자면, 마치 이미 자기소개를 한 사람에게 계속해서 똑같은 내용으로 자기소개를 해야하는 것과 같습니다.  
  

따라서, 만약 로그인 후 상품 구매나 개인정보 수정 같이 여러번의 통신(요청/응답)의 진행 과정에서 연속된 데이터 처리가 필요한 경우에 Stateless의 특징에 따라 매번 로그인을 위한 인증정보를 같이 보내주어야 합니다.  
  

==위와 같은 불편함을 없애고자 일부 정보에 대해서 Stateful 상태를 유지할 필요가 있습니다. 이를 위해서 Session과 Cookie 또는 Token 같은 기술을 사용할 수 있습니다.==

# 2. Session based ****Authentication****

---

## 2-1. Session and Cookie

Session과 Cookie를 이용한 Authentication에 대해 알아보기 전에 Session과 Cookie의 차이에 대해 명확이 알아야 합니다.  
  

### 2-1-1. Session

동일한 클라이언트(사용자)가 브라우저를 통해 웹 서버에 접속한 시점으로부터 브라우저를 종료하여 연결을 끝내는 시점 동안에 들어오는 일련의 Request를 하나의 상태로 보고, 그 상태를 일정하게 유지하여 클라이언트와 웹 서버가 논리적으로 연결된 상태를 뜻합니다.  
  

서버는 Session에 대한 정보를 저장하고 클라이언트에게는 Sesssion을 구분할 수 있는 ID를 부여하는데 이것을 Session ID라고 합니다.  
  

클라이언트 Request를 보낼 때 해당 Session ID를 함께 보냄으로써, 클라이언트의 상태를 확인 할 수 있습니다.  

멘토 : 사용자가 로그인을 하고 끝내는 시점까지를 세션이라고 한다.  

### 2-1-2. Cookie

==Cookie는 클라이언트의 컴퓨터에 저장되는 데이터 파일==입니다. ==Cookie에는 **이름, 값, 만료 날짜/시간(저장기간), 경로 정보** 등으로 구성이 되어있습니다==. ==Cookie는 하나의 도메인 당 20개를 가질 수 있으며, 1개 당 4Kbyte를 넘길 수 없다는 특징==을 가지고 있습니다.  
  

서버에서는 HTTP Response Header에 **Set-Cookie** 속성을 이용하여 클라이언트에 Cookie를 제공하여 저장하게 하고, 클라언트는 HTTP Request에 저장된 Cookie를 함께 전달하여 이전의 통신에서 사용된 정보들을 파악할 수 있습니다.  
  
예를 들어 장바구니 기능 같은 경우 과거에는 로그인을 해야지만 사용할 수 있는데, 최근에는 Cookie를 이용하여 로그인을 하지 않은 상태로 장바구니에 상품을 담을 수 있게 되었습니다.  
  
또한 Cookie를 통해 사용자별로 다른 정보를 표시하는 것이 가능하고, 사용자의 행동과 패턴을 분석할 수 있기 때문에 최근들어 더욱 중요한 개념이 되었습니다.

cookies : 세션 id 저장, 비회원 같은 기능, 오늘 하루 보지 않는다 기능 
위의 행동을 쿠키에 담아서 서비스를 운영하는 서버에게 행동 분석이 가능하도록 한다.


## 2-2. Session과 Cookie를 이용한 인증 Flow

![session img](https://api-media-storage.s3.amazonaws.com/session-media/5bd5a25ea7924deda3d4be0c0f74b045?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MM4MRKFJBN%2F20220808%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220808T005545Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEKH%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaDmFwLW5vcnRoZWFzdC0yIkcwRQIgTn1utfmmWpR5S9TIOYuKqIWQ6GJBfWZscmYYHKL4zq0CIQCJ%2Fdf1jMGSuK5oV4YO7BmaonAb%2F8oh8HjuTt8eOjf5Uir0Agj6%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAQaDDE3OTAyMjQ1MTQ4MSIMrwaPHq2gtSEBMXfFKsgCdceOeUeEWldScySt6TvQURC7bXqs28pnSa7XFW3shlqAZrbJ0RRzTLOCvcdTSQrWib4M%2FWY3GaEKJLLLABO2xUWlqyKLw7xB2IBQOCJytKVw7sZv15lqXkzCn6sQpQ%2FAIs2ZxnHf4wxmWcIUnCvEgkM1d%2BHjMPImwX0LaE976sxOJRuHuwKDkJLYaKiS2yRjQlSy5NHjn53y247FhteUbDMBQwW2rdwEmauvqZoSE%2F4qTgUaRB%2BMA5q2N4aiXpm4%2B9Owh1x536JSpU9pyLNzSifIKgR5G7Q%2B9wW4tTfIi%2FVw0v9bJqAWRIRZ6O5mpvwdVZvRCem2C5HcKQe%2B1b98y3HomnqXKc1htifVPV2DRH8bIxdEc17WQoIxsYVwkMtcx%2FGWK9ktzOivco%2FmydhLFyshO5MvLyWil%2BgqN%2BArIrtTMTx9zlz%2B6DCOucGXBjqeAc3tKB8JXg25w1BbOx5sPz5tugvXFcKsBsUWXKHWg3wxFL%2Bejso8G6MsqxQJX%2FqqcemL3Syi%2BG74wxmMz0lGECLx9S8kwk6vk1bKfDH37WO%2Bxjsfbvvjk7sFaLuIIgEtFC7ZVZMdeRXAmTbhq7acn7QCFXM4Q3gYbnpbgwSv5RjKoIoIxKU5cL%2Fi%2B3YGSd5Ns8Tmoq1vy90WGHqdXxPL&X-Amz-Signature=e3428af9f57eb114c456231d8e41c47703e3c13a03401c5b8c8f90ebb7f632c8)

[그림 2-1] Session based Authentication flow  
  

-   사용자가 로그인을 하기 위해 인증 정보를 가지고 인증 과정을 요청 합니다.
-   인증이 완료 되면 사용자의 Session 정보를 서버의 메모리에 저장 후 해당 Session을 식별할 수 있는 Session ID 발급 합니다.
-   발급한 Session ID가 Cookie에 저장 될 수 있도록 HTTP Response Header의 Set-Cookie 속성을 이용하여 사용자에게 전달 합니다.
-   전달받은 Session ID는 브라우저의 Cookie에 저장 되고, Request를 서버에 보낼 때 함께 전달 됩니다.
-   서버는 사용자가 보낸 Session ID 와 서버 메모리에서 관리하고 있는 Session ID를 비교하여 Verification을 수행 후 권한을 인가 합니다.

## 2-3. Session 기반 인증의 특징

### 2-3-1. 장점

-   Session ID 자체에는 유의미한 개인정보를 담고 있지 않습니다. ==(배열과 객체와 같음)==
-   서버에서 정보를 관리하기 때문에 데이터의 손상 우려에 대해 상대적으로 안전 합니다.
-   서버에서 상태를 유지하고 있으므로, 사용자의 로그인 여부 확인이 쉽고, 경우에 따라서 강제 로그아웃 등의 제재를 가할 수 있습니다.  
      
    

### 2-3-2. 단점

-   서버에서 모든 사용자의 상태를 관리해야 되므로 사용자의 수가 증가 할 수록 서버에 가해지는 부하가 증가합니다.
    
-   ==사용자가 증가하여 서버의 Scale Out을 해야 할 때 Session의 관리==가 어려워 집니다.
    
-   ==모바일 기기와 브라우저에서 공동 사용 할 때 중복 로그인 처리가 되지 않는 문제 등 신경 써줘야 할 부분 들이 증가합니다.==

-> scale out : 서버의 수를 늘리는 것. 인증만 관리하는 서버를 두고 다른 서버로 가게 하는 설정이 필요. 회원가입을 session 기반으로 설정할떄 위의 어려움이 있을 수 있다. 

-> end point는 URL



# 3. Token based ****Authentication****

---

## 3-1. Token

일반적으로 사용되는 Token의 사전적 의미를 찾아보면 버스 요금이나 자동판매기 등에 사용하기 위하여 상인, 회사 등에서 발행한 동전 모양의 주조물 이라고 나와있습니다. 웹에서의 토큰도 이와 비슷한 의미를 가지고 있습니다. 일상에서는 Token을 가지고 있으면 버스를 탈 권리, 도는 자동판매기에서 상품을 구매할 권리를 가지고 있다면, 웹에서는 Token을 가지고 있으면 해당 서비스를 이용할 수 있는 권리가 있다고 생각 할 수 있습니다.  
  

조금 더 자세히 이야기해 보면 ==Token은 제한된 리소스에 대해 일정 기간 동안 접급 할 수 있는 권한을 캡슐화== 한 것입니다. Token은 일반적으로 의미를 알 수 없는 임의의 문자열 형태로 사용자에게 발급 합니다. 또한, ==제한된 리소스에 대한 접근 권한을 캡슐화 할 뿐만 아니라 접근 할 수 있는 리소스의 범위와 접근 가능한 기간을 통제== 할 수 있습니다.

맨토 : 로그인 인증이 완료되면 session id를 주는 것이 아니라 토큰을 부여한다. 토큰 안에는 권한이 내장 

## 3-2. Token을 이용한 인증 Flow


[그림 3-1] Token based Authentication flow  
  

-   사용자가 로그인을 하기 위해 인증 정보를 가지고 인증 과정을 요청 합니다.
-   인증이 완료 되면 ==서버의 메모리에 Session을 저장하는 대신에 사용자의 식별 정보를 가지고 있는 Token을 발급==합니다.
-   ==발급한 Token은 Response의 Body==에 담아 사용자에게 전달합니다.
-   ==사용자는 발급된 Token을 local storage에 저장== 합니다.
-   사용자는 Request를 할 때마다 저장된 Token을 ==Header 에 포함시켜 서버로 보냅==니다.
-   서버는 사용자로부터 전달받은 ==Header의 Token 정보를 Verification 한 뒤, 해당 유저에 권한을 인가== 합니다.

## 3-3. Token 기반 인증의 특징

### 3-3-1. 장점

-   Token을 사용자 측에서 저장하므로 서버의 메모리나 DB 등의 부담이 없습니다.
-   ==사용자의 상태 정보를 서버에서 관리하지 않기 때문에 서버의 Scale Out에 용이== 합니다.
-   ==모바일과 브라우저의 멀티 환경에서 사용이 용이== 합니다. **(session과 반대)**
-   Token의 만료 시간을 짧게 설정하여 ==안정성==을 높일 수 있습니다.
-   ==CORS== 방식을 사용하기 용이 합니다.  
      -> 왜지?ㄷ
    


### 3-3-2. 단점

-   서버에서 사용자의 상태를 저장하고 있지 않기 때문에 사용자의 로그인 여부 확인, 경우에 따른 강제 로그웃 등의 ==제재를 가하기 어렵==습니다.
-   ==사용자가 임의로 토큰을 수정==하거나 구조가 변경되게 되면 서버에서 확인할 수가 없습니다.
-   Payload 부분(유저가 누구인지)에 사용자 식별을 위한 여러 정보들이 포함 되어 있어 Session Id의 길이보다 길어져 ==HTTP request 전송 데이터의 크기가 증가== 합니다.
-   ==XSS 공격==에 취약하여 Payload에 민감한 정보를 포함하는 경우 위험할 수 있습니다.
	-> 브라우저의 저장된 정보를 탈취할 수 있게하는 것 XSS 공격

멘토 : payload 부분에는 민간한 정보를 담으면 안된다. 

# 4. Token based Authentication의 이점

---

## 4-1. Stateless

Session 방식처럼 상태 정보를 서버측에서 관리 하지 않고, 사용자 측에서 관리하기 때문에 서버의 상태를 Stateless하게 유지하게 됩니다. ==따라서 서버측에서는 사용자로부터 받은 Request만을 가지고 작업을 수행== 할 수 있습니다.

## 4-2. Scalability

서버의 상태를 Stateless 하게 유지 한다는 것은 사용자와 서버 사이에 관계가 없다는 의미도 됩니다. 일반적으로 Session 기반 인증에서는 로근인 상태를 유지하기 위해서는 최초 로그인 시에 Request 한 서버로 계속 Session ID를 보내주어야 합니다. 하지만 Token 기반의 인증 방식은 이러한 관계가 존재하지 않기 때문에 서비스를 운영 중인 어떤 서버로든지 Request를 보낼 수 있습니다. 이런 덕분에 Token 기반의 인증 방식을 사용하면 서버의 확장에 유리 합니다.

## 4-3. Security

클라이언트가 서버로 요청을 보낼 때 더 이상 Cookie를 전달하지 않으므로, CSRF 공격을 방지하는 데 도움이 됩니다. 하지만 토큰 환경의 취약점이 존재할 수 있으므로 이에 대비해야 한다.

## 4-4. Extensibility

Token 기반의 인증 시스템에서는 토큰을 통해 권한의 범위를 지정 할 수 있습니다. 이를 이용하여 KaKao, Facebook, Google 등과 같은 소셜 계정을 이용하여 다른 웹서비스에서도 로그인을 할 수 있습니다.

## 4-5. Multiple Devices and Domains

서버 기반 인증 시스템의 문제점 중 하나인 ==CORS를 해결==할 수 있습니다. 애플리케이션과 서비스의 규모가 커지면 여러 기기들을 호환시키고 더 많은 종류의 서비스를 제공하게 됩니다. 토큰을 사용한다면 어떤 기기, 어떤 도메인에서도 토큰의 유효성 검사를 진행한 후에 요청을 처리할 수 있습니다.


멘토: 백앤드와 연관 -> 백앤드에서 cors를 설정한다?[[cors]] 와 멀티 디바이스 연관. 


# 5. Summary

---

-   HTTP를 이용한 통신에서 로그인 상태 같은 Stateful 상태를 유지하기 위해서 Session과 Cookie 또는 Token을 이용한 방법을 사용 합니다.
-   Session을 이용할 경우, 인증이 완료 되면 사용자의 Session 정보를 서버에 저장하고 해당 Session 정보를 식별할 수 있는 session_id를 클라이언트에게 전달합니다. 이 때, 클라이언트와 서버는 cookie를 이용하여 session_id를 주고받습니다.
-   Token은 제한된 리소스에 대해 일정 기간 동안 접급 할 수 있는 권한을 가지고 있는, 일종의 **통행권** 입니다.
-   Token은 Session과 달리 **서버에 token 정보를 저장하지 않습니다.**
-   **Token을 이용하면 서버의 상태를 Stateless 하게 유지 할 수 있어 서버 확장에 유리합니다.**
-   Token을 이용하여 **다양한 기기에서 서비스가 호환 되도록 운영**할 수 있습니다.

### 연결문서
- [[HTTP]]
