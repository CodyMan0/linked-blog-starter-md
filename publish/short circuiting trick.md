---
aliases: [단축평가논리계산법]
tags : 
---

출처 : 벨로퍼트 기술 블로그 
저자 :
URL : https://learnjs.vlpt.us/useful/03-short-circuiting.html
인용 : 


## && 연산자로 코드 단축시키기
&& 많이 썼는데 이제 알았다. truthy 값이면 && 이후의 값이 falsy 값이면 && 이전의 값이 나온다는 것을...

``` jsx
console.log(true && 'hello'); // hello
console.log(false && 'hello'); // false
console.log('hello' && 'bye'); // bye
console.log(null && 'hello'); // null
console.log(undefined && 'hello'); // undefined
console.log('' && 'hello'); // ''
console.log(0 && 'hello'); // 0
console.log(1 && 'hello'); // hello
console.log(1 && 1); // 1
```


## || 연산자로 코드 단축시키기
|| 연산자는 만약 어떤 값이 Falsy 하다면 대체로 사용 할 값을 지정해줄 때 매우 유용하게 사용 할 수 있습니다.

&&와 반대!!!
A || B 라고 할때 Truthy일떈 A Falsy일때는 B


예시 1 
```js
function favoriteDog(someDog) {
	let favoriteDog;
	if(someDog) {
	favoritDog = dog;
	} else {
	favoriteDog = '냐옹';
	}
	return favoriteDog + '입니다'
}

-> 
function favoriteDog(someDog) {
	return (someDog || '냐옹') + '입니다'
}
```

예시 2
```js
const getActiveuserName(user, isLogin) {
if(isLogin) {
	if(user.name) {
	return user.name
	} else {
	return  '이름 없음'
	}
  }
}

-> if (isLogin && user) {
	return user.name || '이름 없음'
}
```

### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[Truthy and Falsy]]
