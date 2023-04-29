# 요약
-  JWT(JSON Web Token)는 토큰 자체에 정보를 넣어서 주고 받을 수 있는 구조 입니다.
-   JWT는 크게 headers,payload,signature로 나눌 수 있고, 정보의 위변조 여부를 signature로 확인가능합니다.
-   ==access token을 만드는 방법중 하나가 JWT==입니다.
-   로그인에 성공하면 서버에서 인증된 유저라고 신분증처럼 JWT를 발급합니다.
-   HTTP 통신의 stateless특성 때문에 JWT를 받은 내역을 기억하고 있지 못해서 어딘가 저장해서 써야합니다.
-   클라이언트는 browser storage를 사용 할 수 있고, local,session,cookie등 목적에 따라 저장 가능합니다.
-   ==local storage 저장을 예로들면 localStorage.setItem(), storage에서 꺼내오려면 localStorage.getItem()으로 활용 가능==합니다.

# JWT


==JWT==(JSON Web Token)는 클라이언트(사용자)와 서버 간에 정보를 JSON 개체로 안전하게 전송하기 위한 개방형 표준(RFC 7519)입니다.



특징
1. ==SAML== (Security Assertion Markup Language Token) 보다 크기가 작아 더 컴팩트하게 사용할 수 있습니다.
2. ==JWT는 JSON 개체에 기본정보, 전달할 정보, 검증 정보==를 모두 담고 있습니다. 또한, JWT는 전자 서명이 되어있기 때문에 검증 과정을 거쳐 확인하고 신뢰할 수 있으며 Secret Key 또는 Public/Private Key Pair를 사용하여 서명할 수 있습니다.  

구성
JWT는 일반적으로 ==Base64로 인코딩된 데이터==와 ==전자 서명==으로 구성되어 있습니다. JWT 역시 데이터를 암호활 할 수 있지만, JWT가 전자서명이 되어 있다는 점이 중요 합니다. 전자 서명된 JWT의 목적은 데이터를 숨기는 것이 아니라 ==데이터의 신뢰성==을 보장하는 것입니다. 그렇기 때문에 서명된 JWT와 함께 HTTPS를 사용하는 것이 좋습니다  
  

JWT을 이용한 인증 과정은 ==사용자 측에 사용자의 정보를 관리하는 ****토큰 기반 인증 메커니즘입니다==. 따라서 서버에서 세션 정보를 저장하기 위해 세션 스토리지 또는 데이터베이스에 완전히 의존할 필요가 없습니다. 또한, 서버의 확장성과 멀티 기기 및 도메인에서 활용에서도 이점을 가지고 있습니다.



## 1-2. JWT 구조

JWT는 JSON Web Token의 약자로, access token을 만드는 방법 중 하나입니다. 


JWT는 토큰 자체에 정보를 담아서 주고받을 수 있는데, ==JWT==는 민감한 정보 교환을 위해 사용되기도 하고 현대 웹에서 가장 많이 쓰이는 예시는 ==인증&인가==를 위해서 사용합니다.



## 3. JWT 사용 방법

---

### 3-1. JWT 브라우저 storage 저장 방법

로그인 후 response의 body에 담긴 access token(JWT)을 브라우저의 저장소인 local storage, session storage, cookie에 저장할 수 있습니다.

-   local storage는 ==해당 도메인에 영구 저장==하고 싶을 때
-   session storage는 해당 도메인의 한 세션에만 저장하고 싶을 때. ==창을 닫으면 저장한 data==가 삭제됩니다.
-   cookie는 해당 ==도메인에 날짜를 설정하고 그때까지만 저장하고 싶을 때==

### access token
저장 위치 : 클라이언트 사이드의 메모리에 저장 (변수에 저장)

### refresh token
저장 위치 : 클라이언트 사이드의 httponly 설정이 되어있는 cookies에 저장