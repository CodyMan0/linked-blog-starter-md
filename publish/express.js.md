---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 :
저자 :
URL : 
인용 : 

## 강점
1. 라우트 
2. [[미들 웨어]]

express는 정말 가벼운 웹서버!!  **라우팅**과 **로직의 모듈화**를 위해 사용된다.

[[http module]]보다 구조화되고 효과적인 api 코드를 작성할 수 있다. 


### express.js 없이
```
const http = require('http')

const server = http.createServer((req,res) => {
	console.log('some')

	res.sehHeader('Content-type', 'application/json')
	res.end(JSON.stringify({message: "some"}))
})
server.listen(3000, string, callback )
```


### 생각의 연결고리
분야 : [[프레임워크]]
키워드 :

관련있는 메모 : [[http module]] , [[CRUD]]
