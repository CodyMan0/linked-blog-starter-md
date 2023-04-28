
# axios

js 런티임 환경에서 사용할 수 있는  Promise 기반의 HTTP 비동기 통신 라이브러리!

##  특징

1. 브라우저를 위해 XMLHttpRequest 생성
2. node.js 위해 http요청 생성
3. Promise API 지원 
4. 요청 및 응답 인터셉트
5. 요청 및 응답 데이터 변환
6. 요청 취소 
7. JSON 데이터 자동 변환
8. XSRF를 막기위한 클라이언트 사이드 지원
9. status code : 200 ~ 300은 정상 그 외는 비정상으로 설정되어 있다.
   -> 이게 무슨 의미지? 즉 status code를 기준 삼아 에러 처리가 용이하다는 것.

## 예제

1. 전역에 디폴트 
```js
axios.default.headers.common['Accept'] = 'application/json'
axios.default.baseURL = 'https://api.example.com'
axios.default.headers.common['Authorization'] = 'AUTH_TOKEN'
```

2. 사용자 지정 

```js
axios.create({
	baseURL: host,
});
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