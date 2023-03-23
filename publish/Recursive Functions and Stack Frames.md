- 특징
1. 자기가 자기 자신을 호출하는게 재귀함수 
2. 반복문과 똑같지만 왜 그렇게 했을까? 


[[recursive function]]

## 중요한 원리 1
```js
function solution(n) {

	const inner = (l) => {
	if (l === 0) return;
	else {
		console.log(l);	
		inner(l - 1);
		}
	};
	inner(n);
	
	}

solution(3);

function solution(n) {

	const inner = (l) => {
	if (l === 0) return;
	else {
		inner(l - 1);
		console.log(l);	
		}
	};
	inner(n);
	 
	}

solution(3);
```

위의 예시와 마찬가지로 console.log(l)의 위치만 아래로 했는데 3,2,1,이 1,2,3,이 되어버리는 이유
[[understand by drawing recursive function]]

함수는 스텍에 담긴다. -> 
재귀함수도 함수니깐 스텍에 담긴다. -> 