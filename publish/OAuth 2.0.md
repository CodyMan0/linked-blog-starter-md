# OAuth 2.0

user요청에 의해서 그들의 Service 가 accessToken을 부여해준다. aT을 이용해서 그들의 서비스에 접근해서 CRUD를 할 수 있다.

OAuth를 통해서 accessToken을 얻을 수 있다는게 핵심

## 역할
1. Resource Owner  
2. Client
3. Resource Server(data) & Authorization Server(인증)

## 등록
Client ID 아이디
Client Secret 비밀번호

Authorized redirect Urls https://client/callback 

## 인증 
UI에 보여질 로그인 버튼은 별거 아니다 
```js
https://resource.server/?client_id=1&scope=B,c%redirect_url=https://client/callback
```
![[스크린샷 2022-12-19 오후 7.14.19.png]]

로그인을 하게 되면 같은 Client_id를 찾는다. 그리고 redirect url과 비교! 해서 맞으면 resource Owner에게 동의를 구한다. 허용을 하면 resource server에 동의 정보를 받고 


## resource server의 승인
access-token을 발급하기 전에 한단계가 있다. Authorization code를 resource server에서 resource owner로 전송한다. 
![[스크린샷 2022-12-19 오후 7.18.44.png]] 
header에 껴서 간다.  code=3이 authorization이었다. Resource Owner가 인식하지 못하게 Client로 이동하게 시킨다. code=3으로 인해 Client도 authorization code = 3을 알게 된다. 
![[스크린샷 2022-12-19 오후 7.20.46.png]]

Authorization code와 Client_secret 두개의 비밀번호를 resource server에 전달

Resource 서버가 받은 정보와 가지고 있는 정보가 동일하다면 이제 access-token을 제공하게 된다. 


## access Token 발급
Oauth2의 목적은 accessToken을 발급하는 것. 
다 확인하면 RS는 accessToken을 생성하고 Client에 응답값으로 준다. 
Client은 파일에 accessToken을 저장한다. 


## API 발급
accessToken을 가지고 API를 사용하기 위해서는 메뉴얼대로 해야한다. 



## refresh token 
액세스 토근을 발급받은 



### 연결문서
- [[Bearer Authentication]]
