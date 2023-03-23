# 소개

이 글은 Oauth를 이용해서 access token을 획득한 후에 api에 접속하는 방법에 대해서 설명하고 있습니다.

## Bearer Authentication란?

API에 접속하기 위해서는 access token을 API 서버에 제출해서 인증을 해야 합니다. 이 때 사용하는 인증 방법이 Bearer Authentication 입니다. 이 방법은 OAuth를 위해서 고안된 방법이고, [RFC 6750](https://tools.ietf.org/html/rfc6750)에 표준명세서가 있습니다.

# 사용법

예를들어 api 서버가 server.example.com이고, 접근해야 하는 path가 resource이고, access token이 mF_9.B5f-4.1JqM라면 아래와 같이 헤더 값을 만들어서 전송하면 됩니다.

GET /resource HTTP/1.1 Host: server.example.com Authorization: Bearer mF_9.B5f-4.1JqM

# 예제

각 언어별 사용법은 아래와 같습니다.

## Web browser JavaScript

ajax를 위해서 도입된 fetch api를 이용한다면 아래와 같이 하면 됩니다.

```
// header 정보를 추가합니다. 
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer mF_9.B5f-4.1JqM");
fetch('https://server.example.com/resource',{
    "headers":myHeaders
}).then(function(res){
    // 서버의 응답이 json인 경우 아래의 코드를 통해서 js의 객체로 변환된 결과를 얻을 수 있습니다. 
    return res.json();
}).then(function(data){
    // json으로 변환된 결과를 출력합니다. 
    console.log(data);
});
```

## Node.js

Node.js에는 fetch api가 없습니다만, node-fetch를 통해서 fetch api와 동일한 코드로 서버에 접속할 수 있습니다.

[https://github.com/bitinn/node-fetch](https://github.com/bitinn/node-fetch)


1.  access token을 서버로 전송할 때는 반드시 ==https(TLS)==를 이용해야 합니다. 그렇지 않으면 일종의 비밀번호라고 할 수 있는 access token이 노출되게 됩니다. api에 접속해서 실제 서비스를 구동하기 전에 https를 살펴보세요.
2.  구글 같은 몇몇 서버스의 경우 api를 호출하기 전에 ==api를 활성화== 해야 합니다. api의 활성화가 필요한지 확인하는 것을 잊지 마세요.
3.  Bearer Authentication 외에 ==Form-Encoded Body Parameter== 방식과 ==URI Query Parameter== 방식이 있습니다. header(Authorization: Bearer )를 이용할 수 없는 경우에 form이나 url의 query string 방식을 활용하는 것인데, ==보안적인 이유로 권장되지 않습니다==. 또한 서비스들이 제공하지 않을 가능성이 높습니다. 가급적 지원된다해도 사용하지 마세요.

### 관련있는 메모 :
[[카카오톡 로그인 하는 기능 추가하는 과정]]

