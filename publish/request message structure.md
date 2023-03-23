

1.  Start Line("제목"): 요청의 첫번째 줄에 해당합니다. 이 시작 줄도 세 부분으로 구성되어있습니다.
    
    -   **HTTP Method:** 해당 요청이 의도한 액션을 정의하는 부분. 주로 **GET**, **POST**, **DELETE**가 많이 쓰임
    -   **Request target:** 해당 request가 전송되는 목표 #url
    -   **HTTP Version:** 말 그대로 사용되는 HTTP 버전을 뜻한다. 주로 1.1 버전이 널리 쓰임
    
    GET /login HTTP/1.1 
    - 해석: GET 메소드로 login 이라는 요청 타겟에 HTTP 1.1 버전으로 요청을 보내겠다!
    
2.  #Headers: 해당 요청에 대한 추가 정보(메타 데이터)를 담고있는 부분입니다. ( html의 head에 있는 부분이 담기는 것이 아님!! )
    
    -   **Key: Value** 값으로 되어있다 (JavaScript의 객체, Python의 딕셔너리 형태라고 보면 된다)
    -   **Host:** 요청을 보내는 목표(타겟)의 주소. 즉, 요청을 보내는 웹사이트의 기본 주소가 된다. (ex. www.apple.co.kr)
    -   #User-Agent:요청을 보내는 클라이언트의 대한 정보 (ex. chrome, firefox, safari, ~~explorer~~)
    -   **Content-Type:** 해당 요청이 보내는 메세지 body의 타입 (ex. application/json)
    -   **Content-Length:** body 내용의 길이
    -   **Authorization:** 회원의 인증/인가를 처리하기 위해 로그인 토큰을 Authroization 에 담는다
    
    Headers: {     Host:   
					     User-Agent:    
					     Content-Type:   
					     Content-Length:
					     Authorization:  }


    
3.  Body: 해당 요청의 실제 내용입니다. 주로 Body를 사용하는 메소드는 **POST** 입니다.
    
    ex) 로그인 시에 서버에 보낼 요청의 내용 
    
    Body: { 
    "user_email":"wecode@gmail.com" "user_password": "wecode" 
    }`
    

