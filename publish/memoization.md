# 메모이제이션이란
계산 결과를 저장해서 여러번 계산하지 않도록 하는 기법. 



예시 ) 1. 피보나치 수열 (재귀)
==성능 -> On2==
```js
function fibonacci(n) {
	if (n === 0 || n === 1) return n;
	return fibonacci(n - 2) + fibonacci(n - 1);
}

console.log(fibonacci(5));

```

- 메모이제이션
==성능 -> On==
```js
function fibonacci(n, memo) {
	if (n === 0 || n === 1) return n;

	if (memo[n] == null) {
		memo[n] = fibonacci(n - 2, memo) + fibonacci(n - 1, memo);
	}
	return memo[n];
}
```

성능에 문제가 있다. 
-> 중복이 너무 많다. 
-> 계산 값을 저장하는 것 
-> 값이 필요할때 사용하는 것. 

## 성능 비교
```js

let start = new Date();
console.log("재귀", fibonacci1(5));
let end = new Date();
console.log(`${end - start}ms`); // 104ms

let start1 = new Date();
console.log("동적", fibonacci(5, {}));
let end1 = new Date();
console.log(`${end1 - start1}ms`); // 10ms

//n 값이 커지면 커질수록 성능차이가 극명하다. 
//n 값을 40으로 하니 2800 ms 와 0 ms 

```


## 큰 흐름
1. 검색
2. 저장 


## 자료 구조 
해시 테이블(데이터 검색, 삽입)이 빠르다. 

## 단점
1. 속도를 위해 메모리를 사용한다. 




