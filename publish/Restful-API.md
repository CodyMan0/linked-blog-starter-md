

# REST-API

-> API에서 전송하는 자원(resource)은 URI로 해당 리소스에 행하고자 하는 의도를 HTTP 메소드 (get, post, put, delete)로 정의하는 방식입니다.


REST는 Representational State Transfer의 줄임말입니다. REST는 클라이언트가 서버 데이터에 액세스(남의 컴퓨터의 기능을 실행시키는 것) 하는 데 사용할 수 있는 **GET, PUT, DELETE 등의 함수 집합을 정의**합니다. 클라이언트와 서버는 HTTP를 사용하여 데이터를 교환합니다.

REST API는 위에서 설명한 **표준 아키텍처 스타일**을 사용하는 특수한 유형의 웹 API입니다.

[REST API](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest?pg=wianapi&cta=restapi)의 주된 특징은 무상태입니다. **무상태는 서버가 요청 간에 클라이언트 데이터를 저장하지 않음**을 의미합니다. 서버에 대한 클라이언트 요청은 웹 사이트를 방문하기 위해 브라우저에 입력하는 URL과 유사합니다. 서버의 응답은 웹 페이지의 일반적인 그래픽 렌더링이 없는 일반 데이터입니다.

최선 웹 API는 REST API 이며 용어는 서로 바꿔 사용할 수 있다. 


## REST API를 사용하면 어떤 이점이 있나요?


### 1. 통합 

API는 새로운 애플리케이션을 기존 소프트웨어 시스템과 통합하는 데 사용됩니다. 그러면 각 기능을 처음부터 작성할 필요가 없기 때문에 개발 속도가 빨라집니다. API를 사용하여 기존 코드를 활용할 수 있습니다.  

### 2. 혁신 

새로운 앱의 등장으로 전체 산업이 바뀔 수 있습니다. 기업은 신속하게 대응하고 혁신적인 서비스의 신속한 배포를 지원해야 합니다. 전체 코드를 다시 작성할 필요 없이 API 수준에서 변경하여 이를 수행할 수 있습니다.  

### 3. 확장

API는 기업이 다양한 플랫폼에서 고객의 요구 사항을 충족할 수 있는 고유한 기회를 제공합니다. 예를 들어 지도 API를 사용하면 웹 사이트, Android, iOS 등을 통해 지도 정보를 통합할 수 있습니다. 어느 기업이나 무료 또는 유료 API를 사용하여 내부 데이터베이스에 유사한 액세스 권한을 부여할 수 있습니다.  

### 4. 유지 관리의 용이성

API는 두 시스템 간의 게이트웨이 역할을 합니다. API가 영향을 받지 않도록 각 시스템은 **내부적으로 변경**해야 합니다. 이렇게 하면 한 시스템의 향후 코드 변경이 다른 시스템에 영향을 미치지 않습니다.

# Restful-API 세션 

## restful - api 란 (what)
- API 시스템을 구현하기 위한 아키텍처 중에 가장 널리 사용되는 형식 

### 특징 
1. 별도의 Tool이 필요하지 않다. 
2. Respresentatinal State Transfer(REST)
	-> 웹상에서 사용되는 여러 리소스를 ==HTTP URI 로 표현==하고 그 ==리소스에 대한 행위를 HTTP Method로 정의 하는 방식 즉 리소스(HTTP URI)를 어떻게 한다==(HTTP method + Payload)를 구조적으로 깔끌하게 표현 
- ==장점== : self -descriptiveness, restful api는 그 자체만으로도 api 의 목적이 쉽게 이해된다.
- 단점: 표준 규약이 없어서 **안티패턴**`(실제 많이 사용되는 패턴이지만 비효율적이거나 비생산적인 패턴)`으로 작성되는 경우가 흔하다. 
	
- Payload : HTTP request에서 server 로 보내는 데이터 ( body) 

- 큰 흐름 : get / https:// 10.58.4.1./ products
		**method , protocol,Host , Resource**

method는 동사의 역할 그리고 보안에 입각한 https 기능을 넣어서 다음 ip 호스트가 주어지고 거기에 연결된 서버단에 target resouce(목적어)를 넣어주므로써 요청을 한다. restful API 는 xml , json () 모든 형태로 전환가능 



### 다른 아키텍처 예시
#### SOAP 의 endPoint 설계 방법
xml 데이터 형태로만  데이터를 주고 받게 됨. (꺾새로 작성되어야함)
envelop의 형태에서 json 형태로 넘어가면 눈이 편해짐

####  rest api 장점 
주고받고자 하는 데이터를 직관적으로 알 수 있다. (비전공자 개발자가 봐도 알 수 있다. )
ㅇ적은 공수가 든다. 

####  GraphQL 장점 
엔트포인트를 적기만해도 그래프 큐엘에 받는 내용을 내부 자체적으로 프론트가 원하는 내용만 추출해서 줄 수 있게 된다.) 

####  GraphQL 단점
유알엘에서 분기가 미리 이뤄지지 않고 내 코드 안에서 이루어지고 백으로 전달되서 내부적으로 불필요하게 다량의 코드를 훑어야하는 단점이 있을 수 있다. 

-> 첫 endpoint 설계하는 사람에게는 진입 장벽이 있을수 있다. 



## restful api 설계 규칙 (how)

#### 1. URI 정보를 명확하게 표현해야 한다. 
resource는 명사를 사용한다. (복수형)
#### 2. resource에 대한 행위를 http method로 표현한다.
1. URI 에 http method가 포함되서는 안된다.
`GET/delete/user/1`
2. URI에 동사가 포함되서는 안된다.
`GET/user/show/1`  
3. resource 사이에 연관 관계가 있는 경우
`리소스/ 고유ID / 관계 있는 리소스`
4. 파일 확장자를 URI에 포함시키면 안된다.
`GET/user/1/profile-photo.jpg (x)`
5. URI 는 / 구분자를 사용하여 자원의 계층 관계를 나타내는데 사용한다. 
6. URI 마지막 문자로 /를 포함하지 않는다.
- 마지막에 /를 쓰면 뒤에 넣을 수많은 내용을 막아버린다.
7. URI 길어지면 -을 사용!! _은 사용하면 X
8. URI 경로는 대문자 사용X


## Path paramether, query parameter (useparams? query)
#### path parameter
경로를 변수로 사용하는 방식
GET htttp:// 10.58.4.1:8000/products==/1==
![[스크린샷 2022-08-11 오전 11.37.20.png]]

#### Query parameter - Filtering
`Query Parameter` 은 경로 뒤에 입력 데이터를 함께 제공하는 식으로 사용하는 방식
필요한 기능
- pagination 
- search

어떤 resource를 단순히 식별하고 싶으면 ==Path Parameter==를 사용하고,
정렬이나 필터링을 한다면 ==Query Parameter==를 사용합니다!




### 연결문서
- [[Web API]]
- [[HTTP]]
