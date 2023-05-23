
# axios

js 런티임 환경 (브라우저 및 Node.js) 에서 사용할 수 있는  Promise 기반의 HTTP 비동기 통신 라이브러리!

##  Fetch와 비교

![[axios.excalidraw.png]]

1. 브라우저를 위해 XMLHttpRequest 생성
2. node.js 위해 http요청 생성
3. Promise API 지원 
4. 요청 및 응답 인터셉트
5. 요청 및 응답 데이터 변환
6. 요청 취소 
7. JSON 데이터 자동 변환
8. XSRF를 막기위한 클라이언트 사이드 지원
9. status code : 200 ~ 300은 정상 그 외는 비정상으로 설정되어 있다.



## 예제

### 기본 문법
```js
axios({
	url : 'https://test/api...',
	method:'get',
	data: {
		foo: 'test'
	}
})
```


### 요청 파라미터 옵션

1. method
2. url
3. baseURL
4. headers
5. params:
6. timeout
7. response Type : 서버가 응답해주는 데이터의 타입 지정 ( arraybuffer, documetn, json, txt,stream, blob)
8. responseEncoding : 디코딩 응답에 사용하기 위한 인고딩 (utf-8)
9. transformRequest : 서버에 전달되기 전, 요청 데이터를 바꿀 수 있다.
	1. 요청이 POST, DELETE 해당할때만 가능
	2. 배열의 마지막 함수는 string 또는 Buffer 또는 arrayBuffer를 반환
	3. header 객체를 수정 가능
10. transformResponse : 응답 데이터가 만들어지기 전에 변환 가능
11. withCredentials : cross-site access-control 요청을 허용 유무. 이를 true로 하면 cross-origin으로 쿠키을 전달할 수 있다. 
12. maxContentLength : http 응답 내용의 max 사이즈를 지정하는 옵션
13. proxy : proxy 서버의 hostname과 port를 정의하는 옵션
14. cancelToken: 요청을 취소하는데 사용되는 취소토큰을 명시

-> 생각보다 지원해주는 파라미터가 많다. 적잘하게 사용하면 좋겠따. 


```js
axios({ 
	method: "get", // 통신 방식
	url: "www.naver.com", // 서버 
	headers: {'X-Requested-With': 'XMLHttpRequest'} // 요청 헤더 설정 
	params: { api_key: "1234", langualge: "en" }, // ?파라미터를 전달 
	responseType: 'json', // default 
	maxContentLength: 2000, // http 응답 내용의 max 사이즈 
	validateStatus: function (status) { return status >= 200 && status < 300; // default }, // HTTP응답 상태 코드에 대해 promise의 반환 값이 resolve 또는 reject 할지 지정 
	proxy: { 
		host: '127.0.0.1',
		port: 9000,
		auth: { username: 'mikeymike', password: 'rapunz3l' }
	}, // proxy서버의 hostname과 port를 정의
	maxRedirects: 5, // node.js에서 사용되는 리다이렉트 최대치를 지정 
	httpsAgent: new https.Agent({ keepAlive: true }), // node.js에서 https를 요청을 할때 사용자 정의 agent를 정의 })
.then(function (response) { // response Action });
```



### 응답 데이터
1. data : 응답 데이터
2. status 상태 코드
3. statusText : 상태 메세지
4. headers : 서버가 보내준 해더
5. config : 요청에 대한 axios에 설정된 환경 설정
6. request : 응답을 생성한 요청 : 브라우저는 XMLHttpRequest 인스턴스 
7. 전역에 디폴트 



### axios GET
```js
async function getUser() {
	try { 
		const response = await axios.get('/user?ID=12345');
		console.log(response); 
		}
	catch (error) {
	 console.error(error); 
	 } 
}
```


## Axios의 응용 메소드
### 1. axios 동시 요청 

```js
function getUserAccount() {
	return axios.get('user/123')
}

function getUserPermissions(){
	return axios.get('user/123/permissions')
}

axios.all([getUserAccount() , getUserPermssions()])
	.then(axios.spread((acct, perms) => {
	// 성공시 조건
	}))
```

### 2. axios Instance 만들기

```js
//axios.create({baseURL: host});

const instance = axios.create({
	baseURL : 'http://localhost/api',
	timeout:1000,
	headers: {"X-Custom-Header" : 'foobar'}
})
```

```js
axios.default.headers.common['Accept'] = 'application/json'
axios.default.baseURL = 'https://api.example.com'
axios.default.headers.common['Authorization'] = 'AUTH_TOKEN'
```

### 3. axios로 폼데이터 보내기
```js
const addCustomer = () => {
	const url = 환경변수
	const formData = new FormData();
	formData.append("image", file);
	formData.append("name", userName);
	formData.append("birthday", birthday);
	formData.append("gender", gender);
	formData.append("job", job);
	const config = {
		headers ={
			"content-type" : "multipart/form-data"
		}
	};
	return axios.post(url,formData, config)
}

```


### 4. 원격 이미지 다운 받기
```js
const imgurl = 'https://play-lh.googleusercontent.com/hYdIazwJBlPhmN74Yz3m_jU9nA6t02U7ZARfKunt6dauUAB6O3nLHp0v5ypisNt9OJk';

axios({
	url : imgurl,
	method: 'GET,
	responseType:'blob'
})
.then((response) => {
	const url = URL.createObjectURL( new Blob([response.data]))// blob 데이터를 객체 url로 변환
})
```

==2. cancelToken==
   요청을 취소해야하는 로직이 있을 경우 axios의 cancelToken 메소드를 사용하면 쉽게 구현할 수 있다.

3. 인터셉터
   then 또는 catch로 처리되기 전에 요청과 응답을 가로챌 수 있다.
   Express의 미들웨어를 설정하듯 서버로 보낸 get 요청의 response를 받기 전에 **공통된** 로직을 넣어 사용할 수 있다.

예시) 에러처리(공통적인 부분이니!)

- axios에 인터셉터 추가 
```js
axios.interceptors.request.use(config => P
  // 요청을 보내기 전 로직
  return config
), (err) => {
  return Promise.reject(err)
})
```


- instance에 인터셉터 추가 
```js
const authFetch = axios.create({
	baseURL: "https://course-api.com",
});

authFetch.interceptors.request.use(
	(request) => {
		request.headers.common["Accept"] = "application/json";
		console.log("request sent");
		return request;
	},
	(error) => {
		return Promise.reject(error);
	}
);
```


## fetch와 비교
1.  response timeout 처리 방법이 있다. (fetch에는 존재하지 않는 기능)
2. 크로스 브라우징에 신경을 많이썼기에 브라우저 호환성이 뛰어나다.

### 관련 있는 메모
1. [[Fetch API]]