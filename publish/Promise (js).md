# Promise #✏️

**Promise**는 비동기 처리 상태와 처리 결과를 관리하는 자바스크립트 객체!!
결과값을 내가 원할 때 사용할 수 있다는 것이 가장 큰 장점  


# 특징 
1. 결과값을 받아서 저장 
Promise 객체 이전에는 setTimeout 안에 콜백함수로 비동기를 만들었다.
[[callBack]]
2. [[Promise  chaining]]으로 callback hell 극복

# 상태 

1. Pending : 비동기 처리가 수행되지 않은 상태
2. Fullfilled : 성공 
3. Rejected : 실패


## 동기 비동기

언제 비동기적인 처리를 하는지?
1. 명령을 실행한 후 언제끝날지 예측하기 어렵거나 
2. 주가 되는 작업이 아닐때 비동기
--> ==통신을 할때 많이 쓰인다.==  이거지...!!!
--> 브라우저 서버 간에 페이지 리로드를 하지 않고 자바스크립트를 이용해서 통신하는 것 ([[AJAX]]) 

API는 Promise를 사용한다 왜? 비동기 통신을 하려고

# how? 
어떻게? 비동기 에러처리와 값을 동기적으로 사용할 수 있게 되는거지? 

```js
const promise = new Promise((resolve, reject) => {
	if (비동기 성공) {
	resolve ('result')
	} else {
	reject ('failure reason')
	}
})

const promiseGet = url => {
	return new Promise((resolve, reject) => {
	const xhr = newXMLHttpRequest();
	xhr.open("GET", url)
	xhr.send();

	xhr.onload = () => {
		if (xhr.status === 200) {
		resolve(JSON.parse(xhr.response))
		}
		else {
		reject(new Error(xhr.status))}
	}
	})
}

promiseGet("url")
```

아!! 비동기를 사용할때 왜 에러처리가 힘든지 알았다. 우선 비동기의 에러처리를 알아야한다. 비동기 함수가 실행되면 해당 함수는 호출이 되고 바로 종료가 되어 해당 함수에서 처리하여 얻어지는 값을 상위 스코프에서 값을 가져오지 못하는 상황이 발생한다. 그래서 비동기 함수의 파라미터로 함수를 넘겨주는데 이것이 콜백함수의 정의이다. 파라미터로 넘겨지는 함수를 콜백함수라고 한다. 그래서 에러를 처리하기 위해서 비동
기 함수 내부에서 넘겨받은 콜백함수를 실행하는 방식으로 에러처리를 하였는데 이렇게 하면 가독성이 떨어져 ES6에 나온 Promise 객체를 활용해서 비동기를 동기처럼 사용할 수 있게 해줌. 지금 수준에서 이해하는 방식! 


## 설명
Promise 객체는 executor인 resolve와 reject 콜백함수를 받는다. 








### 관련있는 메모 
1. [[Fetch API]]
2. [[ES6]]
3. [[async-await]]