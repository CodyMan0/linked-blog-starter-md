# API란 무엇인가요?
1. API는 정의 및 프로토콜 집합을 사용하여 **두 소프트웨어 구성 요소**가 서로 통신할 수 있게 하는 메커니즘(매개체 or 중간다리or 콘센트or 소통 창구 )입니다. 예를 들어, 기상청의 소프트웨어 시스템에는 일일 기상 데이터가 들어 있습니다. 휴대폰의 날씨 앱은 API를 통해 이 시스템과 "대화"하고 휴대폰에 매일 최신 날씨 정보를 표시합니다.

2. 컴퓨터의 기능을 실행시키는 방법.

## API는 무엇을 의미하나요?

API는 Application Programming Interface(애플리케이션 프로그램 인터페이스)의 줄임말입니다. **API의 맥락에서 애플리케이션이라는 단어는 고유한 기능을 가진 모든 소프트웨어를 나타냅니다.** 인터페이스는 두 애플리케이션 간의 서비스 계약이라고 할 수 있습니다. 이 계약은 요청과 응답을 사용하여 두 애플리케이션이 서로 통신하는 방법을 정의합니다. **API 문서에는 개발자가 이러한 요청과 응답을 구성하는 방법**에 대한 정보가 들어 있습니다.

## 생성된 시기와 이유에 따라 API는 네 가지 방식 분류
### SOAP API (과거의 복잡한 API)

이 API는 단순 객체 접근 프로토콜을 사용합니다. 클라이언트와 서버는 XML을 사용하여 메시지를 교환합니다. 과거에 더 많이 사용되었으며 유연성이 떨어지는 API입니다.  

### RPC_API

이 API를 원격 프로시저 호출이라고 합니다. 클라이언트가 서버에서 함수나 프로시저를 완료하면 서버가 출력을 클라이언트로 다시 전송합니다.  

### Websocket_API [[Web Soket Protocol]]

[Websocket API](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-overview?pg=wianapi&cta=websocketapi)는 JSON 객체를 사용하여 데이터를 전달하는 또 다른 최신 웹 API 개발입니다. WebSocket API는 클라이언트 앱과 서버 간의 **양방향** 통신을 지원합니다. **서버가 연결된 클라이언트에 콜백 메시지를 전송할 수 있어 REST API보다 효율적입니다.**  

### REST_API   [[Restful-API]]

오늘날 웹에서 볼 수 있는 가장 많이 사용되고 **유연한 API**입니다. 클라이언트가 서버에 요청을 데이터로 전송합니다. 서버가 이 클라이언트 입력을 사용하여 내부 함수를 시작하고 출력 데이터를 다시 클라이언트에 반환합니다. 아래에서 REST API에 대해 더 자세히 살펴보겠습니다.



#endpoint : 엔드 포인트를 쉽게 이해하려면 택배를 보낼 때를 생각하면 도움이 됩니다.
 실제 물건(요청)이 도착하는 지점을 엔드포인트라고 한다. 엔드포인트(End-point)란 API에서 서버 자원(resource)에 접근할 수 있도록 하는 URI





## 나만의 언어로 정리
>


### 출처(참고문헌)
1. https://aws.amazon.com/ko/what-is/api/
2. https://www.youtube.com/watch?v=PmY3dWcCxXI&t=497s [생활 코딩]


### 연결문서
-  [[Web API]]
- [[interface]]
- [[API documentation]]
- [[deployment]]
- [[SDK]]
