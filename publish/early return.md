```js
function loginService(isLogin,user) {
if(!isLogin) {
	if(ckechToken()) {
		if(!user.nickName){
		return registerUser(user);
	} else {
	refreshToken();
		return '로그인 성공';
	        }
	}
  } else {
	throw new Error('no Token')
  }
}
```

```js
function loginService(isLogin,user) {
if (isLogin) {
	return 
}

if(!checkToken()){
	throw new Error('no Token')
}

if (!user.nickName) {
return registerUser(user);
}

refreshToken();

return '로그인 성공';



}
```

장점: 사람이 읽기 편한 코드로 바뀜. 

방법: 
1. 원하는 조건을 역으로 바꿔서 리턴 처리를 해서 원하는 조건이 아닐때는 리턴을 할도록 하여 동작의 깊이를 줄인다. 
2. 최상위에 거르는 로직을 하나 선언하는게 좋다